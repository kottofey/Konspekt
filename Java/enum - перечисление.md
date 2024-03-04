#enum
_Это **тип данных**, переменные которого принимают только значения из небольшого фиксированного списка_
```java
enum Day
{
   MONDAY,
   TUESDAY,
   WEDNESDAY,
   THURSDAY,
   FRIDAY,
   SATURDAY,
   SUNDAY
}
```

|Код|Примечание|
|---|---|
|Day day = Day.MONDAY; |Понедельник|
|int index = day.ordinal();|Получаем индекс понедельника (0)|
|Day newDay = Day.values()[index+2];|День недели на 2 дня позже понедельника|

- Элементы можно сравнивать через ==
- При компиляции enum превращается в обычный класс, поэтому внутри enum можно объявлять свои методы:
```java
enum Day
{
   MONDAY,
   TUESDAY,
   WEDNESDAY,
   THURSDAY,
   FRIDAY,
   SATURDAY,
   SUNDAY;

   public static List<Day> asList()
   {
      ArrayList<Day> list = new ArrayList<Day>();

      Collections.addAll(list, values());

      return list;
   }

}
```
вызов:
```java
List<Day> list = Day.asList();
```
