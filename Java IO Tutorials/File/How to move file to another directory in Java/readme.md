**Java.io.File** does not contains any ready make move file method, but you can workaround with the following two alternatives :

1.  File.renameTo().
2.  Copy to new file and delete the original file.

In the below two examples, you move a file “**C:\\folderA\\Afile.txt**” from one directory to another directory with the same file name “**C:\\folderB\\Afile.txt**“.

## 1\. File.renameTo()

    package com.mkyong.file;

    import java.io.File;

    public class MoveFileExample
    {
        public static void main(String[] args)
        {
        	try{

        	   File afile =new File("C:\\folderA\\Afile.txt");

        	   if(afile.renameTo(new File("C:\\folderB\\" + afile.getName()))){
        		System.out.println("File is moved successful!");
        	   }else{
        		System.out.println("File is failed to move!");
        	   }

        	}catch(Exception e){
        		e.printStackTrace();
        	}
        }
    }

## 2\. Copy and Delete

    package com.mkyong.file;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.OutputStream;

    public class MoveFileExample
    {
        public static void main(String[] args)
        {

        	InputStream inStream = null;
    	OutputStream outStream = null;

        	try{

        	    File afile =new File("C:\\folderA\\Afile.txt");
        	    File bfile =new File("C:\\folderB\\Afile.txt");

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

        	    //delete the original file
        	    afile.delete();

        	    System.out.println("File is copied successful!");

        	}catch(IOException e){
        	    e.printStackTrace();
        	}
        }
    }

[http://www.mkyong.com/java/how-to-move-file-to-another-directory-in-java/](http://www.mkyong.com/java/how-to-move-file-to-another-directory-in-java/)
