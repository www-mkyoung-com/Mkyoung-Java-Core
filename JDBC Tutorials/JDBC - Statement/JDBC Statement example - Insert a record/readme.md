Here’s an example to show you how to insert a record into table via JDBC statement. To issue a insert statement, calls the `Statement.executeUpdate()` method like this :

    Statement statement = dbConnection.createStatement();
    // execute the insert SQL stetement
    statement.executeUpdate(insertTableSQL);

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;
    import java.sql.Statement;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;

    public class JDBCStatementInsertExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";
    	private static final DateFormat dateFormat = new SimpleDateFormat(
    			"yyyy/MM/dd HH:mm:ss");

    	public static void main(String[] argv) {

    		try {

    			insertRecordIntoDbUserTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void insertRecordIntoDbUserTable() throws SQLException {

    		Connection dbConnection = null;
    		Statement statement = null;

    		String insertTableSQL = "INSERT INTO DBUSER"
    				+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) " + "VALUES"
    				+ "(1,'mkyong','system', " + "to_date('"
    				+ getCurrentTimeStamp() + "', 'yyyy/mm/dd hh24:mi:ss'))";

    		try {
    			dbConnection = getDBConnection();
    			statement = dbConnection.createStatement();

    			System.out.println(insertTableSQL);

    			// execute insert SQL stetement
    			statement.executeUpdate(insertTableSQL);

    			System.out.println("Record is inserted into DBUSER table!");

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		} finally {

    			if (statement != null) {
    				statement.close();
    			}

    			if (dbConnection != null) {
    				dbConnection.close();
    			}

    		}

    	}

    	private static Connection getDBConnection() {

    		Connection dbConnection = null;

    		try {

    			Class.forName(DB_DRIVER);

    		} catch (ClassNotFoundException e) {

    			System.out.println(e.getMessage());

    		}

    		try {

    			dbConnection = DriverManager.getConnection(
                                   DB_CONNECTION, DB_USER,DB_PASSWORD);
    			return dbConnection;

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    		return dbConnection;

    	}

    	private static String getCurrentTimeStamp() {

    		java.util.Date today = new java.util.Date();
    		return dateFormat.format(today.getTime());

    	}

    }

## Result

A record is inserted into a table named “DBUSER”.

    INSERT INTO DBUSER(USER_ID, USERNAME, CREATED_BY, CREATED_DATE)
    VALUES(1,'mkyong','system', to_date('2011/04/04 13:59:03', 'yyyy/mm/dd hh24:mi:ss'))
    Record is inserted into DBUSER table!

[http://www.mkyong.com/jdbc/jdbc-statement-example-insert-a-record/](http://www.mkyong.com/jdbc/jdbc-statement-example-insert-a-record/)
