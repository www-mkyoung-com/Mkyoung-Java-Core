In Java, file permissions are very OS specific: *nix , NTFS (windows) and FAT/FAT32, all have different kind of file permissions. Java comes with some generic file permission to deal with it.

**Check if the file permission allow** :

1.  file.canExecute(); – return true, file is executable; false is not.
2.  file.canWrite(); – return true, file is writable; false is not.
3.  file.canRead(); – return true, file is readable; false is not.

**Set the file permission** :

1.  file.setExecutable(boolean); – true, allow execute operations; false to disallow it.
2.  file.setReadable(boolean); – true, allow read operations; false to disallow it.
3.  file.setWritable(boolean); – true, allow write operations; false to disallow it.

In *nix system, you may need to configure more specifies about file permission, e.g set a 777 permission for a file or directory, however, Java IO classes do not have ready method for it, but you can use the following dirty workaround :

    Runtime.getRuntime().exec("chmod 777 file");

## File permission example

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class FilePermissionExample
    {
        public static void main( String[] args )
        {
        	try {

    	      File file = new File("/mkyong/shellscript.sh");

    	      if(file.exists()){
    	    	  System.out.println("Is Execute allow : " + file.canExecute());
    		  System.out.println("Is Write allow : " + file.canWrite());
    		  System.out.println("Is Read allow : " + file.canRead());
    	      }

    	      file.setExecutable(false);
    	      file.setReadable(false);
    	      file.setWritable(false);

    	      System.out.println("Is Execute allow : " + file.canExecute());
    	      System.out.println("Is Write allow : " + file.canWrite());
    	      System.out.println("Is Read allow : " + file.canRead());

    	      if (file.createNewFile()){
    	        System.out.println("File is created!");
    	      }else{
    	        System.out.println("File already exists.");
    	      }

        	} catch (IOException e) {
    	      e.printStackTrace();
    	    }
        }
    }

## Reference

1.  [http://java.sun.com/javase/6/docs/api/java/io/File.html](http://java.sun.com/javase/6/docs/api/java/io/File.html)

[http://www.mkyong.com/java/how-to-set-the-file-permission-in-java/](http://www.mkyong.com/java/how-to-set-the-file-permission-in-java/)
