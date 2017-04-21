Here’s an example to show you how to connect to Oracle database via a JDBC driver.

## 1\. Download Oracle JDBC Driver

Visit [Oracle website](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html) to get the Oracle JDBC driver `ojdbc6.jar` or `ojdbc7.jar`

![oracle jdbc driver](http://www.mkyong.com/wp-content/uploads/2011/01/download-oracle-jdbc-driver.png)

_P.S You need to create an Oracle account (free) to download the JDBC driver._

## 2\. Java JDBC connection example

Code snippets to connect an Oracle database via a JDBC driver.

    Class.forName("oracle.jdbc.driver.OracleDriver");
    Connection connection = null;
    connection = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:SID","username","password");
    connection.close();

See a complete example below :

OracleJDBCExample.java

    package com.mkyong;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;

    public class OracleJDBCExample {

        public static void main(String[] argv) {

            System.out.println("-------- Oracle JDBC Connection Testing ------");

            try {

                Class.forName("oracle.jdbc.driver.OracleDriver");

            } catch (ClassNotFoundException e) {

                System.out.println("Where is your Oracle JDBC Driver?");
                e.printStackTrace();
                return;

            }

            System.out.println("Oracle JDBC Driver Registered!");

            Connection connection = null;

            try {

                connection = DriverManager.getConnection(
                        "jdbc:oracle:thin:@localhost:1521:xe", "system", "password");

            } catch (SQLException e) {

                System.out.println("Connection Failed! Check output console");
                e.printStackTrace();
                return;

            }

            if (connection != null) {
                System.out.println("You made it, take control your database now!");
            } else {
                System.out.println("Failed to make connection!");
            }
        }

    }

## 3\. Run it

Assume `OracleJDBCExample.java` is stored in `C:\jdbc-test` folder, together with the Oracle JDBC driver `ojdbc7.jar`

Terminal

    C:\jdbc-test>javac OracleJDBCExample.java

    C:\jdbc-test>java -cp c:\jdbc-test\ojdbc7.jar;c:\jdbc-test OracleJDBCExample
    -------- Oracle JDBC Connection Testing ------------
    Oracle JDBC Driver Registered!
    You made it, take control your database now!

Done.

## References

1.  [How to add Oracle JDBC driver in your Maven local repository](https://www.mkyong.com/maven/how-to-add-oracle-jdbc-driver-in-your-maven-local-repository/)
2.  [OracleDriver Doc](http://docs.oracle.com/cd/E11882_01/appdev.112/e13995/oracle/jdbc/OracleDriver.html)

[http://www.mkyong.com/jdbc/connect-to-oracle-db-via-jdbc-driver-java/](http://www.mkyong.com/jdbc/connect-to-oracle-db-via-jdbc-driver-java/)
