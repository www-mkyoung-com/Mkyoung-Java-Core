In previous article, we show you [how to compress files to a zip file format](http://www.mkyong.com/java/how-to-compress-files-in-zip-format/). In this article we will show you how to unzip it.

1.  Read ZIP file with “**ZipInputStream**”
2.  Get the files to “**ZipEntry**” and output it to “**FileOutputStream**“

## 1\. Decompress ZIP file example

In this example, it will read a ZIP file from “**C:\\MyFile.zip**“, and decompress all zipped files to “**C:\\outputzip**” folder.

    package com.mkyong.zip;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    import java.util.List;
    import java.util.zip.ZipEntry;
    import java.util.zip.ZipInputStream;

    public class UnZip
    {
        List<String> fileList;
        private static final String INPUT_ZIP_FILE = "C:\\MyFile.zip";
        private static final String OUTPUT_FOLDER = "C:\\outputzip";

        public static void main( String[] args )
        {
        	UnZip unZip = new UnZip();
        	unZip.unZipIt(INPUT_ZIP_FILE,OUTPUT_FOLDER);
        }

        /**
         * Unzip it
         * @param zipFile input zip file
         * @param output zip file output folder
         */
        public void unZipIt(String zipFile, String outputFolder){

         byte[] buffer = new byte[1024];

         try{

        	//create output directory is not exists
        	File folder = new File(OUTPUT_FOLDER);
        	if(!folder.exists()){
        		folder.mkdir();
        	}

        	//get the zip file content
        	ZipInputStream zis =
        		new ZipInputStream(new FileInputStream(zipFile));
        	//get the zipped file list entry
        	ZipEntry ze = zis.getNextEntry();

        	while(ze!=null){

        	   String fileName = ze.getName();
               File newFile = new File(outputFolder + File.separator + fileName);

               System.out.println("file unzip : "+ newFile.getAbsoluteFile());

                //create all non exists folders
                //else you will hit FileNotFoundException for compressed folder
                new File(newFile.getParent()).mkdirs();

                FileOutputStream fos = new FileOutputStream(newFile);

                int len;
                while ((len = zis.read(buffer)) > 0) {
           		fos.write(buffer, 0, len);
                }

                fos.close();
                ze = zis.getNextEntry();
        	}

            zis.closeEntry();
        	zis.close();

        	System.out.println("Done");

        }catch(IOException ex){
           ex.printStackTrace();
        }
       }
    }

_Output_

    file unzip : C:\outputzip\pdf\Java-Interview.pdf
    file unzip : C:\outputzip\spy\log\spy.log
    file unzip : C:\outputzip\utf-encoded.txt
    file unzip : C:\outputzip\utf.txt
    Done

## Reference

1.  [Compressing and Decompressing Data Using Java APIs](http://java.sun.com/developer/technicalArticles/Programming/compression/)

[http://www.mkyong.com/java/how-to-decompress-files-from-a-zip-file/](http://www.mkyong.com/java/how-to-decompress-files-from-a-zip-file/)
