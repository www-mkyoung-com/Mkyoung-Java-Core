Here’s an example to show you how to delete a record from a table via JDBC statement. To issue a delete statement, calls the `Statement.executeUpdate()` method like this :

    Statement statement = dbConnection.createStatement();
    // execute the delete SQL stetement
    statement.executeUpdate(deleteTableSQL);

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;
    import java.sql.Statement;

    public class JDBCStatementDeleteExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			deleteRecordFromDbUserTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void deleteRecordFromDbUserTable() throws SQLException {

    		Connection dbConnection = null;
    		Statement statement = null;

    		String deleteTableSQL = "DELETE DBUSER WHERE USER_ID = 1";

    		try {
    			dbConnection = getDBConnection();
    			statement = dbConnection.createStatement();

    			System.out.println(deleteTableSQL);

    			// execute delete SQL stetement
    			statement.execute(deleteTableSQL);

    			System.out.println("Record is deleted from DBUSER table!");

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

A record with “user_id=1” is deleted from table.

    DELETE DBUSER WHERE USER_ID = 1
    Record is deleted from DBUSER table!

[http://www.mkyong.com/jdbc/jdbc-statement-example-delete-a-record/](http://www.mkyong.com/jdbc/jdbc-statement-example-delete-a-record/)
