Here’s an example to show you how to create a table in database via JDBC statement. To issue a create statement, calls the S`tatement.execute()` method like this :

    Statement statement = dbConnection.createStatement();
    // execute create SQL stetement
    statement.execute(createTableSQL);

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;
    import java.sql.Statement;

    public class JDBCStatementCreateExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			createDbUserTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void createDbUserTable() throws SQLException {

    		Connection dbConnection = null;
    		Statement statement = null;

    		String createTableSQL = "CREATE TABLE DBUSER("
    				+ "USER_ID NUMBER(5) NOT NULL, "
    				+ "USERNAME VARCHAR(20) NOT NULL, "
    				+ "CREATED_BY VARCHAR(20) NOT NULL, "
    				+ "CREATED_DATE DATE NOT NULL, " + "PRIMARY KEY (USER_ID) "
    				+ ")";

    		try {
    			dbConnection = getDBConnection();
    			statement = dbConnection.createStatement();

    			System.out.println(createTableSQL);
                            // execute the SQL stetement
    			statement.execute(createTableSQL);

    			System.out.println("Table \"dbuser\" is created!");

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

Here’s the result.

    CREATE TABLE DBUSER(
      USER_ID NUMBER(5) NOT NULL,
      USERNAME VARCHAR(20) NOT NULL,
      CREATED_BY VARCHAR(20) NOT NULL,
      CREATED_DATE DATE NOT NULL,
      PRIMARY KEY (USER_ID)
    )
    Table "user" is created!

[http://www.mkyong.com/jdbc/jdbc-statement-example-create-a-table/](http://www.mkyong.com/jdbc/jdbc-statement-example-create-a-table/)
