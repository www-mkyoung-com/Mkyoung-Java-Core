In this tutorial, we will show you how to get the current date time from the classic [Date](http://docs.oracle.com/javase/8/docs/api/java/util/Date.html) and [Calendar](http://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html) APIs, and also the new Java 8 date and time APIs – [LocalDateTime](http://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html) and [LocalDate](http://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)

## 1\. Code Snippets

For `java.util.Date`, just create a new Date()

    DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
    Date date = new Date();
    System.out.println(dateFormat.format(date)); //2016/11/16 12:08:43

For `java.util.Calendar`, uses Calendar.getInstance()

    DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
    Calendar cal = Calendar.getInstance();
    System.out.println(dateFormat.format(cal)); //2016/11/16 12:08:43

For `java.time.LocalDateTime`, uses LocalDateTime.now()

    DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
    LocalDateTime now = LocalDateTime.now();
    System.out.println(dtf.format(now)); //2016/11/16 12:08:43

For `java.time.LocalDate`, uses LocalDate.now()

    DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd");
    LocalDate localDate = LocalDate.now();
    System.out.println(dtf.format(localDate)); //2016/11/16

## 2\. Full Example

Review a full Java example to show you how to get the current date, time and display in a predefined format.

GetCurrentDateTime.java

    package com.mkyong;

    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;
    import java.util.Calendar;
    import java.util.Date;

    public class GetCurrentDateTime {

        private static final DateFormat sdf = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
        private static final DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");

        public static void main(String[] args) {

            Date date = new Date();
            System.out.println(sdf.format(date));

            Calendar cal = Calendar.getInstance();
            System.out.println(sdf.format(cal.getTime()));

            LocalDateTime now = LocalDateTime.now();
            System.out.println(dtf.format(now));

            LocalDate localDate = LocalDate.now();
            System.out.println(DateTimeFormatter.ofPattern("yyy/MM/dd").format(localDate));

        }

    }

Output

    2016/11/16 12:08:43
    2016/11/16 12:08:43
    2016/11/16 12:08:43
    2016/11/16

## References

1.  [Date JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/util/Date.html)
2.  [Calendar JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html)
3.  [SimpleDateFormat JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)
4.  [LocalDateTime JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)
5.  [LocalDate JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)
6.  [DateTimeFormatter JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)

[http://www.mkyong.com/java/java-how-to-get-current-date-time-date-and-calender/](http://www.mkyong.com/java/java-how-to-get-current-date-time-date-and-calender/)
