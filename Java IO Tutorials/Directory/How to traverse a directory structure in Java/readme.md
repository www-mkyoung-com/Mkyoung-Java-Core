In this example, the program will traverse the given directory and print out all the directories and files absolute path and name one by one.

## Example

    package com.mkyong.io;

    import java.io.File;

    public class DisplayDirectoryAndFile{

    	public static void main (String args[]) {

    		displayIt(new File("C:\\Downloads"));
    	}

    	public static void displayIt(File node){

    		System.out.println(node.getAbsoluteFile());

    		if(node.isDirectory()){
    			String[] subNote = node.list();
    			for(String filename : subNote){
    				displayIt(new File(node, filename));
    			}
    		}

    	}
    }

## Output

    C:\Downloads
    C:\Downloads\100 Java Tips.pdf
    C:\Downloads\1590599799.rar
    C:\Downloads\2009
    C:\Downloads\573440.flv
    C:\Downloads\575492.flv
    C:\Downloads\avira_antivir_personal_en.exe
    C:\Downloads\backup-mkyong.com-12-24-2009.tar.gz
    ......

[http://www.mkyong.com/java/how-to-traverse-a-directory-structure-in-java/](http://www.mkyong.com/java/how-to-traverse-a-directory-structure-in-java/)
