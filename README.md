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


# Задача 2: XML - JSON парсер

## Описание
В данной задаче вам предстоит произвести запись в файл JSON объекта, полученного из XML файла.

Данную задачу выполняйте в рамках созданного в предыдущей задаче проекта.

В качестве исходной информации создан файл `data.xml` со следующим содержимым (поместите этот файл в корень проекта):
```xml
<staff>
    <employee>
        <id>1</id>
        <firstName>John</firstName>
        <lastName>Smith</lastName>
        <country>USA</country>
        <age>25</age>
    </employee>
    <employee>
        <id>2</id>
        <firstName>Inav</firstName>
        <lastName>Petrov</lastName>
        <country>RU</country>
        <age>23</age>
    </employee>
</staff>
```
В резyльтате работы программы в корне проекта должен появиться файл `data2.json` с содержимым, аналогичным json-файлу из предыдущей задачи.

## Реализация
Для получения списка сотрудников из XML документа используется метод `parseXML()`:
```java
List<Employee> list = parseXML("data.xml");
```
При реализации метода `parseXML()` необходимо получить экземпляр класса `Document` с использованием `DocumentBuilderFactory` и `DocumentBuilder` через метод `parse()`. Далее получаем из объекта `Document` корневой узел `Node` с помощью метода `getDocumentElement()`. Из корневого узла извлекается список узлов `NodeList` с помощью метода `getChildNodes()`. По списку узлов и получен из каждого из них `Element`. У элементов получены значения, с помощью которых создан экземпляр класса `Employee`. Так как элементов может быть несколько, организован цикле. Метод `parseXML()` должен возвращет список сотрудников. 

С помощью ранее написанного метода `listToJson()` преобразован список в JSON и записан в файл c помощью метода `writeString()`.



## [Задание из курсов java-разработчик](https://github.com/netology-code/jd-homeworks/blob/master/special_files/task1/README.md)
