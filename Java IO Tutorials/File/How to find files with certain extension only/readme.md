A `[FilenameFilter](http://docs.oracle.com/javase/1.4.2/docs/api/java/io/FilenameFilter.html)` example, it will only display files that use “**.jpg**” extension in folder “**c:\\folder**“.

    package com.mkyong.io;

    import java.io.*;

    public class FindCertainExtension {

    	private static final String FILE_DIR = "c:\\folder";
    	private static final String FILE_TEXT_EXT = ".jpg";

    	public static void main(String args[]) {
    		new FindCertainExtension().listFile(FILE_DIR, FILE_TEXT_EXT);
    	}

    	public void listFile(String folder, String ext) {

    		GenericExtFilter filter = new GenericExtFilter(ext);

    		File dir = new File(folder);

    		if(dir.isDirectory()==false){
    			System.out.println("Directory does not exists : " + FILE_DIR);
    			return;
    		}

    		// list out all the file name and filter by the extension
    		String[] list = dir.list(filter);

    		if (list.length == 0) {
    			System.out.println("no files end with : " + ext);
    			return;
    		}

    		for (String file : list) {
    			String temp = new StringBuffer(FILE_DIR).append(File.separator)
    					.append(file).toString();
    			System.out.println("file : " + temp);
    		}
    	}

    	// inner class, generic extension filter
    	public class GenericExtFilter implements FilenameFilter {

    		private String ext;

    		public GenericExtFilter(String ext) {
    			this.ext = ext;
    		}

    		public boolean accept(File dir, String name) {
    			return (name.endsWith(ext));
    		}
    	}
    }

[http://www.mkyong.com/java/how-to-find-files-with-certain-extension-only/](http://www.mkyong.com/java/how-to-find-files-with-certain-extension-only/)
