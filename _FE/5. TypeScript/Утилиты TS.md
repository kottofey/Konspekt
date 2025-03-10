```ts
type IPartial = Partial<T> // Делает все ключи Т необязательными

type IRequired = Required<T> // Делает все ключи Т обязательными

type INonNullable = NonNullable<T> // Убирает все типы null и  undefined

type IRecord = Record<'a1' | 'a2' | 'a3', number>
const record: IRecord = {a1: 1, a2: 2, a3: 3}
/* эквивалентно */
const record: {a1: number, a2: number, a3: number}

const readonly: Readonly<T> = {a: 1, b: 2} // делает все поля объекта Т константами
/* эквивалентно */
const readonly = <const>{a: 1, b: 2}
/* или */
const readonly = {a: 1, b: 2} as const

type IReadonlyArray = ReadOnlyArray<T> // делает элементы массива Т readonly
```

- Pick<T, a | b> - оставляет только поля a и b
- Extract<T, U> - оставляет только общие поля T и U
- Exclude<T, U> - оставляет только уникальные несовпадающие поля T и U
- Omit<T, a | b> - оставляет все ключи кроме a и b

```ts
function f1(a: string, b: number): boolean {
	return a.length > b.toString().length
}

class C1 {
	a: boolean
	b: string
	
	constructor(a: number, b: string) {
		this.a = a
		this.b = b
	}
}

type A = typeof f1
type B = typeof C1

type AA = Parameters<A> // [string, number]
type BB = ConstructorParameters<B> // [number, string]

type IReturnType = ReturnType<f1> // boolean (см функцию выше)
type IInstanceType = InstanceType<B> // C1, потому что тип В возвращает тип конструктора класса C1, см выше

```