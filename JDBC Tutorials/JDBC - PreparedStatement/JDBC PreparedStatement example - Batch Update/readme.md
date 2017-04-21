Here’s an example to show you how to insert few records in batch process, via JDBC `PreparedStatement`.

    dbConnection.setAutoCommit(false);//commit trasaction manually

    String insertTableSQL = "INSERT INTO DBUSER"
    			+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    			+ "(?,?,?,?)";
    PreparedStatement = dbConnection.prepareStatement(insertTableSQL);

    preparedStatement.setInt(1, 101);
    preparedStatement.setString(2, "mkyong101");
    preparedStatement.setString(3, "system");
    preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    preparedStatement.addBatch();

    preparedStatement.setInt(1, 102);
    preparedStatement.setString(2, "mkyong102");
    preparedStatement.setString(3, "system");
    preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    preparedStatement.addBatch();
    preparedStatement.executeBatch();

    dbConnection.commit();

**Note**  
Batch Update is not limit to Insert statement, it’s apply for Update and Delete statement as well.

_See full JDBC batch update example …_

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.SQLException;

    public class JDBCBatchUpdateExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			batchInsertRecordsIntoTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void batchInsertRecordsIntoTable() throws SQLException {

    		Connection dbConnection = null;
    		PreparedStatement preparedStatement = null;

    		String insertTableSQL = "INSERT INTO DBUSER"
    				+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    				+ "(?,?,?,?)";

    		try {
    			dbConnection = getDBConnection();
    			preparedStatement = dbConnection.prepareStatement(insertTableSQL);

    			dbConnection.setAutoCommit(false);

    			preparedStatement.setInt(1, 101);
    			preparedStatement.setString(2, "mkyong101");
    			preparedStatement.setString(3, "system");
    			preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    			preparedStatement.addBatch();

    			preparedStatement.setInt(1, 102);
    			preparedStatement.setString(2, "mkyong102");
    			preparedStatement.setString(3, "system");
    			preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    			preparedStatement.addBatch();

    			preparedStatement.setInt(1, 103);
    			preparedStatement.setString(2, "mkyong103");
    			preparedStatement.setString(3, "system");
    			preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    			preparedStatement.addBatch();

    			preparedStatement.executeBatch();

    			dbConnection.commit();

    			System.out.println("Record is inserted into DBUSER table!");

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());
    			dbConnection.rollback();

    		} finally {

    			if (preparedStatement != null) {
    				preparedStatement.close();
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

    	private static java.sql.Timestamp getCurrentTimeStamp() {

    		java.util.Date today = new java.util.Date();
    		return new java.sql.Timestamp(today.getTime());

    	}

    }

## Result

3 records are inserted into database via batch update process.

## Why need to use Batch Update?

Alternatively, you can use normal `executeUpdate()` method like this :

    String insertTableSQL = "INSERT INTO DBUSER"
    				+ "(USER_ID, USERNAME, CREATED_BY, CREATED_DATE) VALUES"
    				+ "(?,?,?,?)";
    PreparpreparedStatement = dbConnection.prepareStatement(insertTableSQL);

    preparedStatement.setInt(1, 111);
    preparedStatement.setString(2, "mkyong101");
    preparedStatement.setString(3, "system");
    preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    preparedStatement.executeUpdate();

    preparedStatement.setInt(1, 112);
    preparedStatement.setString(2, "mkyong102");
    preparedStatement.setString(3, "system");
    preparedStatement.setTimestamp(4, getCurrentTimeStamp());
    preparedStatement.executeUpdate();

The above code snippet is works as well, but has performance issue if you are try to insert many records, let say 1000 records, because every `executeUpdate()` will hits database once. For batch update process, it hits database when `executeBatch()` is called.

[http://www.mkyong.com/jdbc/jdbc-preparedstatement-example-batch-update/](http://www.mkyong.com/jdbc/jdbc-preparedstatement-example-batch-update/)
