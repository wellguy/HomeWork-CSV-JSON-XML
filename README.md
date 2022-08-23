# Задача 1: CSV - JSON парсер

## Описание
Конвертер CSV и XML в формат JSON, а так же парсер JSON файлов в Java классы.

В качестве исходной информации создайте файл `data.csv` со следующим содержимым и поместите его в корень созданного проекта:
```csv
1,John,Smith,USA,25
2,Inav,Petrov,RU,23
```
Помимо этого потребуется класс `Employee`, который будет содержать информацию о сотрудниках. Для парсинга Java классов из CSV потребуется пустой конструктор класса.
```java
public class Employee {
    public long id;
    public String firstName;
    public String lastName;
    public String country;
    public int age;

    public Employee() {
        // Пустой конструктор
    }

    public Employee(long id, String firstName, String lastName, String country, int age) {
        this.id = id;
        this.firstName = firstName;
        this.lastName = lastName;
        this.country = country;
        this.age = age;
    }   
}
``` 
В резльтате работы программы в корне проекта должен появиться файл `data.json` со следующим содержимым:
```json
[
  {
    "id": 1,
    "firstName": "John",
    "lastName": "Smith",
    "country": "USA",
    "age": 25
  },
  {
    "id": 2,
    "firstName": "Inav",
    "lastName": "Petrov",
    "country": "RU",
    "age": 23
  }
]
```

## Реализация
Первым делом в классе `Main` в методе `main()` создан массив строчек `columnMapping`, содержащий информацию о предназначении колонок в CVS файле:
```java
String[] columnMapping = {"id", "firstName", "lastName", "country", "age"};
```
Далее определено имя для считываемого CSV файла:
```java
String fileName = "data.csv";
```
Далее получен список сотрудников, вызвав метод `parseCSV()`:
```java
List<Employee> list = parseCSV(columnMapping, fileName);
```

Полученный список преобразован в строчку в формате JSON  метода `listToJson()
```java
String json = listToJson(list);
```
При написании метода `listToJson()` понадобятся объекты типа `GsonBuilder` и `Gson`. Для преобразования списка объектов в JSON, требуется определить тип этого спика:
```java
Type listType = new TypeToken<List<T>>() {}.getType();
```
Получить JSON из экземпляра класса `Gson` можно с помощтю метода `toJson()`, передав в качестве аргументов список сотрудников и тип списка:
```java
String json = gson.toJson(list, listType);
```
Далее записан полученный JSON в файл с помощью метода `writeString()`.

## [Задание из курсов java-разработчик](https://github.com/netology-code/jd-homeworks/blob/master/special_files/task1/README.md)
