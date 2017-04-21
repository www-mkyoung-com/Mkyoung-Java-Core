For stored procedure returns OUT parameters, it must be

1.  Registered via JDBC `CallableStatement.registerOutParameter(index,sqlType)`.
2.  Get it back via `CallableStatement.getDataType(index)`.

See code snippets

    //getDBUSERByUserId is a stored procedure
    String getDBUSERByUserIdSql = "{call getDBUSERByUserId(?,?,?,?)}";
    callableStatement = dbConnection.prepareCall(getDBUSERByUserIdSql);
    callableStatement.setInt(1, 10);
    callableStatement.registerOutParameter(2, java.sql.Types.VARCHAR);
    callableStatement.registerOutParameter(3, java.sql.Types.VARCHAR);
    callableStatement.registerOutParameter(4, java.sql.Types.DATE);

    // execute getDBUSERByUserId store procedure
    callableStatement.executeUpdate();

    String userName = callableStatement.getString(2);
    String createdBy = callableStatement.getString(3);
    Date createdDate = callableStatement.getDate(4);

## JDBC CallableStatement Example

See a full JDBC `CallableStatement` example for OUT parameter.

## 1\. Stored Procedure

A stored procedure in Oracle database, with IN and OUT parameters. Later, calls it via JDBC.

    CREATE OR REPLACE PROCEDURE getDBUSERByUserId(
    	   p_userid IN DBUSER.USER_ID%TYPE,
    	   o_username OUT DBUSER.USERNAME%TYPE,
    	   o_createdby OUT  DBUSER.CREATED_BY%TYPE,
    	   o_date OUT DBUSER.CREATED_DATE%TYPE)
    IS
    BEGIN

      SELECT USERNAME , CREATED_BY, CREATED_DATE
      INTO o_username, o_createdby,  o_date
      from  DBUSER WHERE USER_ID = p_userid;

    END;
    /

## 2\. Calls Stored Procedure via CallableStatement

JDBC example to call a stored procedure via `CallableStatement`.

_File : JDBCCallableStatementOUTParameterExample.java_

    package com.mkyong.jdbc;

    import java.sql.CallableStatement;
    import java.sql.Date;
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.SQLException;

    public class JDBCCallableStatementOUTParameterExample {

    	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
    	private static final String DB_CONNECTION = "jdbc:oracle:thin:@localhost:1521:MKYONG";
    	private static final String DB_USER = "user";
    	private static final String DB_PASSWORD = "password";

    	public static void main(String[] argv) {

    		try {

    			callOracleStoredProcOUTParameter();

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		}

    	}

    	private static void callOracleStoredProcOUTParameter() throws SQLException {

    		Connection dbConnection = null;
    		CallableStatement callableStatement = null;

    		String getDBUSERByUserIdSql = "{call getDBUSERByUserId(?,?,?,?)}";

    		try {
    			dbConnection = getDBConnection();
    			callableStatement = dbConnection.prepareCall(getDBUSERByUserIdSql);

    			callableStatement.setInt(1, 10);
    			callableStatement.registerOutParameter(2, java.sql.Types.VARCHAR);
    			callableStatement.registerOutParameter(3, java.sql.Types.VARCHAR);
    			callableStatement.registerOutParameter(4, java.sql.Types.DATE);

    			// execute getDBUSERByUserId store procedure
    			callableStatement.executeUpdate();

    			String userName = callableStatement.getString(2);
    			String createdBy = callableStatement.getString(3);
    			Date createdDate = callableStatement.getDate(4);

    			System.out.println("UserName : " + userName);
    			System.out.println("CreatedBy : " + createdBy);
    			System.out.println("CreatedDate : " + createdDate);

    		} catch (SQLException e) {

    			System.out.println(e.getMessage());

    		} finally {

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

1.  [http://download.oracle.com/javase/6/docs/api/java/sql/CallableStatement.html](http://download.oracle.com/javase/6/docs/api/java/sql/CallableStatement.html)
2.  [http://docsrv.sco.com/JDK_guide/jdbc/getstart/callablestatement.doc.html](http://docsrv.sco.com/JDK_guide/jdbc/getstart/callablestatement.doc.html)
3.  [http://onjava.com/pub/a/onjava/2003/08/13/stored_procedures.html](http://onjava.com/pub/a/onjava/2003/08/13/stored_procedures.html)

[http://www.mkyong.com/jdbc/jdbc-callablestatement-stored-procedure-out-parameter-example/](http://www.mkyong.com/jdbc/jdbc-callablestatement-stored-procedure-out-parameter-example/)
