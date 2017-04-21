Here’s an example to show you how to insert few records in batch process, via JDBC `Statement`.

    dbConnection.setAutoCommit(false);

    statement = dbConnection.createStatement();
    statement.addBatch(insertTableSQL1);
    statement.addBatch(insertTableSQL2);
    statement.addBatch(insertTableSQL3);

    statement.executeBatch();

    dbConnection.commit();

**Note**  
Batch Update is not limit to Insert statement, it’s apply for Update and Delete statement as well.

_See full JDBC batch update example …_

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;
    import java.sql.Statement;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;

    public class JDBCBatchUpdateExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";
    	private static final DateFormat dateFormat = new SimpleDateFormat(
    			"yyyy/MM/dd HH:mm:ss");

    	public static void main(String[] argv) {

    		try {

    			batchInsertRecordsIntoTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void batchInsertRecordsIntoTable() throws SQLException {

    		Connection dbConnection = null;
    		Statement statement = null;

    		String insertTableSQL1 = "INSERT INTO DBUSER"
    				+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) " + "VALUES"
    				+ "(101,'mkyong','system', " + "to_date('"
    				+ getCurrentTimeStamp() + "', 'yyyy/mm/dd hh24:mi:ss'))";

    		String insertTableSQL2 = "INSERT INTO DBUSER"
    				+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) " + "VALUES"
    				+ "(102,'mkyong','system', " + "to_date('"
    				+ getCurrentTimeStamp() + "', 'yyyy/mm/dd hh24:mi:ss'))";

    		String insertTableSQL3 = "INSERT INTO DBUSER"
    				+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) " + "VALUES"
    				+ "(103,'mkyong','system', " + "to_date('"
    				+ getCurrentTimeStamp() + "', 'yyyy/mm/dd hh24:mi:ss'))";

    		try {
    			dbConnection = getDBConnection();
    			statement = dbConnection.createStatement();

    			dbConnection.setAutoCommit(false);

    			statement.addBatch(insertTableSQL1);
    			statement.addBatch(insertTableSQL2);
    			statement.addBatch(insertTableSQL3);

    			statement.executeBatch();

    			dbConnection.commit();

    			System.out.println("Records are inserted into DBUSER table!");

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

3 records are inserted into database via batch update process.

## Why need to use Batch Update?

The above batch update is same with normal `executeUpdate()` method like this :

    statement.executeUpdate(insertTableSQL1);
    statement.executeUpdate(insertTableSQL2);
    statement.executeUpdate(insertTableSQL3);

But batch update has performance benefit if you want to insert many records, because `executeBatch()` reduces the number of JDBC calls to database.

[http://www.mkyong.com/jdbc/jdbc-statement-example-batch-update/](http://www.mkyong.com/jdbc/jdbc-statement-example-batch-update/)
