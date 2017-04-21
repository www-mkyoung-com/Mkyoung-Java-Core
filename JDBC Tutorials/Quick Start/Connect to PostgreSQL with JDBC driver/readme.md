Here is an example to show you how to connect to PostgreSQL database with JDBC driver.

## 1\. Download PostgreSQL JDBC Driver

Get a PostgreSQL JDBC driver at this URL : [http://jdbc.postgresql.org/download.html](http://jdbc.postgresql.org/download.html)

## 2\. Java JDBC connection example

Code snippets to use JDBC to connect a PostgreSQL database

    Class.forName("org.postgresql.Driver");
    Connection connection = null;
    connection = DriverManager.getConnection(
       "jdbc:postgresql://hostname:port/dbname","username", "password");
    connection.close();

See a complete example below :  
_File : JDBCExample.java_

<pre>import java.sql.DriverManager;
import java.sql.Connection;
import java.sql.SQLException;

public class JDBCExample {

	public static void main(String[] argv) {

		System.out.println("-------- PostgreSQL "
				+ "JDBC Connection Testing ------------");

		try {

			Class.forName("org.postgresql.Driver");

		} catch (ClassNotFoundException e) {

			System.out.println("Where is your PostgreSQL JDBC Driver? "
					+ "Include in your library path!");
			e.printStackTrace();
			return;

		}

		System.out.println("PostgreSQL JDBC Driver Registered!");

		Connection connection = null;

		try {

			connection = DriverManager.getConnection(
					"jdbc:postgresql://127.0.0.1:5432/testdb", "mkyong",
					"123456");

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
</pre>

## 3\. Run it

Assume JDBCExample is store in **c:\test** folder, together with PostgreSQL JDBC driver, then run it :

    C:\test>java -cp c:\test\postgresql-8.3-603.jdbc4.jar;c:\test JDBCExample
    -------- MySQL JDBC Connection Testing ------------
    PostgreSQL JDBC Driver Registered!
    You made it, take control your database now!

Done

[http://www.mkyong.com/jdbc/how-do-connect-to-postgresql-with-jdbc-driver-java/](http://www.mkyong.com/jdbc/how-do-connect-to-postgresql-with-jdbc-driver-java/)
