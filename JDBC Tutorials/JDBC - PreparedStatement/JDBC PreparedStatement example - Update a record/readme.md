Here’s an example to show you how to update a record in table via JDBC PreparedStatement. To issue a update statement, calls the `PreparedStatement.executeUpdate()` method like this :

    String updateTableSQL = "UPDATE DBUSER SET USERNAME = ? WHERE USER_ID = ?";
    PreparedStatement preparedStatement = dbConnection.prepareStatement(updateTableSQL);
    preparedStatement.setString(1, "mkyong_new_value");
    preparedStatement.setInt(2, 1001);
    // execute insert SQL stetement
    preparedStatement .executeUpdate();

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.SQLException;

    public class JDBCPreparedStatementUpdateExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			updateRecordToTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void updateRecordToTable() throws SQLException {

    		Connection dbConnection = null;
    		PreparedStatement preparedStatement = null;

    		String updateTableSQL = "UPDATE DBUSER SET USERNAME = ? "
    				                  + " WHERE USER_ID = ?";

    		try {
    			dbConnection = getDBConnection();
    			preparedStatement = dbConnection.prepareStatement(updateTableSQL);

    			preparedStatement.setString(1, "mkyong_new_value");
    			preparedStatement.setInt(2, 1001);

    			// execute update SQL stetement
    			preparedStatement.executeUpdate();

    			System.out.println("Record is updated to DBUSER table!");

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

The username of “user_id = 1001” is updated to a new value ‘mkyong_new_value’.

[http://www.mkyong.com/jdbc/jdbc-preparestatement-example-update-a-record/](http://www.mkyong.com/jdbc/jdbc-preparestatement-example-update-a-record/)
