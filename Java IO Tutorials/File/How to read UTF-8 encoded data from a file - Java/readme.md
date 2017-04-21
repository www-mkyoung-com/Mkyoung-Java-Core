A text file with UTF-8 encoded data

![utf8 encoded file](http://www.mkyong.com/wp-content/uploads/2009/04/utf8-result.jpg)

_P.S File is created by this article [How to write UTF-8 encoded data into a file](http://www.mkyong.com/java/how-to-write-utf-8-encoded-data-into-a-file-java/)_

Here’s the example to demonstrate how to read “UTF-8” encoded data from a file in Java

    package com.mkyong;

    import java.io.BufferedReader;
    import java.io.File;
    import java.io.FileInputStream;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.io.UnsupportedEncodingException;

    public class test {
    	public static void main(String[] args){

    	try {
    		File fileDir = new File("c:\\temp\\test.txt");

    		BufferedReader in = new BufferedReader(
    		   new InputStreamReader(
                          new FileInputStream(fileDir), "UTF8"));

    		String str;

    		while ((str = in.readLine()) != null) {
    		    System.out.println(str);
    		}

                    in.close();
    	    }
    	    catch (UnsupportedEncodingException e)
    	    {
    			System.out.println(e.getMessage());
    	    }
    	    catch (IOException e)
    	    {
    			System.out.println(e.getMessage());
    	    }
    	    catch (Exception e)
    	    {
    			System.out.println(e.getMessage());
    	    }
    	}
    }

## Result

    Website UTF-8
    ?? UTF-8
    ??????? UTF-8

Do not worry about the symbol “???”, this is because my output console is not support the UTF-8 data. The variable “str” is storing exactly same “UTF-8” encoded data as showed in the text file.

[http://www.mkyong.com/java/how-to-read-utf-8-encoded-data-from-a-file-java/](http://www.mkyong.com/java/how-to-read-utf-8-encoded-data-from-a-file-java/)
