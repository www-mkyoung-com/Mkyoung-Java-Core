There are no official way to get the file creation date in Java. However, you can use the following workaround to get the file creation date in Windows platform.

## How it work

In Windows command prompt, type the command to list the file creation date.

    C:\>cmd /c dir c:\logfile.log /tc
     Volume in drive C has no label.
     Volume Serial Number is 0410-1EC3

     Directory of c:\

    31/05/2010  08:05                14 logfile.log
                   1 File(s)             14 bytes
                   0 Dir(s)  35,389,460,480 bytes free

The “**31/05/2010 08:05**” is what you need. The idea is use the Java “**Runtime.getRuntime().exec**” to execute the above command, hold the output, and parse it by lines until you get the date and time.

## Example

In this example, it will get the creation date of file (c:\\logfile.log).

    package com.mkyong.file;

    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.util.StringTokenizer;

    public class GetFileCreationDateExample
    {
        public static void main(String[] args)
        {

        	try{

        		Process proc =
        		   Runtime.getRuntime().exec("cmd /c dir c:\\logfile.log /tc");

        		BufferedReader br =
        		   new BufferedReader(
        		      new InputStreamReader(proc.getInputStream()));

        		String data ="";

        		//it's quite stupid but work
        		for(int i=0; i<6; i++){
        			data = br.readLine();
        		}

        		System.out.println("Extracted value : " + data);

        		//split by space
        		StringTokenizer st = new StringTokenizer(data);
        		String date = st.nextToken();//Get date
        		String time = st.nextToken();//Get time

        		System.out.println("Creation Date  : " + date);
        		System.out.println("Creation Time  : " + time);

        	}catch(IOException e){

        		e.printStackTrace();

        	}

        }
    }

## Result

    Extracted value : 31/05/2010  08:05  14 logfile.log
    Creation Date  : 31/05/2010
    Creation Time  : 08:05

[http://www.mkyong.com/java/how-to-get-the-file-creation-date-in-java/](http://www.mkyong.com/java/how-to-get-the-file-creation-date-in-java/)
