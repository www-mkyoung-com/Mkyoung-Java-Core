Here’s an example to show you how to connect to MySQL database via a JDBC driver. First, get a MySQL JDBC driver from here –[MySQL JDBC Driver Download Here](http://dev.mysql.com/downloads/connector/j/).

## 1\. Java JDBC connection example

Code snippets to use a JDBC driver to connect a MySQL database.

    Class.forName("com.mysql.jdbc.Driver");
    Connection conn = null;
    conn = DriverManager.getConnection("jdbc:mysql://hostname:port/dbname","username", "password");
    conn.close();

See a complete example below :

JDBCExample.java

    package com.mkyong.common;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;

    public class JDBCExample {

      public static void main(String[] argv) {

    	System.out.println("-------- MySQL JDBC Connection Testing ------------");

    	try {
    		Class.forName("com.mysql.jdbc.Driver");
    	} catch (ClassNotFoundException e) {
    		System.out.println("Where is your MySQL JDBC Driver?");
    		e.printStackTrace();
    		return;
    	}

    	System.out.println("MySQL JDBC Driver Registered!");
    	Connection connection = null;

    	try {
    		connection = DriverManager
    		.getConnection("jdbc:mysql://localhost:3306/mkyongcom","root", "password");

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

## 2\. Run it

Assume `JDBCExample.java` is store in `c:\test` folder, along with the `MySQL JDBC driver`

    C:\test>java -cp c:\test\mysql-connector-java-5.1.8-bin.jar;c:\test JDBCExample
    -------- MySQL JDBC Connection Testing ------------
    MySQL JDBC Driver Registered!
    You made it, take control your database now!

    C:\test>

_P.S To run this example, your need `mysql-connector-java-{version}-bin.jar` in your classpath._

Done.

[http://www.mkyong.com/jdbc/how-to-connect-to-mysql-with-jdbc-driver-java/](http://www.mkyong.com/jdbc/how-to-connect-to-mysql-with-jdbc-driver-java/)
