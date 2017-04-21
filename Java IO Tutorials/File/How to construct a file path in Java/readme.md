In this tutorial, we will show you three Java examples to construct a file path :

1.  File.separator or System.getProperty(“file.separator”) (Recommended)
2.  File file = new File(workingDir, filename); (Recommended)
3.  Create the file separator manually. (Not recommend, just for fun)

## 1\. File.separator

Classic Java example to construct a file path, using `File.separator` or `System.getProperty("file.separator")`. Both will check the OS and returns the file separator correctly, for example,

1.  Windows = `\`
2.  *nix or Mac = `/`

FilePathExample1.java

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class FilePathExample1 {
    	public static void main(String[] args) {
    	  try {

    		String filename = "newFile.txt";
    		String workingDirectory = System.getProperty("user.dir");

    		//****************//

    		String absoluteFilePath = "";

    		//absoluteFilePath = workingDirectory + System.getProperty("file.separator") + filename;
    		absoluteFilePath = workingDirectory + File.separator + filename;

    		System.out.println("Final filepath : " + absoluteFilePath);

    		//****************//

    		File file = new File(absoluteFilePath);

    		if (file.createNewFile()) {
    			System.out.println("File is created!");
    		} else {
    			System.out.println("File is already existed!");
    		}

    	  } catch (IOException e) {
    		e.printStackTrace();
    	  }
    	}
    }

Output

    Final filepath : /Users/mkyong/Documents/workspace/maven/fileUtils/newFile.txt
    File is created!

## 2\. new File()

Some developers are using `new File()` API to construct the file path.

FilePathExample2.java

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class FilePathExample2 {
    	public static void main(String[] args) {
    	  try {

    		String filename = "newFile.txt";
    		String workingDirectory = System.getProperty("user.dir");

    		//****************//

    		File file = new File(workingDirectory, filename);

    		//****************//

    		System.out.println("Final filepath : " + file.getAbsolutePath());
    		if (file.createNewFile()) {
    			System.out.println("File is created!");
    		} else {
    			System.out.println("File is already existed!");
    		}

    	  } catch (IOException e) {
    		e.printStackTrace();
    	  }
    	}
    }

Output

    Final filepath : /Users/mkyong/Documents/workspace/maven/fileUtils/newFile.txt
    File is created!

## 3\. Manual file separator

Check the system OS and create file path manually, just for fun, not recommend.

FilePathExample3.java

    package com.mkyong.file;

    import java.io.File;
    import java.io.IOException;

    public class FilePathExample3 {
    	public static void main(String[] args) {
    	  try {

    		String filename = "testing.txt";
    		String workingDir = System.getProperty("user.dir");

    		String absoluteFilePath = "";

    		//****************//

    		String your_os = System.getProperty("os.name").toLowerCase();

    		if (your_os.indexOf("win") >= 0) {

    			//if windows
    			absoluteFilePath = workingDir + "\\" + filename;

    		} else if (your_os.indexOf("nix") >= 0 ||
                               your_os.indexOf("nux") >= 0 ||
                               your_os.indexOf("mac") >= 0) {

    			//if unix or mac
    			absoluteFilePath = workingDir + "/" + filename;

    		}else{

    			//unknow os?
    			absoluteFilePath = workingDir + "/" + filename;

    		}

    		System.out.println("Final filepath : " + absoluteFilePath);

    		//****************//

    		File file = new File(absoluteFilePath);

    		if (file.createNewFile()) {
    			System.out.println("Done");
    		} else {
    			System.out.println("File already exists!");
    		}

    	  } catch (IOException e) {
    		e.printStackTrace();
    	  }
    	}
    }

Output

    Final filepath : /Users/mkyong/Documents/workspace/maven/fileUtils/newFile.txt
    File is created!

## References

1.  [File JavaDoc](http://java.sun.com/javase/6/docs/api/java/io/File.html)
2.  [How to get current working directory](http://www.mkyong.com/java/how-to-get-the-current-working-directory-in-java/)
3.  [How to detect os in Java](http://www.mkyong.com/java/how-to-detect-os-in-java-systemgetpropertyosname/)
4.  [What os or arch value can I use?](http://lopica.sourceforge.net/os.html)

[http://www.mkyong.com/java/how-to-construct-a-file-path-in-java/](http://www.mkyong.com/java/how-to-construct-a-file-path-in-java/)
