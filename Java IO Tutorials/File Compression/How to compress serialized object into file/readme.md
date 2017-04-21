In last section, you learn about [how to write or serialized an object into a file](http://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/). In this example , you can do more than just serialized it , you also can compress the serialized object to reduce the file size.

The idea is very simple, just using the “**GZIPOutputStream**” for the data compression.

    FileOutputStream fos = new FileOutputStream("c:\\address.gz");
    GZIPOutputStream gz = new GZIPOutputStream(fos);
    ObjectOutputStream oos = new ObjectOutputStream(gz);

## GZIP Example

In this example, you will create an “Address” object , compress it and write it into a file “**c:\\address.gz**“.

_P.S Address object can refer to this [article](http://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/)._

    package com.mkyong.io;

    import java.io.FileOutputStream;
    import java.io.ObjectOutputStream;
    import java.io.Serializable;
    import java.util.zip.GZIPOutputStream;

    public class Serializer implements Serializable{

       public static void main (String args[]) {

    	   Serializer serializer = new Serializer();
    	   serializer.serializeAddress("wall street", "united state");
       }

       public void serializeAddress(String street, String country){

    	   Address address = new Address();
    	   address.setStreet(street);
    	   address.setCountry(country);

    	   try{

    		   FileOutputStream fos = new FileOutputStream("c:\\address.gz");
    		   GZIPOutputStream gz = new GZIPOutputStream(fos);

    		   ObjectOutputStream oos = new ObjectOutputStream(gz);

    		   oos.writeObject(address);
    		   oos.close();

    		   System.out.println("Done");

    	   }catch(Exception ex){
    		   ex.printStackTrace();
    	   }
       }
    }

[http://www.mkyong.com/java/how-to-compress-serialized-object-into-file/](http://www.mkyong.com/java/how-to-compress-serialized-object-into-file/)
