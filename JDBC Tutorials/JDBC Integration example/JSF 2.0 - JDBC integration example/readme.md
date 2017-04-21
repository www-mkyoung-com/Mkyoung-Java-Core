Here’s a guide to show you how to integrate JSF 2.0 with database via JDBC. In this example, we are using MySQL database and Tomcat web container.

_Directory structure of this example_

![](http://www.mkyong.com/wp-content/uploads/2010/12/jsf2-jdbc-integration-example-folder.png)

## 1\. Table Structure

Create a “_customer_” table and insert five dummy records. Later, display it via JSF `h:dataTable`.

_SQL commands_

    DROP TABLE IF EXISTS `mkyongdb`.`customer`;
    CREATE TABLE  `mkyongdb`.`customer` (
      `CUSTOMER_ID` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT,
      `NAME` varchar(45) NOT NULL,
      `ADDRESS` varchar(255) NOT NULL,
      `CREATED_DATE` datetime NOT NULL,
      PRIMARY KEY (`CUSTOMER_ID`)
    ) ENGINE=InnoDB AUTO_INCREMENT=17 DEFAULT CHARSET=utf8;

    insert into mkyongdb.customer(customer_id, name, address, created_date)
    values(1, 'mkyong1', 'address1', now());
    insert into mkyongdb.customer(customer_id, name, address, created_date)
    values(2, 'mkyong2', 'address2', now());
    insert into mkyongdb.customer(customer_id, name, address, created_date)
    values(3, 'mkyong3', 'address3', now());
    insert into mkyongdb.customer(customer_id, name, address, created_date)
    values(4, 'mkyong4', 'address4', now());
    insert into mkyongdb.customer(customer_id, name, address, created_date)
    values(5, 'mkyong5', 'address5', now());

## 2\. MySQL DataSource

Configure a MySQL datasource named “**jdbc/mkyongdb**“, follow this article – [How to configure MySQL DataSource in Tomcat 6](http://www.mkyong.com/tomcat/how-to-configure-mysql-datasource-in-tomcat-6/)

## 3\. Model Class

Create a “_Customer_” model class to store the table records.

_File : Customer.java_

    package com.mkyong.customer.model;

    import java.util.Date;

    public class Customer{

    	public long customerID;
    	public String name;
    	public String address;
    	public Date created_date;

    	//getter and setter methods
    }

## 4\. JDBC Example

A JSF 2.0 managed bean, inject datasource “**jdbc/mkyongdb**” via `@Resource`, and uses normal JDBC API to retrieve all the customer records from database and store it into a List.

_File : CustomerBean.java_

    package com.mkyong;

    import java.io.Serializable;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.util.ArrayList;
    import java.util.List;

    import javax.annotation.Resource;
    import javax.faces.bean.ManagedBean;
    import javax.faces.bean.SessionScoped;
    import javax.naming.Context;
    import javax.naming.InitialContext;
    import javax.naming.NamingException;
    import javax.sql.DataSource;

    import com.mkyong.customer.model.Customer;

    @ManagedBean(name="customer")
    @SessionScoped
    public class CustomerBean implements Serializable{

    	//resource injection
    	@Resource(name="jdbc/mkyongdb")
    	private DataSource ds;

    	//if resource injection is not support, you still can get it manually.
    	/*public CustomerBean(){
    		try {
    			Context ctx = new InitialContext();
    			ds = (DataSource)ctx.lookup("java:comp/env/jdbc/mkyongdb");
    		} catch (NamingException e) {
    			e.printStackTrace();
    		}

    	}*/

    	//connect to DB and get customer list
    	public List<Customer> getCustomerList() throws SQLException{

    		if(ds==null)
    			throw new SQLException("Can't get data source");

    		//get database connection
    		Connection con = ds.getConnection();

    		if(con==null)
    			throw new SQLException("Can't get database connection");

    		PreparedStatement ps
    			= con.prepareStatement(
    			   "select customer_id, name, address, created_date from customer");

    		//get customer data from database
    		ResultSet result =  ps.executeQuery();

    		List<Customer> list = new ArrayList<Customer>();

    		while(result.next()){
    			Customer cust = new Customer();

    			cust.setCustomerID(result.getLong("customer_id"));
    			cust.setName(result.getString("name"));
    			cust.setAddress(result.getString("address"));
    			cust.setCreated_date(result.getDate("created_date"));

    			//store all data into a List
    			list.add(cust);
    		}

    		return list;
    	}
    }

## 5\. JSF Page dataTable

A JSF 2.0 xhtml page, uses `h:dataTable` to display all the customer records in table layout format.

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml"
          xmlns:h="http://java.sun.com/jsf/html"
          xmlns:f="http://java.sun.com/jsf/core"
          >
        <h:head>
        	<h:outputStylesheet library="css" name="table-style.css"  />
        </h:head>

        <h:body>

        	<h1>JSF 2.0 + JDBC Example</h1>

     		<h:dataTable value="#{customer.getCustomerList()}" var="c"
        			styleClass="order-table"
        			headerClass="order-table-header"
        			rowClasses="order-table-odd-row,order-table-even-row"
        		>

        		<h:column>
        			<f:facet name="header">
        				Customer ID
        			</f:facet>
        				#{c.customerID}
        		</h:column>

        		<h:column>
        			<f:facet name="header">
        				Name
    				</f:facet>
        				#{c.name}
        		</h:column>

     			<h:column>
        			<f:facet name="header">
        				Address
    				</f:facet>
        				#{c.address}
        		</h:column>

        		<h:column>
        			<f:facet name="header">
        				Created Date
    				</f:facet>
        				#{c.created_date}
        		</h:column>

        	</h:dataTable>

        </h:body>

    </html>

## 6\. Demo

Run it, see output

![](http://www.mkyong.com/wp-content/uploads/2010/12/jsf2-jdbc-integration-example.png)

[http://www.mkyong.com/jsf2/jsf-2-0-jdbc-integration-example/](http://www.mkyong.com/jsf2/jsf-2-0-jdbc-integration-example/)
