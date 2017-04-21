Here’s an example to show you how to update a record in a table via JDBC statement. To issue a update statement, calls the `Statement.executeUpdate()` method like this :

    Statement statement = dbConnection.createStatement();
    // execute the update SQL stetement
    statement.executeUpdate(updateTableSQL);

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;
    import java.sql.Statement;

    public class JDBCStatementUpdateExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			updateRecordIntoDbUserTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void updateRecordIntoDbUserTable() throws SQLException {

    		Connection dbConnection = null;
    		Statement statement = null;

    		String updateTableSQL = "UPDATE DBUSER"
    				+ " SET USERNAME = 'mkyong_new' "
    				+ " WHERE USER_ID = 1";

    		try {
    			dbConnection = getDBConnection();
    			statement = dbConnection.createStatement();

    			System.out.println(updateTableSQL);

    			// execute update SQL stetement
    			statement.execute(updateTableSQL);

    			System.out.println("Record is updated to DBUSER table!");

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

    }

## Result

The username of “user_id = 1” is updated to a new value ‘mkyong_new’.

    UPDATE DBUSER SET USERNAME = 'mkyong_new'  WHERE USER_ID = 1
    Record is updated into DBUSER table!

[http://www.mkyong.com/jdbc/jdbc-statement-example-update-a-record/](http://www.mkyong.com/jdbc/jdbc-statement-example-update-a-record/)
