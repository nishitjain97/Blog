---
title: 10. File I/O
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-09-29'
lastmod: '2020-09-29'
---

## File

- ```File f = new File("abc.txt");```

- This creates a Java file object but not an actual file. If file exists, it will be referred to by f, else not

```
File f = new File("abc.txt");
System.out.println(f.exists());
f.createNewFile();
System.out.println(f.exists());
```

- Java is based on UNIX perating system where everything is considered as a file (even directories)

```
File f = new File("Nishit");
System.out.println(f.exists()); // false
f.mkdir();
System.out.println(f.exists()); // true
```

- Constructors

    - ```File f = new File(String name)```: 'name' can be file or directory in current working directory

    - ```File f = new File(String subdir, String name)```: Create inside specific subdir

    - ```File f = new File(File subdir, String name)```: Passing reference of a sub-directory

- Method

    - ```boolean exists()```

    - ```boolean createNewFile()```: If file already present, returns false. Returns true if file is created by this method.

    - ```boolean mkdir()```: Same as above, but for directory

    - ```boolean isFile()```

    - ```boolean isDirectory()```

    - ```String[] list()```: Returns names of all files and subdirectories in specified directory

    - ```long length()``` Number of characters in file

    - ```boolean delete()```

## FileWriter

- To write character data to files

- Constructors

    - ```FileWriter fw = new FileWriter(String filename)```

    - ```FileWriter fw = new FileWriter(File f)```

        - These constructors overwrite file if data is already present in them

    - ```FileWriter fw = new FileWriter(String fname, boolean append)```

    - ```FileWriter fw = new FileWriter(File f, boolean append)```

        - If the file is not already available, these constructors would create the file

- Methods

    - ```write(int ch)```

    - ```write(char[] ch)```

    - ```write(String s)```

    - ```flush()```: Applicable for Writers to guarantee that total data, including last character, will be returned to file

    - ```close()```
    
- The problem with FileWriter is newline characters have to be manually inserted. This is a burden for programmer as the symbol for newline might change based on operating system.

## FileReader

- To read character data from a file

- Constructors

    - ```FileReader fr = new FileReader(String fname)```

    - ```FileReader fr = new FileReader(File f)```

- Methods

    - ```int read()```: Attempts to read next character and return unicode value of character. If no next character, returns -1

    - ```int read(char[] ch)``` Attempts to read enough characters from file to character array and returns number of characters copied

    - ```void close()```

- Same problem as FileWriter where files are read character by character, making it inconvenient for programmers

## BufferedWriter

- To write character data to the file

- Constructors

    - ```BufferedWriter bw = new BufferedWriter(Writer w)```

    - ```BufferedWriter bw = new BufferedWriter(Writer w, int bufferSize)```

        - BW can't communicate directly with the file. It needs a Writer object.

- Methods: First 5 methods are same as FileWriter methods

    - ```newLine()```: To insert line separator

- Closing BW would internally automatically close FW.

## BufferedReader

- To read character data from a file

- We can read data line by line in addition to char by char

- Constructor

    - ```BufferedReader br = new BufferedReader(Reader r)```

    - ```BufferedReader br = new BufferedReader(Reader r, int bufferSize)```

        - br can't directly communicate with the file and needs FileReader

- Methods: First 3 methods are same as FileReader

    - ```String readLine()```: Attempts to read next line from file. Does this until getting null.

- Closing BR automatically closes internal FR

- Most enhanced Reader to read char data from file.

## PrintWriter

- The previous Writers had some problems

    - Newline symbol in FW and newLine() method in BW was still inconvenient to programmers

    - They only worked for character data. Any other type had to be converted to string before storing

- PrintWriter improves on these problems and is the most enhanced Writer

- Constructors

    - ```PrintWriter pw = new PrintWriter(String fname)```

    - ```PrintWriter pw = new PrintWriter(File file)```

    - ```PrintWriter pw = new PrintWriter(Writer w)```

        - It can communicate directly with the file or through another writer.

- Methods

    - First 5 methods are same as the other Writers

    - ```print(char ch)```

    - ```print(int i)```

    - ```print(double d)```

    - ```print(boolean b)```

    - ```print(String s)```

    - The above 5 methods are also available as println()

- **Note:** Readers and Writers are used to handle text data. We use Streams to handle binary data (images, pdf, video etc.)



<div>
    <img src="/docs/java/core_java_ocjp_scjp/file_io_hierarchy.png" style="height:300px;margin:auto;">
</div>