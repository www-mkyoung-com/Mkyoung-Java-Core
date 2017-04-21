Gzip is a popular tool to compress a file in *nix system. However, Gzip is not a ZIP tool, **it only use to compress a file into a “.gz” format, not compress several files into a single archive**.

## GZip example

In this example, it will compress a file “**/home/mkyong/file1.txt**” into a gzip file – “**/home/mkyong/file1.gz**“.

    package com.mkyong.gzip;

    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.util.zip.GZIPOutputStream;

    public class GZipFile
    {
        private static final String OUTPUT_GZIP_FILE = "/home/mkyong/file1.gz";
        private static final String SOURCE_FILE = "/home/mkyong/file1.txt";

        public static void main( String[] args )
        {
        	GZipFile gZip = new GZipFile();
        	gZip.gzipIt();
        }

        /**
         * GZip it
         * @param zipFile output GZip file location
         */
        public void gzipIt(){

         byte[] buffer = new byte[1024];

         try{

        	GZIPOutputStream gzos =
        		new GZIPOutputStream(new FileOutputStream(OUTPUT_GZIP_FILE));

            FileInputStream in =
                new FileInputStream(SOURCE_FILE);

            int len;
            while ((len = in.read(buffer)) > 0) {
            	gzos.write(buffer, 0, len);
            }

            in.close();

        	gzos.finish();
        	gzos.close();

        	System.out.println("Done");

        }catch(IOException ex){
           ex.printStackTrace();
        }
       }

    }

## Follow up

[How to decompress file from a gzip file.](http://www.mkyong.com/java/how-to-decompress-file-from-gzip-file/)

## Reference

1.  [http://java.sun.com/developer/technicalArticles/Programming/compression/](http://java.sun.com/developer/technicalArticles/Programming/compression/)
2.  [http://www.gzip.org/](http://www.gzip.org/)
3.  [http://en.wikipedia.org/wiki/Gzip](http://en.wikipedia.org/wiki/Gzip)

[http://www.mkyong.com/java/how-to-compress-a-file-in-gzip-format/](http://www.mkyong.com/java/how-to-compress-a-file-in-gzip-format/)
