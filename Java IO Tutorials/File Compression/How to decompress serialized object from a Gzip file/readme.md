In last section, you learn about [how to compress a serialized object into a file](http://www.mkyong.com/java/how-to-compress-serialized-object-into-file/), now you learn how to decompress it from a Gzip file.

    FileInputStream fin = new FileInputStream("c:\\address.gz");
    GZIPInputStream gis = new GZIPInputStream(fin);
    ObjectInputStream ois = new ObjectInputStream(gis);
    address = (Address) ois.readObject();

## GZIP example

In this example, you will decompress a compressed file “**address.gz**“, and print it out the value.

    package com.mkyong.io;

    import java.io.FileInputStream;
    import java.io.ObjectInputStream;
    import java.io.Serializable;
    import java.util.zip.GZIPInputStream;

    public class Deserializer implements Serializable{

       public static void main (String args[]) {

    	   Deserializer deserializer = new Deserializer();
    	   Address address = deserializer.deserialzeAddress();
    	   System.out.println(address);
       }

       public Address deserialzeAddress(){

    	   Address address;

    	   try{

    		   FileInputStream fin = new FileInputStream("c:\\address.gz");
    		   GZIPInputStream gis = new GZIPInputStream(fin);
    		   ObjectInputStream ois = new ObjectInputStream(gis);
    		   address = (Address) ois.readObject();
    		   ois.close();

    		   return address;

    	   }catch(Exception ex){
    		   ex.printStackTrace();
    		   return null;
    	   }
       }
    }

## Output

    Street : wall street Country : united state

[http://www.mkyong.com/java/how-to-decompress-serialized-object-from-a-gzip-file/](http://www.mkyong.com/java/how-to-decompress-serialized-object-from-a-gzip-file/)
