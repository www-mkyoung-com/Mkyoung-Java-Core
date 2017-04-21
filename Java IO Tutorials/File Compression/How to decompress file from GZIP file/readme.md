In previous article, you learn about [how to compress a file into a GZip format](http://www.mkyong.com/java/how-to-compress-a-file-in-gzip-format/). In this article, you will learn how to unzip it / decompress the compressed file from a Gzip file.

## Gzip example

In this example, it will decompress the Gzip file “**/home/mkyong/file1.gz**” back to “**/home/mkyong/file1.txt**“.

    package com.mkyong.gzip;

    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.util.zip.GZIPInputStream;

    public class GZipFile
    {
        private static final String INPUT_GZIP_FILE = "/home/mkyong/file1.gz";
        private static final String OUTPUT_FILE = "/home/mkyong/file1.txt";

        public static void main( String[] args )
        {
        	GZipFile gZip = new GZipFile();
        	gZip.gunzipIt();
        }

        /**
         * GunZip it
         */
        public void gunzipIt(){

         byte[] buffer = new byte[1024];

         try{

        	 GZIPInputStream gzis =
        		new GZIPInputStream(new FileInputStream(INPUT_GZIP_FILE));

        	 FileOutputStream out =
                new FileOutputStream(OUTPUT_FILE);

            int len;
            while ((len = gzis.read(buffer)) > 0) {
            	out.write(buffer, 0, len);
            }

            gzis.close();
        	out.close();

        	System.out.println("Done");

        }catch(IOException ex){
           ex.printStackTrace();
        }
       }
    }

## Reference

1.  [http://java.sun.com/developer/technicalArticles/Programming/compression/](http://java.sun.com/developer/technicalArticles/Programming/compression/)
2.  [http://www.gzip.org/](http://www.gzip.org/)
3.  [http://en.wikipedia.org/wiki/Gzip](http://en.wikipedia.org/wiki/Gzip)

[http://www.mkyong.com/java/how-to-decompress-file-from-gzip-file/](http://www.mkyong.com/java/how-to-decompress-file-from-gzip-file/)
