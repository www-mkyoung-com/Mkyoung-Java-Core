Here’s the Java example to demonstrate how to write **UTF-8 encoded data** into a text file – “**c:\\temp\\test.txt**”

_P.S Symbol “??” is some “UTF-8” data in Chinese and Japanese_

<pre>package com.mkyong;

import java.io.BufferedWriter;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.io.UnsupportedEncodingException;
import java.io.Writer;

public class test {
	public static void main(String[] args){

	  try {
		File fileDir = new File("c:\\temp\\test.txt");

		Writer out = new BufferedWriter(new OutputStreamWriter(
			new FileOutputStream(fileDir), "UTF8"));

		out.append("Website UTF-8").append("\r\n");
		out.append("?? UTF-8").append("\r\n");
		out.append("??????? UTF-8").append("\r\n");

		out.flush();
		out.close();

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
</pre>

## Result

![utf8 result](http://www.mkyong.com/wp-content/uploads/2009/04/utf8-result.jpg)

[http://www.mkyong.com/java/how-to-write-utf-8-encoded-data-into-a-file-java/](http://www.mkyong.com/java/how-to-write-utf-8-encoded-data-into-a-file-java/)
