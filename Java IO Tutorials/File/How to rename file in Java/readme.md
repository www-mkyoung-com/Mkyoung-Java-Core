Java comes with **renameTo()** method to rename a file. However , this method is really platform-dependent: you may successfully rename a file in *nix but failed in Windows. So, the return value (true if the file rename successful, false if failed) should always be checked to make sure the file is rename successful.

## File.renameTo() Example

    package com.mkyong.file;

    import java.io.File;

    public class RenameFileExample
    {
        public static void main(String[] args)
        {

    		File oldfile =new File("oldfile.txt");
    		File newfile =new File("newfile.txt");

    		if(oldfile.renameTo(newfile)){
    			System.out.println("Rename succesful");
    		}else{
    			System.out.println("Rename failed");
    		}

        }
    }

## Reference

1.  [File renameTo() documentation](http://java.sun.com/j2se/1.4.2/docs/api/java/io/File.html#renameTo%28java.io.File%29)

[http://www.mkyong.com/java/how-to-rename-file-in-java/](http://www.mkyong.com/java/how-to-rename-file-in-java/)
