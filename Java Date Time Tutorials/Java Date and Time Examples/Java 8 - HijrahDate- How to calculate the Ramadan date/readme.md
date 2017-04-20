[Ramadan](https://en.wikipedia.org/wiki/Ramadan_(calendar_month)) is the 9th month of the Islamic calendar, the entire month.

## 1\. HijrahDate -> Ramadan 2016

Full example to calculate the start and end of the Ramadan 2016

TestHijrahDate.java

    package com.mkyong.date;

    import java.time.LocalDate;
    import java.time.chrono.HijrahDate;
    import java.time.temporal.ChronoField;
    import java.time.temporal.TemporalAdjusters;

    public class TestDate {

        public static void main(String[] args) {

            //first day of Ramadan, 9th month
            HijrahDate ramadan = HijrahDate.now()
                    .with(ChronoField.DAY_OF_MONTH, 1).with(ChronoField.MONTH_OF_YEAR, 9);
            System.out.println("HijrahDate : " + ramadan);

            //HijrahDate -> LocalDate
            System.out.println("\n--- Ramandan 2016 ---");
            System.out.println("Start : " + LocalDate.from(ramadan));

            //until the end of the month
            System.out.println("End : " + LocalDate.from(ramadan.with(TemporalAdjusters.lastDayOfMonth())));

        }

    }

Output

    HijrahDate : Hijrah-umalqura AH 1437-09-01

    --- Ramandan 2016 ---
    Start : 2016-06-06
    End : 2016-07-05

## References

1.  [Wikipedia – Ramadan (calendar month)](https://en.wikipedia.org/wiki/Ramadan_(calendar_month))
2.  [HijrahDate JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/chrono/HijrahDate.html)

[http://www.mkyong.com/java8/java-8-hijrahdate-how-to-calculate-the-ramadan-date/](http://www.mkyong.com/java8/java-8-hijrahdate-how-to-calculate-the-ramadan-date/)
