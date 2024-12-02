# Мое изучение JAVA

По правилам Объектно-ориентированного программирования для того, чтобы создать функцию, необходимо создать объект, который будет находится эта функция. По сути объект будет выполнять эту функцию. Для того, чтобы создать объект, необходимо создать его класс, в котором будет находится описание типа данных.


|**Основы**||
|-|-|
|Файл с расширение FileName.java содержит информацию о коде программы.| Код программы находится внутри блока  public class FileName{}. Программа может иметь один или несколько файлов с расширением .java|
|public static void main(String[] args) {}|Метод находится внутри блока public class FileName {}  и отвечает за то, что запускает приложение в этом классе. Метод - это часть кода, в которой прописан порядок действий, которые можно вызвать неограниченное количество раз. |
|**Часто используемые типы переменных**||
|**Переменная** - это контейнер, в котором может храниться некоторое значение данных для дальнейшего использования в программе. Имена переменных должны быть написаны в **camelCase** - первая буква строчная, каждое следующее слово в имени с заглавной буквы и без нижних подчеркиваний или пробелов. В качестве идентификаторов **нельзя** использовать ключевые слова **Java**. |К ключевым словам языка **Java** относятся: abstract assert boolean break byte case catch char class const continue default do double else enum extends final finally float for goto if implements import instanceof int interface long native new package private protected public.|
|int|Целые числа|
|double|Числа с плавающей запятой|
|char|Используется для хранения символов в кодировке Unicode|
|boolean|Логический тип данных (false - ложь, true - правда)|
|||
|Ссылочные типы переменных||
|||
|**Переменные**||
|||
|Объявление переменной| int a;|
|Присвоение значения переменной|a = 10;|
|Возможно объединение объявления переменной и присвоения ей значения|int a = 10;|
|Приведение переменных одного типа к другому| double x = 75,78;  int y = (int) x; |
|**Сокращения для удобства ввода**||
|psvm| public static void main(String[] args) {} |
|sout|System.out.println() |
|souf|System.out.printf("");|
|psfs|public static final String|
|||
|**Прочее**||
|Подключение библиотек происходит в файле pom.xml  в теге <dependencies></dependencies>||
|Сборник библиотек для Maven|https://Maven Central Repository: mvnrepository.com/repos/central|

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

- **Surefire** - плагин для Maven, без которого автотесты могут не запускаться  

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

- **TelegramBot** -  библиотека для подключения телеграмм бота.

[Библиотека](https://github.com/rubenlagus/TelegramBots/blob/aad139de980ae25ee7a4b06bbe7644c6077421ce/TelegramBots.wiki/Getting-Started.md)

```java

    <dependency>
        <groupId>org.telegram</groupId>
        <artifactId>telegrambots</artifactId>
        <version>6.8.0</version>
    </dependency>
```


