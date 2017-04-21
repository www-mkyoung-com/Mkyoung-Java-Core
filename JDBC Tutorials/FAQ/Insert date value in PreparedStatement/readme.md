## Problem

A simple table script in Oracle database.

    CREATE TABLE DBUSER (
      USER_ID       NUMBER (5)    NOT NULL,
      USERNAME      VARCHAR2 (20)  NOT NULL,
      CREATED_BY    VARCHAR2 (20)  NOT NULL,
      CREATED_DATE  DATE          NOT NULL,
      PRIMARY KEY ( USER_ID )
     )

No idea how to insert current date value, e.g. “_04/04/2011_” into “**CREATED_DATE**” field, via JDBC PreparedStatement.

    String insertTableSQL = "INSERT INTO DBUSER"
    		+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    		+ "(?,?,?,?)";
    preparedStatement = dbConnection.prepareStatement(insertTableSQL);
    preparedStatement.setDate(4, ???);

## Solution

The “`preparedStatement.setDate()`” method is accept a `java.sql.Date` parameter, so, you have to convert from `java.util.Date` to `java.sql.Date`.

For example, create a method to return current date, and convert it `java.sql.Date` :

    private static java.sql.Date getCurrentDate() {
        java.util.Date today = new java.util.Date();
        return new java.sql.Date(today.getTime());
    }

And set the returned date via `preparedStatement.setDate()`.

    String insertTableSQL = "INSERT INTO DBUSER"
    	+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    	+ "(?,?,?,?)";
    preparedStatement = dbConnection.prepareStatement(insertTableSQL);
    preparedStatement.setDate(4, getCurrentDate());

Done.

[http://www.mkyong.com/jdbc/how-to-insert-date-value-in-preparedstatement/](http://www.mkyong.com/jdbc/how-to-insert-date-value-in-preparedstatement/)
