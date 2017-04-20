Few examples to show you how to format `java.time.LocalDateTime` in Java 8.

## 1\. LocalDateTime + DateTimeFormatter

To format a LocalDateTime object, uses `DateTimeFormatter`

TestDate1.java

    package com.mkyong.time;

    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;

    public class TestDate1 {
        public static void main(String[] args) {

            //Get current date time
            LocalDateTime now = LocalDateTime.now();

            System.out.println("Before : " + now);

            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

            String formatDateTime = now.format(formatter);

            System.out.println("After : " + formatDateTime);

        }
    }

Output

    Before : 2016-11-09T11:44:44.797

    After  : 2016-11-09 11:44:44

## 2\. String -> LocalDateTime

Another example to convert a String to `LocalDateTime`

TestDate2.java

    package com.mkyong.time;

    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;

    public class TestDate2 {
        public static void main(String[] args) {

            String now = "2016-11-09 10:30";

            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");

            LocalDateTime formatDateTime = LocalDateTime.parse(now, formatter);

            System.out.println("Before : " + now);

            System.out.println("After : " + formatDateTime);

            System.out.println("After : " + formatDateTime.format(formatter));

        }
    }

Output

    Before : 2016-11-09 10:30

    After : 2016-11-09T10:30

    After : 2016-11-09 10:30

## References

1.  [DateTimeFormatter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)
2.  [Java 8 – How to convert String to LocalDate](http://www.mkyong.com/java8/java-8-how-to-convert-string-to-localdate/)

[http://www.mkyong.com/java8/java-8-how-to-format-localdatetime/](http://www.mkyong.com/java8/java-8-how-to-format-localdatetime/)
