Here’s an example to copy a directory and all its sub-directories and files to a new destination directory. The code is full of comments and self-explanatory, left me comment if you need more explanation.

## Example

Copy folder “**c:\\mkyong**” and its sub-directories and files to another new folder “**c:\\mkyong-new**“.

    package com.mkyong.file;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.OutputStream;

    public class CopyDirectoryExample
    {
        public static void main(String[] args)
        {
        	File srcFolder = new File("c:\\mkyong");
        	File destFolder = new File("c:\\mkyong-new");

        	//make sure source exists
        	if(!srcFolder.exists()){

               System.out.println("Directory does not exist.");
               //just exit
               System.exit(0);

            }else{

               try{
            	copyFolder(srcFolder,destFolder);
               }catch(IOException e){
            	e.printStackTrace();
            	//error, just exit
                    System.exit(0);
               }
            }

        	System.out.println("Done");
        }

        public static void copyFolder(File src, File dest)
        	throws IOException{

        	if(src.isDirectory()){

        		//if directory not exists, create it
        		if(!dest.exists()){
        		   dest.mkdir();
        		   System.out.println("Directory copied from "
                                  + src + "  to " + dest);
        		}

        		//list all the directory contents
        		String files[] = src.list();

        		for (String file : files) {
        		   //construct the src and dest file structure
        		   File srcFile = new File(src, file);
        		   File destFile = new File(dest, file);
        		   //recursive copy
        		   copyFolder(srcFile,destFile);
        		}

        	}else{
        		//if file, then copy it
        		//Use bytes stream to support all file types
        		InputStream in = new FileInputStream(src);
        	        OutputStream out = new FileOutputStream(dest);

        	        byte[] buffer = new byte[1024];

        	        int length;
        	        //copy the file content in bytes
        	        while ((length = in.read(buffer)) > 0){
        	    	   out.write(buffer, 0, length);
        	        }

        	        in.close();
        	        out.close();
        	        System.out.println("File copied from " + src + " to " + dest);
        	}
        }
    }

## Result

    Directory copied from c:\mkyong  to c:\mkyong-new
    File copied from c:\mkyong\404.php to c:\mkyong-new\404.php
    File copied from c:\mkyong\footer.php to c:\mkyong-new\footer.php
    File copied from c:\mkyong\js\superfish.css to c:\mkyong-new\js\superfish.css
    File copied from c:\mkyong\js\superfish.js to c:\mkyong-new\js\superfish.js
    File copied from c:\mkyong\js\supersubs.js to c:\mkyong-new\js\supersubs.js
    Directory copied from c:\mkyong\images  to c:\mkyong-new\images
    File copied from c:\mkyong\page.php to c:\mkyong-new\page.php
    Directory copied from c:\mkyong\psd  to c:\mkyong-new\psd
    ...
    Done

[http://www.mkyong.com/java/how-to-copy-directory-in-java/](http://www.mkyong.com/java/how-to-copy-directory-in-java/)
