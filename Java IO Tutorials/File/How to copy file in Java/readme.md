Java didn’t comes with any ready make file copy function, you have to manual create the file copy process. To copy file, just convert the file into a bytes stream with **FileInputStream** and write the bytes into another file with **FileOutputStream**.

The overall processes are quite simple, just do not understand why Java doesn’t include this method into the **java.io.File** class.

## File copy example

Here’s an example to copy a file named “Afile.txt” to another file named “Bfile.txt”. If the “Bfile.txt” is exists, the existing content will be replace, else it will create with the content of the “Afile.txt”.

    package com.mkyong.file;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.OutputStream;

    public class CopyFileExample
    {
        public static void main(String[] args)
        {

        	InputStream inStream = null;
    	OutputStream outStream = null;

        	try{

        	    File afile =new File("Afile.txt");
        	    File bfile =new File("Bfile.txt");

        	    inStream = new FileInputStream(afile);
        	    outStream = new FileOutputStream(bfile);

        	    byte[] buffer = new byte[1024];

        	    int length;
        	    //copy the file content in bytes
        	    while ((length = inStream.read(buffer)) > 0){

        	    	outStream.write(buffer, 0, length);

        	    }

        	    inStream.close();
        	    outStream.close();

        	    System.out.println("File is copied successful!");

        	}catch(IOException e){
        		e.printStackTrace();
        	}
        }
    }

[http://www.mkyong.com/java/how-to-copy-file-in-java/](http://www.mkyong.com/java/how-to-copy-file-in-java/)
