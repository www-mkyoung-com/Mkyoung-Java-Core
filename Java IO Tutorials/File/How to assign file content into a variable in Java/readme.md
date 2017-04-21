Most people will read the file content and assign to StringBuffer or String line by line. Here’s another trick that may interest you – how to assign whole file content into a variable with one Java’s statement, try it :)

## Example

In this example, you will use **DataInputStream**to convert all the content into bytes, and create a String variable with the converted bytes.

    package com.mkyong.io;

    import java.io.DataInputStream;
    import java.io.FileInputStream;

    public class App{

    	public static void main (String args[]) {

    	try{

    	         DataInputStream dis =
    		    new DataInputStream (
    		    	 new FileInputStream ("c:\\logging.log"));

    		 byte[] datainBytes = new byte[dis.available()];
    		 dis.readFully(datainBytes);
    		 dis.close();

    		 String content = new String(datainBytes, 0, datainBytes.length);

    		 System.out.println(content);

    	}catch(Exception ex){
    		ex.printStackTrace();
    	}

      }
    }

## Output

This will print out all the “logging.log” file content.

    10:21:29,425  INFO Version:15 - Hibernate Annotations 3.3.0.GA
    10:21:29,441  INFO Environment:509 - Hibernate 3.2.3
    10:21:29,441  INFO Environment:542 - hibernate.properties not found
    10:21:29,456  INFO Environment:676 - Bytecode provider name : cglib
    10:21:29,456  INFO Environment:593 - using JDK 1.4 java.sql.Timestamp handling
    ............

[http://www.mkyong.com/java/how-to-assign-file-content-into-a-variable-in-java/](http://www.mkyong.com/java/how-to-assign-file-content-into-a-variable-in-java/)
