# Мое изучение JAVA

По правилам Объектно-ориентированного программирования для того, чтобы создать функцию, необходимо создать объект, котором будет находится эта функция. По сути объект будет выполнять эту функцию. Для того, чтобы создать объект, необходимо создать его класс, в котором будет находится описание типа данных.


**Основы**

Файл с расширение FileName.java содержит информацию о коде программы.
Код программы находится внутри блока  public class FileName{}.
Программа может иметь один или несколько файлов с расширением .java

```java
 public class Main {
    public static void main(String[] args){
        // Метод находится внутри блока  и отвечает за то, что запускает приложение в этом классе.
        // Метод - это часть кода, в которой прописан порядок действий, который можно вызвать неограниченное количество раз.
        // void - ставится, когда метод не требует вывода, то есть в конце метода не ставится return
        // 
    }
 }
```

**Переменная** - это контейнер, в котором может храниться некоторое значение данных для дальнейшего использования в программе. 
* Имена переменных должны быть написаны в **camelCase** - первая буква строчная, каждое следующее слово в имени с заглавной буквы и без нижних подчеркиваний или пробелов. В качестве идентификаторов **нельзя** использовать ключевые слова **Java**.
* К ключевым словам языка **Java** относятся: abstract assert boolean break byte case catch char class const continue default do double else enum extends final finally float for goto if implements import instanceof int interface long native new package private protected public.

*Типы переменных*
* int - Целые числа
* double - Числа с плавающей запятой
* char - Используется для хранения символов в кодировке Unicode
* boolean - Логический тип данных (false - ложь, true - правда)
- Ссылочные типы переменных - 

|||
|-|-|
|Объявление переменной| int a;|
|Присвоение значения переменной|a = 10;|
|Возможно объединение объявления переменной и присвоения ей значения|int a = 10;|
|Приведение переменных одного типа к другому| double x = 75,78;  int y = (int) x; |

**Циклы**

Циклы позволяют в зависимости от определенных условий выполнять определенное действие множество раз. В языке Java есть следующие виды циклов:

* for
```java
  for ([инициализация счетчика]; [условие]; [изменение счетчика])
  {
    // действия
  }
```

* while - сразу проверяет истинность некоторого условия, и если условие истинно, то код цикла выполняется
```java
  int j = 6;
  while (j > 0){
 
    System.out.println(j);
    j--;
  }
```

* do...while - Цикл do сначала выполняет код цикла, а потом проверяет условие в инструкции while. И пока это условие истинно, цикл повторяется. 
```java
  int j = 7;
  do{
    System.out.println(j);
    j--;
  }
  while (j > 0);
```
* Операторы continue и break
  * break - позволяет выйти из цикла в любой его момент, даже если цикл не закончил свою работу
  ```java
    for (int i = 0; i < 10; i++){
      if (i == 5)
         break;
      System.out.println(i);
    }
   ```
  * continue - позволяет пропустить итерацию цикла.
  ```java
    for (int i = 0; i < 10; i++){
      if (i == 5)
        continue;
      System.out.println(i);
    }
  ```

**Прочее**

* == - подходит только для инт переменных
* .equals (name.equals("name")) - используется для сравнения  других типов переменных
* .lenght  - определение длинны слова, строки, массива для сравления

**Continuous Integration**
непрерывная интеграция - это практика разработки ПО, при которой участники команды интегрируют изменения настолько часто, насколько это возможно (как минимум,
ежедневно или несколько раз в день). Каждая интеграция верифицируется автоматической сборкой, включая тесты, для определения ошибок интеграции настолько быстро, насколько это возможно. 
Шаблон для Maven

``` 
name: Java CI with Maven

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up JDK 17
      uses: actions/setup-java@v2
      with:
        java-version: '17'
        distribution: 'adopt'
    - name: Build with Maven
      run: mvn -B -e verify

```

**Подключение пакетов**
Package  — это механизм организации классов и интерфейсов в логические группы. Он помогает управлять пространством имён, обеспечивая структурирование и упорядочивание кода.

 package -  название пакета может составляться из groupId.artifactId.namePackage

```java
   package ru.netology.services;
   // Для перемещения  пакета в папку используется Alt+Enter, далее "Move to package..." 
```
```java
// Для привязки файла в классе Main используется импорт 
   import ru.netology.services.IncomeCalculationService;

```

**Тесты**

