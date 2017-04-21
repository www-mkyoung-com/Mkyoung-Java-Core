To delete a directory, you can simply use the **File.delete()**, but the directory must be empty in order to delete it.

Often times, you may require to perform **recursive delete in a directory**, which means all it’s sub-directories and files should be delete as well, see below example :

## Directory recursive delete example

Delete the directory named “**C:\\mkyong-new**“, and all it’s sub-directories and files as well. The code is self-explanatory and well documented, it should be easy to understand.

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class DeleteDirectoryExample
    {
        private static final String SRC_FOLDER = "C:\\mkyong-new";

        public static void main(String[] args)
        {

        	File directory = new File(SRC_FOLDER);

        	//make sure directory exists
        	if(!directory.exists()){

               System.out.println("Directory does not exist.");
               System.exit(0);

            }else{

               try{

                   delete(directory);

               }catch(IOException e){
                   e.printStackTrace();
                   System.exit(0);
               }
            }

        	System.out.println("Done");
        }

        public static void delete(File file)
        	throws IOException{

        	if(file.isDirectory()){

        		//directory is empty, then delete it
        		if(file.list().length==0){

        		   file.delete();
        		   System.out.println("Directory is deleted : "
                                                     + file.getAbsolutePath());

        		}else{

        		   //list all the directory contents
            	   String files[] = file.list();

            	   for (String temp : files) {
            	      //construct the file structure
            	      File fileDelete = new File(file, temp);

            	      //recursive delete
            	     delete(fileDelete);
            	   }

            	   //check the directory again, if empty then delete it
            	   if(file.list().length==0){
               	     file.delete();
            	     System.out.println("Directory is deleted : "
                                                      + file.getAbsolutePath());
            	   }
        		}

        	}else{
        		//if file, then delete it
        		file.delete();
        		System.out.println("File is deleted : " + file.getAbsolutePath());
        	}
        }
    }

## Result

    File is deleted : C:\mkyong-new\404.php
    File is deleted : C:\mkyong-new\archive.php
    ...
    Directory is deleted : C:\mkyong-new\includes
    File is deleted : C:\mkyong-new\index.php
    File is deleted : C:\mkyong-new\index.php.hacked
    File is deleted : C:\mkyong-new\js\hoverIntent.js
    File is deleted : C:\mkyong-new\js\jquery-1.4.2.min.js
    File is deleted : C:\mkyong-new\js\jquery.bgiframe.min.js
    Directory is deleted : C:\mkyong-new\js\superfish-1.4.8\css
    Directory is deleted : C:\mkyong-new\js\superfish-1.4.8\images
    Directory is deleted : C:\mkyong-new\js\superfish-1.4.8
    File is deleted : C:\mkyong-new\js\superfish-navbar.css
    ...
    Directory is deleted : C:\mkyong-new
    Done

[http://www.mkyong.com/java/how-to-delete-directory-in-java/](http://www.mkyong.com/java/how-to-delete-directory-in-java/)
