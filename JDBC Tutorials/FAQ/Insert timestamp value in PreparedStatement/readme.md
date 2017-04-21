## Problem

A simple table script in Oracle database.

    CREATE TABLE DBUSER (
      USER_ID       NUMBER (5)    NOT NULL,
      USERNAME      VARCHAR2 (20)  NOT NULL,
      CREATED_BY    VARCHAR2 (20)  NOT NULL,
      CREATED_DATE  DATE          NOT NULL,
      PRIMARY KEY ( USER_ID )
     )

No idea how to insert a timestamp value, e.g. “_04/04/2011 14:45:04_” into “**CREATED_DATE**” field, via JDBC PreparedStatement.

    String insertTableSQL = "INSERT INTO DBUSER"
    		+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    		+ "(?,?,?,?)";
    preparedStatement = dbConnection.prepareStatement(insertTableSQL);
    preparedStatement.setTimestamp(4,???);

## Solution

Create a method to return current timestamp(`java.sql.Timestamp`) like this :

    private static java.sql.Timestamp getCurrentTimeStamp() {

    	java.util.Date today = new java.util.Date();
    	return new java.sql.Timestamp(today.getTime());

    }

And set the timestamp via `preparedStatement.setTimestamp()`.

    String insertTableSQL = "INSERT INTO DBUSER"
    	+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    	+ "(?,?,?,?)";
    preparedStatement = dbConnection.prepareStatement(insertTableSQL);
    preparedStatement.setTimestamp(4,getCurrentTimeStamp());

**Note**  
Refer to this full [JDBC PreparedStatement insert timestamp example](http://www.mkyong.com/jdbc/jdbc-preparestatement-example-create-a-table/).

[http://www.mkyong.com/jdbc/how-to-insert-timestamp-value-in-preparedstatement/](http://www.mkyong.com/jdbc/how-to-insert-timestamp-value-in-preparedstatement/)
