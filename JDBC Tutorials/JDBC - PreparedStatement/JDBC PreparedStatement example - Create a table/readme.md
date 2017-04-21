Here’s an example to show you how to create a table in database via JDBC PrepareStatement. To issue a create statement, calls the `PrepareStatement.executeUpdate()` method like this :

    PreparedStatement preparedStatement = dbConnection.prepareStatement(createTableSQL);
    // execute create SQL stetement
    preparedStatement.executeUpdate();

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.SQLException;

    public class JDBCPreparedStatementCreateExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			createTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void createTable() throws SQLException {

    		Connection dbConnection = null;
    		PreparedStatement preparedStatement = null;

    		String createTableSQL = "CREATE TABLE DBUSER1("
    				+ "USER_ID NUMBER(5) NOT NULL, "
    				+ "USERNAME VARCHAR(20) NOT NULL, "
    				+ "CREATED_BY VARCHAR(20) NOT NULL, "
    				+ "CREATED_DATE DATE NOT NULL, " + "PRIMARY KEY (USER_ID) "
    				+ ")";

    		try {
    			dbConnection = getDBConnection();
    			preparedStatement = dbConnection.prepareStatement(createTableSQL);

    			System.out.println(createTableSQL);

    			// execute create SQL stetement
    			preparedStatement.executeUpdate();

    			System.out.println("Table \"dbuser\" is created!");

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

A table named “DBUSER” is created.

    CREATE TABLE DBUSER(
       USER_ID NUMBER(5) NOT NULL,
       USERNAME VARCHAR(20) NOT NULL,
       CREATED_BY VARCHAR(20) NOT NULL,
       CREATED_DATE DATE NOT NULL,
       PRIMARY KEY (USER_ID)
    )
    Table "dbuser" is created!

http://www.mkyong.com/jdbc/jdbc-preparestatement-example-create-a-table/
