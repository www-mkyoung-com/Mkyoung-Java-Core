Here’s an example to check if a directory is empty.

## Example

    package com.mkyong.file;

    import java.io.File;

    public class CheckEmptyDirectoryExample
    {
        public static void main(String[] args)
        {

    	File file = new File("C:\\folder");

    	if(file.isDirectory()){

    		if(file.list().length>0){

    			System.out.println("Directory is not empty!");

    		}else{

    			System.out.println("Directory is empty!");

    		}

    	}else{

    		System.out.println("This is not a directory");

    	}
        }
    }

[http://www.mkyong.com/java/how-to-check-if-directory-is-empty-in-java/](http://www.mkyong.com/java/how-to-check-if-directory-is-empty-in-java/)
