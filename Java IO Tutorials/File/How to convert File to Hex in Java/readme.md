A simple Java program to demonstrate the use of **String formatter(“%02X “)** to convert a **File into Hex** value. The attached comments should be self-explanatory.

## Example

    package com.mkyong;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.PrintStream;

    public class File2Hex
    {
        public static void convertToHex(PrintStream out, File file) throws IOException {
    	InputStream is = new FileInputStream(file);

    	int bytesCounter =0;
    	int value = 0;
    	StringBuilder sbHex = new StringBuilder();
    	StringBuilder sbText = new StringBuilder();
    	StringBuilder sbResult = new StringBuilder();

    	while ((value = is.read()) != -1) {
    	    //convert to hex value with "X" formatter
                sbHex.append(String.format("%02X ", value));

    	    //If the chracater is not convertable, just print a dot symbol "."
    	    if (!Character.isISOControl(value)) {
    	      	sbText.append((char)value);
    	    }else {
    	        sbText.append(".");
    	    }

    	    //if 16 bytes are read, reset the counter,
                //clear the StringBuilder for formatting purpose only.
    	    if(bytesCounter==15){
    	      	sbResult.append(sbHex).append("      ").append(sbText).append("\n");
    	       	sbHex.setLength(0);
    	        sbText.setLength(0);
    	       	bytesCounter=0;
    	    }else{
    	        bytesCounter++;
    	    }
           }

    	//if still got content
    	if(bytesCounter!=0){
    	     //add spaces more formatting purpose only
    	    for(; bytesCounter<16; bytesCounter++){
    		//1 character 3 spaces
    		sbHex.append("   ");
    	    }
    	    sbResult.append(sbHex).append("      ").append(sbText).append("\n");
            }

            out.print(sbResult);
            is.close();
      }

       public static void main(String[] args) throws IOException
       {
        	//display output to console
        	convertToHex(System.out, new File("c:/file.txt"));

        	//write the output into a file
        	convertToHex(new PrintStream("c:/file.hex"), new File("c:/file.txt"));
        }
    }

## Demo

A File with some dummy content

    ABCDEFG
    12345678
    !@#$%^&*()
    Testing only

After processed by above class, will display the following Hex values :

    41 42 43 44 45 46 47 0D 0A 31 32 33 34 35 36 37       ABCDEFG..1234567
    38 0D 0A 21 40 23 24 25 5E 26 2A 28 29 0D 0A 54       8..!@#$%^&*()..T
    65 73 74 69 6E 67 20 6F 6E 6C 79                      esting only

## Reference

[http://download.oracle.com/javase/1.5.0/docs/api/java/util/Formatter.html#syntax](http://download.oracle.com/javase/1.5.0/docs/api/java/util/Formatter.html#syntax)

[http://www.mkyong.com/java/how-to-convert-file-to-hex-in-java/](http://www.mkyong.com/java/how-to-convert-file-to-hex-in-java/)