Тесты создаются в папке src/test. Название класса повторяет название основного класса с добавлением в название *Test.
* Переменная expected содержит ожидаемый результат
* Переменная actual - результат вычисления метода.
Для запуска тестов в файл pom.xml добавляется зависимость JUnit Jupiter и плагин Surefire

```java

  public class NameClassTest {

    @Test
    public void nameTest() {

        NameClass service = new NameClass();

        int expected = ;
        int actual = service.nameMetod();

        Assertions.assertEquals(expected, actual);
    }
  }

```


**Параметризированные тесты**

Параметризированные тесты - это тесты, которые дают возможность прогонять один и тот же тест с разными входящими параметрами. Параметры для теста находятся в специальном файле, который подгружается к тестам.

```java

public class NameClassTest {

    @ParameterizedTest
    @CsvSource(files = "src/test/resources/nameMetod.csv")
    public void nameTest(параметры) {

        NameClass service = new NameClass();

        int actual = service.nameMetod();

        Assertions.assertEquals(expected, actual);
    }
  }

```
```
nameMetod.csv
3, 10000, 3000, 20000
2, 100000, 60000, 150000
```



**Библиотеки**

Подключение библиотек происходит в файле pom.xml  в теге ```<dependencies></dependencies>```

Сборник библиотек для Maven: https://mvnrepository.com/

- **Apache HttpClient** - Библиотека для HTTP  запросов

```java

     <dependency>
        <groupId>org.apache.httpcomponents.client5</groupId>
        <artifactId>httpclient5</artifactId>
        <version>5.3</version>
     </dependency>
```

- **Jackson Databind** - позволяет переводить данные полученные в Json формате в данные понятные для прочтения Java. Основной функционал для работы с форматом JSON предоставляет класс ObjectMapper.

```java

    <dependency>
       <groupId>com.fasterxml.jackson.core</groupId>
       <artifactId>jackson-databind</artifactId>
       <version>2.16.2</version>
    </dependency>
```

- **JUnit Jupiter** - это модуль для работы с автотестами|

```java 

    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.10.2</version>
        <scope>test</scope>
    </dependency>
```

- **Surefire** - плагин для Maven, без которого автотесты могут не запускаться  подключается в теге <build> </build>

```java

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.2</version>
                <configuration>
                   <failIfNoTests>true</failIfNoTests>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

**JaCoCo**

Code Coverage — метрика, показывающая, насколько наш код покрыт автотестами, т.е. % запущенного в результате прогона автотестов.

```

  <plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.11</version>

    <executions>
      <execution>
        <id>prepare-agent</id>
        <goals>
          <goal>prepare-agent</goal>
        </goals>
      </execution>

      <execution>
        <id>report</id>
        <phase>verify</phase>
          <goals>
            <goal>report</goal>
          </goals>
      </execution>

      <execution>
        <id>check</id>
        <goals>
          <goal>check</goal>
        </goals>
        <configuration>
          <rules>
            <rule>
              <limits>
                <limit>
                  <counter>BRANCH</counter>
                  <value>COVEREDRATIO</value>
                  <minimum>100%</minimum>
                </limit>
              </limits>
            </rule>
          </rules>
        </configuration>
     </execution>
    </executions>
  </plugin> 

```
**Lombok**
Программа для Maven  для создания базовых конструкторов

```java
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>1.18.36</version>
		<scope>provided</scope>
	</dependency>

```

- **TelegramBot** -  библиотека для подключения телеграмм бота.

[Библиотека](https://github.com/rubenlagus/TelegramBots/blob/aad139de980ae25ee7a4b06bbe7644c6077421ce/TelegramBots.wiki/Getting-Started.md)

```java

    <dependency>
        <groupId>org.telegram</groupId>
        <artifactId>telegrambots</artifactId>
        <version>6.8.0</version>
    </dependency>
```
- **Maven-checkstyle-plugin** - плагин для проверки правильности написания переменных. В случае если переменная названа с заглавной буквы, то тест обружается.

```java

  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.2.1</version>
    <configuration>
        <checkstyleRules>
            <module name="Checker">
                <module name="TreeWalker">
                    <module name="LocalVariableName"/>
                </module>
            </module>
        </checkstyleRules>
    </configuration>
    <executions>
        <execution>
            <id>validate</id>
                <phase>validate</phase>
                <goals>
                    <goal>check</goal>
                </goals>
            </execution>
        </executions>
    </plugin>

```
|**Сокращения для удобства ввода**||
|-|-|
|psvm| public static void main(String[] args) {} |
|sout|System.out.println() |
|souf|System.out.printf("");|
|psfs|public static final String|



