This [MinguoDate](https://docs.oracle.com/javase/8/docs/api/java/time/chrono/MinguoDate.html) calendar system is primarily used in Taiwan (Republic of China…)

<pre>(ISO) 1912-01-01 = 1-01-01 (Minguo ROC)
</pre>

To convert the current date to the Minguo date, just subtracts the current year with number 1911, for example

<pre>2016 (ISO) - 1911 = 105 (Minguo ROC)
</pre>

## 1\. LocalDate -> MinguoDate

Review a full example to convert a `LocalDate` to `MinguoDate`

TestMinguoDate.java

    package com.mkyong.date;

    import java.time.LocalDate;
    import java.time.chrono.MinguoDate;

    public class TestMinguoDate {

        public static void main(String[] args) {

            // LocalDate -> MinguoDate
            System.out.println("Example 1...");

            LocalDate localDate = LocalDate.of(1912, 1, 1);
            MinguoDate minguo = MinguoDate.from(localDate);
            System.out.println("LocalDate : " + localDate); //1912-01-01
            System.out.println("MinguoDate : " + minguo);   //1-01-01

            // MinguoDate -> LocalDate
            System.out.println("\nExample 2...");

            MinguoDate minguo2 = MinguoDate.of(105, 8, 24);
            //LocalDate localDate = LocalDate.ofEpochDay(minguo2.toEpochDay());
            LocalDate localDate2 = LocalDate.from(minguo2);
            System.out.println("MinguoDate : " + minguo2);   //105-08-24
            System.out.println("LocalDate : " + localDate2); //2016-08-24

        }

    }

Output

    Example 1...
    LocalDate : 1912-01-01
    MinguoDate : Minguo ROC 1-01-01

    Example 2...
    MinguoDate : Minguo ROC 105-08-24
    LocalDate : 2016-08-24

## References

1.  [MinguoDate JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/time/chrono/MinguoDate.html)
2.  [Minguo calendar](http://calendars.wikia.com/wiki/Minguo_calendar)

[http://www.mkyong.com/java8/java-8-minguodate-examples/](http://www.mkyong.com/java8/java-8-minguodate-examples/)
