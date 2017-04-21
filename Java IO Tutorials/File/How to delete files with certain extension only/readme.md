In Java, you can implements the [FilenameFilter](http://java.sun.com/j2se/1.4.2/docs/api/java/io/FilenameFilter.html), override the accept(File dir, String name) method, to perform the file filtering function.

In this example, we show you how to use `FilenameFilter` to list out all files that are end with “**.txt**” extension in folder “**c:\\folder**“, and then delete it.

    package com.mkyong.io;

    import java.io.*;

    public class FileChecker {

       private static final String FILE_DIR = "c:\\folder";
       private static final String FILE_TEXT_EXT = ".txt";

       public static void main(String args[]) {
    	new FileChecker().deleteFile(FILE_DIR,FILE_TEXT_EXT);
       }

       public void deleteFile(String folder, String ext){

         GenericExtFilter filter = new GenericExtFilter(ext);
         File dir = new File(folder);

         //list out all the file name with .txt extension
         String[] list = dir.list(filter);

         if (list.length == 0) return;

         File fileDelete;

         for (String file : list){
       	String temp = new StringBuffer(FILE_DIR)
                          .append(File.separator)
                          .append(file).toString();
        	fileDelete = new File(temp);
        	boolean isdeleted = fileDelete.delete();
        	System.out.println("file : " + temp + " is deleted : " + isdeleted);
         }
       }

       //inner class, generic extension filter
       public class GenericExtFilter implements FilenameFilter {

           private String ext;

           public GenericExtFilter(String ext) {
             this.ext = ext;
           }

           public boolean accept(File dir, String name) {
             return (name.endsWith(ext));
           }
        }
    }

[http://www.mkyong.com/java/how-to-delete-files-with-certain-extension-only/](http://www.mkyong.com/java/how-to-delete-files-with-certain-extension-only/)
