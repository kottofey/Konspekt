```MySQL ln=1
SELECT
	(
		SELECT
			COUNT(*)
		FROM
			users
		WHERE
			STATUS = 1
			AND id != 1
			AND deleted_at IS NULL
			AND group_id IN (2, 3, 4, 7)
	) AS constant_users,
	(
		SELECT
			COUNT(*)
		FROM
			users
		WHERE
			STATUS = 1
			AND id != 1
			AND deleted_at IS NULL
			AND group_id NOT IN (3, 7, 4, 2)
	) AS temporary_users,
	(
		SELECT
			COUNT(*)
		FROM
			users
		WHERE
			STATUS = 1
			AND id != 1
			AND deleted_at IS NULL
	) AS total
```