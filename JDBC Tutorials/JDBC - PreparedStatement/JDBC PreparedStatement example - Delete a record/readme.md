Here’s an example to show you how to delete a record from a table via JDBC PreparedStatement. To issue a delete statement, calls the `PreparedStatement.executeUpdate()` method like this :

    String deleteSQL = "DELETE DBUSER WHERE USER_ID = ?";
    PreparedStatement preparedStatement = dbConnection.prepareStatement(deleteSQL);
    preparedStatement.setInt(1, 1001);
    // execute delete SQL stetement
    preparedStatement.executeUpdate();

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.SQLException;

    public class JDBCPreparedStatementSelectExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			deleteRecordFromTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void deleteRecordFromTable() throws SQLException {

    		Connection dbConnection = null;
    		PreparedStatement preparedStatement = null;

    		String deleteSQL = "DELETE DBUSER WHERE USER_ID = ?";

    		try {
    			dbConnection = getDBConnection();
    			preparedStatement = dbConnection.prepareStatement(deleteSQL);
    			preparedStatement.setInt(1, 1001);

    			// execute delete SQL stetement
    			preparedStatement.executeUpdate();

    			System.out.println("Record is deleted!");

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

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

    }

## Result

A record with “user_id=1001″ is deleted from table.

[http://www.mkyong.com/jdbc/jdbc-preparestatement-example-delete-a-record/](http://www.mkyong.com/jdbc/jdbc-preparestatement-example-delete-a-record/)
