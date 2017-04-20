In Java 8, you can use the predefined `java.time.temporal.TemporalAdjusters` to adjust a date or [Temporal](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/Temporal.html)

## 1\. TemporalAdjusters

Example to move a date to firstDayOfMonth, firstDayOfNextMonth, next Monday and etc.

TestDate.java

    package com.mkyong.time;

    import java.time.DayOfWeek;
    import java.time.LocalDate;
    import java.time.temporal.TemporalAdjusters;

    public class TestDate {

        public static void main(String[] args) {

            LocalDate localDate = LocalDate.now();
            System.out.println("current date : " + localDate);

            LocalDate with = localDate.with(TemporalAdjusters.firstDayOfMonth());
            System.out.println("firstDayOfMonth : " + with);

            LocalDate with1 = localDate.with(TemporalAdjusters.lastDayOfMonth());
            System.out.println("lastDayOfMonth : " + with1);

            LocalDate with2 = localDate.with(TemporalAdjusters.next(DayOfWeek.MONDAY));
            System.out.println("next monday : " + with2);

            LocalDate with3 = localDate.with(TemporalAdjusters.firstDayOfNextMonth());
            System.out.println("firstDayOfNextMonth : " + with3);

        }

    }

Output

    current date : 2016-11-15
    firstDayOfMonth : 2016-11-01
    lastDayOfMonth : 2016-11-30
    next monday : 2016-11-21
    firstDayOfNextMonth : 2016-12-01

**Note**  
Please check this [official TemporalAdjusters JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjusters.html) for the entire list of the predefined TemporalAdjusters.

## 2\. Custom TemporalAdjuster

Example to implement `TemporalAdjuster` to move a date to next Christmas.

NextChristmas.java

    package com.mkyong.time;

    import java.time.temporal.ChronoField;
    import java.time.temporal.Temporal;
    import java.time.temporal.TemporalAdjuster;

    public class NextChristmas implements TemporalAdjuster {

        @Override
        public Temporal adjustInto(Temporal temporal) {

            return temporal.with(ChronoField.MONTH_OF_YEAR, 12).with(ChronoField.DAY_OF_MONTH, 25);

        }
    }

TestDate.java

    package com.mkyong.time;

    import java.time.LocalDate;

    public class TestDate {

        public static void main(String[] args) {

            LocalDate localDate = LocalDate.now();
            System.out.println("current date : " + localDate);

            localDate = localDate.with(new NextChristmas());
            System.out.println("Next Christmas : " + localDate);

        }

    }

Output

    current date : 2016-11-15
    Next Christmas : 2016-12-25

Alternatively, you can use the following lambda expression :

    localDate = localDate.with(
    	temporal -> temporal.with(ChronoField.MONTH_OF_YEAR, 12).with(ChronoField.DAY_OF_MONTH, 25)
    );

## References

1.  [Java 8 – HijrahDate, How to calculate the Ramadan date](http://www.mkyong.com/java8/java-8-hijrahdate-how-to-calculate-the-ramadan-date/)
2.  [TemporalAdjuster JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjuster.html)
3.  [TemporalAdjusters JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjusters.html)
4.  [Temporal JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/Temporal.html)
5.  [Wikipedia Christmas](https://en.wikipedia.org/wiki/Christmas)

[http://www.mkyong.com/java8/java-8-temporaladjusters-examples/](http://www.mkyong.com/java8/java-8-temporaladjusters-examples/)
