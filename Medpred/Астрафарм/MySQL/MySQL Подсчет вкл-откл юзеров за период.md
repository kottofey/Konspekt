
```MySQL ln=1
-- Сие чудо инженерной мысли подсчитывает подключение/отключение юзеров
-- для указанного периода на 69-70 строках, дабы не взрывать мозг
-- ручным просмотром логов в СРМ для Астрафарма.

-- Подсчет ведется для "Постоянных" пользователей из групп:
-- Администраторы, РМ, ТП и ВВ (айдишники: 2, 3, 4, 7)
-- На всякий случай если будет действие restore нужно проконтролировать
-- повдение и пересчитать вручную. Для этого можно отключить
-- HAVING на 78й строке и оно выведет все строки для всех дат

SELECT
	COALESCE(day_date, 'Total') AS period,
	SUM(status_change) AS total_change
FROM
	(
		SELECT
			DATE(FROM_UNIXTIME(`datetime`)) AS day_date,
			SUM(
				CASE
					-- status 0 or 1
					WHEN COALESCE(old_status, '0') = '0'
						AND COALESCE(new_status, '0') = '1' THEN
						1
					WHEN COALESCE(old_status, '0') = '1'
						AND COALESCE(new_status, '0') = '0' THEN
						- 1
						-- status NULL
					WHEN COALESCE(old_status, '0') = NULL
						AND COALESCE(new_status, '0') = '1' THEN
						1
					WHEN COALESCE(old_status, '0') = '1'
						AND COALESCE(new_status, '0') = NULL THEN
						- 1
						-- deleted_at
					WHEN COALESCE(old_del, '0') = NULL
						AND COALESCE(new_del, '0') = '1' THEN
						- 1
					WHEN COALESCE(old_del, '0') = '1'
						AND COALESCE(new_del, '0') = NULL THEN
						1
					WHEN action = 'delete' THEN
						- 1
					WHEN action = 'restore' THEN
						'9000'
						-- default
					ELSE
						0
				END
			) AS status_change
		FROM
			(
				SELECT
					`datetime`,
					IF(json_valid(log_details), COALESCE(JSON_UNQUOTE(JSON_EXTRACT(log_details, '$.previous.status')), '0'), '0') AS old_status,
					IF(json_valid(log_details), COALESCE(JSON_UNQUOTE(JSON_EXTRACT(log_details, '$.changes.status')), '0'), '0') AS new_status,
					IF(json_valid(log_details), COALESCE(JSON_UNQUOTE(JSON_EXTRACT(log_details, '$.previous.deleted_at')), '0'), '0') AS old_del,
					IF(json_valid(log_details), COALESCE(JSON_UNQUOTE(JSON_EXTRACT(log_details, '$.changes.deleted_at')), '0'), '0') AS new_del,
					`action`
				FROM
					`logs`
				WHERE
					`model_name` = 'user'
					AND (log_details LIKE '%status%' OR log_details LIKE '%deleted_at%' OR action IN ('create', 'update', 'delete', 'restore'))

					-- Здесь указаны группы для "постоянных" пользователей
					AND `model_id` IN (SELECT id FROM users WHERE group_id IN (2, 3, 4, 7))
					
					-- Здесь нужно поменять период дат на нужный по времени МСК
					AND `datetime` BETWEEN UNIX_TIMESTAMP('2025-05-26 00:00:00' - INTERVAL 3 HOUR)
					AND UNIX_TIMESTAMP('2025-05-26 23:59:59' - INTERVAL 3 HOUR)
					
			) AS subquery
		GROUP BY
			day_date WITH ROLLUP
	) AS final_data
GROUP BY
	period
	HAVING total_change != 0
ORDER BY
	CASE
		WHEN period = 'Total' THEN
			1
		ELSE
			0
	END,
	period ASC;
```