```ts
endpoints:
...

endpoint_name: builder.mutation<интерфейс_ответа_запроса, интерфейс_аргумента_запроса>({
	query(body) {
		return {
			url: '...'.
			method: '...',
			body: '...',
		}
	}
})

```