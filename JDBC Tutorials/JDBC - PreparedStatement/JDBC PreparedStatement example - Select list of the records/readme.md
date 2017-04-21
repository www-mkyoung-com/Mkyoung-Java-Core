Here’s an example to show you how to select records from table via JDBC PreparedStatement, and display the records via a ResultSet object. To issue a select query, calls the `PreparedStatement.executeQuery()` method like this :

    String selectSQL = "SELECT USER_ID, USERNAME FROM DBUSER WHERE USER_ID = ?";
    PreparedStatement preparedStatement = dbConnection.prepareStatement(selectSQL);
    preparedStatement.setInt(1, 1001);
    ResultSet rs = preparedStatement.executeQuery(selectSQL );
    while (rs.next()) {
    	String userid = rs.getString("USER_ID");
    	String username = rs.getString("USERNAME");
    }

Full example…

    package com.mkyong.jdbc;

    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    import java.sql.SQLException;

    public class JDBCPreparedStatementSelectExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			selectRecordsFromTable();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void selectRecordsFromTable() throws SQLException {

    		Connection dbConnection = null;
    		PreparedStatement preparedStatement = null;

    		String selectSQL = "SELECT USER_ID, USERNAME FROM DBUSER WHERE USER_ID = ?";

    		try {
    			dbConnection = getDBConnection();
    			preparedStatement = dbConnection.prepareStatement(selectSQL);
    			preparedStatement.setInt(1, 1001);

    			// execute select SQL stetement
    			ResultSet rs = preparedStatement.executeQuery();

    			while (rs.next()) {

    				String userid = rs.getString("USER_ID");
    				String username = rs.getString("USERNAME");

    				System.out.println("userid : " + userid);
    				System.out.println("username : " + username);

    			}

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

List of the records with “user_id = 1001” are retrieved from table “DBUSER” and displayed.

[http://www.mkyong.com/jdbc/jdbc-preparestatement-example-select-list-of-the-records/](http://www.mkyong.com/jdbc/jdbc-preparestatement-example-select-list-of-the-records/)
