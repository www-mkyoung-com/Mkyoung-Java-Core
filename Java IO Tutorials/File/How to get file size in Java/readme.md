In Java, you can use the **File.length()** method to get the file size in bytes.

## Example

Get an image file (c:\\java_xml_logo.jpg) 14KB, and display the file size.

    package com.mkyong.file;

    import java.io.File;

    public class FileSizeExample
    {
        public static void main(String[] args)
        {
    		File file =new File("c:\\java_xml_logo.jpg");

    		if(file.exists()){

    			double bytes = file.length();
    			double kilobytes = (bytes / 1024);
    			double megabytes = (kilobytes / 1024);
    			double gigabytes = (megabytes / 1024);
    			double terabytes = (gigabytes / 1024);
    			double petabytes = (terabytes / 1024);
    			double exabytes = (petabytes / 1024);
    			double zettabytes = (exabytes / 1024);
    			double yottabytes = (zettabytes / 1024);

    			System.out.println("bytes : " + bytes);
    			System.out.println("kilobytes : " + kilobytes);
    			System.out.println("megabytes : " + megabytes);
    			System.out.println("gigabytes : " + gigabytes);
    			System.out.println("terabytes : " + terabytes);
    			System.out.println("petabytes : " + petabytes);
    			System.out.println("exabytes : " + exabytes);
    			System.out.println("zettabytes : " + zettabytes);
    			System.out.println("yottabytes : " + yottabytes);
    		}else{
    			 System.out.println("File does not exists!");
    		}

        }
    }

## Result

    bytes : 13900.0
    kilobytes : 13.57421875
    megabytes : 0.013256072998046875
    gigabytes : 1.2945383787155151E-5
    terabytes : 1.2641976354643703E-8
    petabytes : 1.234568003383174E-11
    exabytes : 1.205632815803881E-14
    zettabytes : 1.1773757966834775E-17
    yottabytes : 1.1497810514487085E-20

[http://www.mkyong.com/java/how-to-get-file-size-in-java/](http://www.mkyong.com/java/how-to-get-file-size-in-java/)
