For Oracle stored procedure returns CURSOR parameter, you can

1.  Registered via JDBC `CallableStatement.registerOutParameter(index,OracleTypes.CURSOR)`.
2.  Get it back via `callableStatement.getObject(index)`.

See code snippets

    //getDBUSERCursor is a stored procedure
    String getDBUSERCursorSql = "{call getDBUSERCursor(?,?)}";
    callableStatement = dbConnection.prepareCall(getDBUSERCursorSql);
    callableStatement.setString(1, "mkyong");
    callableStatement.registerOutParameter(2, OracleTypes.CURSOR);

    // execute getDBUSERCursor store procedure
    callableStatement.executeUpdate();

    // get cursor and cast it to ResultSet
    rs = (ResultSet) callableStatement.getObject(2);

    // loop it like normal
    while (rs.next()) {
    	String userid = rs.getString("USER_ID");
    	String userName = rs.getString("USERNAME");
    }

## JDBC CallableStatement CURSOR Example

See a full JDBC `CallableStatement` example for OUT **CURSOR** parameter.

## 1\. Stored Procedure

A Oracle stored procedure, with one IN and one OUT CURSOR parameter. Later, calls it via JDBC.

    CREATE OR REPLACE PROCEDURE getDBUSERCursor(
    	   p_username IN DBUSER.USERNAME%TYPE,
    	   c_dbuser OUT SYS_REFCURSOR)
    IS
    BEGIN

      OPEN c_dbuser FOR
      SELECT * FROM DBUSER WHERE USERNAME LIKE p_username || '%';

    END;
    /

## 2\. Calls Stored Procedure via CallableStatement

JDBC example to call above stored procedure, cast the returned **CURSOR** to **ResultSet** and loop through the records sequentially.

_File : JDBCCallableStatementCURSORExample.java_

    package com.mkyong.jdbc;

    import java.sql.CallableStatement;
    import java.sql.Date;
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.ResultSet;
    import java.sql.SQLException;

    import oracle.jdbc.OracleTypes;

    public class JDBCCallableStatementCURSORExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			callOracleStoredProcCURSORParameter();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void callOracleStoredProcCURSORParameter()
    			throws SQLException {

    		Connection dbConnection = null;
    		CallableStatement callableStatement = null;
    		ResultSet rs = null;

    		String getDBUSERCursorSql = "{call getDBUSERCursor(?,?)}";

    		try {
    			dbConnection = getDBConnection();
    			callableStatement = dbConnection.prepareCall(getDBUSERCursorSql);

    			callableStatement.setString(1, "mkyong");
    			callableStatement.registerOutParameter(2, OracleTypes.CURSOR);

    			// execute getDBUSERCursor store procedure
    			callableStatement.executeUpdate();

    			// get cursor and cast it to ResultSet
    			rs = (ResultSet) callableStatement.getObject(2);

    			while (rs.next()) {
    				String userid = rs.getString("USER_ID");
    				String userName = rs.getString("USERNAME");
    				String createdBy = rs.getString("CREATED_BY");
    				String createdDate = rs.getString("CREATED_DATE");

    				System.out.println("UserName : " + userid);
    				System.out.println("UserName : " + userName);
    				System.out.println("CreatedBy : " + createdBy);
    				System.out.println("CreatedDate : " + createdDate);
    			}

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		} finally {

    			if (rs != null) {
    				rs.close();
    			}

    			if (callableStatement != null) {
    				callableStatement.close();
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

Done.

## Reference

1.  [http://www.oradev.com/ref_cursor.jsp](http://www.oradev.com/ref_cursor.jsp)
2.  [http://download.oracle.com/javase/6/docs/api/java/sql/CallableStatement.html](http://download.oracle.com/javase/6/docs/api/java/sql/CallableStatement.html)
3.  [http://docsrv.sco.com/JDK_guide/jdbc/getstart/callablestatement.doc.html](http://docsrv.sco.com/JDK_guide/jdbc/getstart/callablestatement.doc.html)
4.  [http://onjava.com/pub/a/onjava/2003/08/13/stored_procedures.html](http://onjava.com/pub/a/onjava/2003/08/13/stored_procedures.html)

[http://www.mkyong.com/jdbc/jdbc-callablestatement-stored-procedure-cursor-example/](http://www.mkyong.com/jdbc/jdbc-callablestatement-stored-procedure-cursor-example/)
