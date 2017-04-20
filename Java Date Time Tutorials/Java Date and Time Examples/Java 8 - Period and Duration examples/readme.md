Few examples to show you how to use Java 8 `Duration`, `Period` and `ChronoUnit` objects to find out the difference between dates.

1.  Duration – Measures time in seconds and nanoseconds.
2.  Period – Measures time in years, months and days.

## 1\. Duration Example

A `java.time.Duration` example to find out difference seconds between two `LocalDateTime`

DurationExample.java

    package com.mkyong.time;

    import java.time.Duration;
    import java.time.LocalDateTime;
    import java.time.Month;
    import java.time.temporal.ChronoUnit;

    public class DurationExample {

        public static void main(String[] args) {

    		// Creating Durations
            System.out.println("--- Examples --- ");

            Duration oneHours = Duration.ofHours(1);
            System.out.println(oneHours.getSeconds() + " seconds");

            Duration oneHours2 = Duration.of(1, ChronoUnit.HOURS);
            System.out.println(oneHours2.getSeconds() + " seconds");

    		// Test Duration.between
            System.out.println("\n--- Duration.between --- ");

            LocalDateTime oldDate = LocalDateTime.of(2016, Month.AUGUST, 31, 10, 20, 55);
            LocalDateTime newDate = LocalDateTime.of(2016, Month.NOVEMBER, 9, 10, 21, 56);

            System.out.println(oldDate);
            System.out.println(newDate);

            //count seconds between dates
            Duration duration = Duration.between(oldDate, newDate);

            System.out.println(duration.getSeconds() + " seconds");

        }
    }

Output

    --- Examples ---
    3600 seconds
    3600 seconds

    --- Duration.between ---
    2016-08-31T10:20:55
    2016-11-09T10:21:56
    6048061 seconds

## 2\. Period Example

A `java.time.Period` example to find out differently (years, months, days) between two `LocalDates`

PeriodExample.java

    package com.mkyong.time;

    import java.time.LocalDate;
    import java.time.Month;
    import java.time.Period;

    public class PeriodExample {

        public static void main(String[] args) {

            System.out.println("--- Examples --- ");

            Period tenDays = Period.ofDays(10);
            System.out.println(tenDays.getDays()); //10

            Period oneYearTwoMonthsThreeDays = Period.of(1, 2, 3);
            System.out.println(oneYearTwoMonthsThreeDays.getYears());   //1
            System.out.println(oneYearTwoMonthsThreeDays.getMonths());  //2
            System.out.println(oneYearTwoMonthsThreeDays.getDays());    //3

            System.out.println("\n--- Period.between --- ");
            LocalDate oldDate = LocalDate.of(1982, Month.AUGUST, 31);
            LocalDate newDate = LocalDate.of(2016, Month.NOVEMBER, 9);

            System.out.println(oldDate);
            System.out.println(newDate);

            // check period between dates
            Period period = Period.between(oldDate, newDate);

            System.out.print(period.getYears() + " years,");
            System.out.print(period.getMonths() + " months,");
            System.out.print(period.getDays() + " days");

        }
    }

Output

    --- Examples ---
    10
    1
    2
    3

    --- Period.between ---
    1982-08-31
    2016-11-09
    34 years,2 months,9 days

## 3\. ChronoUnit Example

Alternatively, you can use `ChronoUnit.{unit}.between` to find out the difference between dates, review the following example :

ChronoUnitExample.java

    package com.mkyong.time;

    import java.time.LocalDateTime;
    import java.time.Month;
    import java.time.temporal.ChronoUnit;

    public class ChronoUnitExample {

        public static void main(String[] args) {

            LocalDateTime oldDate = LocalDateTime.of(1982, Month.AUGUST, 31, 10, 20, 55);
            LocalDateTime newDate = LocalDateTime.of(2016, Month.NOVEMBER, 9, 10, 21, 56);

            System.out.println(oldDate);
            System.out.println(newDate);

            // count between dates
            long years = ChronoUnit.YEARS.between(oldDate, newDate);
            long months = ChronoUnit.MONTHS.between(oldDate, newDate);
            long weeks = ChronoUnit.WEEKS.between(oldDate, newDate);
            long days = ChronoUnit.DAYS.between(oldDate, newDate);
            long hours = ChronoUnit.HOURS.between(oldDate, newDate);
            long minutes = ChronoUnit.MINUTES.between(oldDate, newDate);
            long seconds = ChronoUnit.SECONDS.between(oldDate, newDate);
            long milis = ChronoUnit.MILLIS.between(oldDate, newDate);
            long nano = ChronoUnit.NANOS.between(oldDate, newDate);

            System.out.println("\n--- Total --- ");
            System.out.println(years + " years");
            System.out.println(months + " months");
            System.out.println(weeks + " weeks");
            System.out.println(days + " days");
            System.out.println(hours + " hours");
            System.out.println(minutes + " minutes");
            System.out.println(seconds + " seconds");
            System.out.println(milis + " milis");
            System.out.println(nano + " nano");

        }
    }

Output

    1982-08-31T10:20:55
    2016-11-09T10:21:56

    --- Total ---
    34 years
    410 months
    1784 weeks
    12489 days
    299736 hours
    17984161 minutes
    1079049661 seconds
    1079049661000 milis
    1079049661000000000 nano

## References

1.  [Oracle Tutorials – Period and Duration](https://docs.oracle.com/javase/tutorial/datetime/iso/period.html)
2.  [Duration JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/Duration.html)
3.  [Period JavaDoc](http://docs.oracle.com/javase/8/docs/api/java/time/Period.html)
4.  [ChronoUnit JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoUnit.html)

[http://www.mkyong.com/java8/java-8-period-and-duration-examples/](http://www.mkyong.com/java8/java-8-period-and-duration-examples/)
