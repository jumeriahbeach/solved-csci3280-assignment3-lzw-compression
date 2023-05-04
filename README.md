Download Link: https://assignmentchef.com/product/solved-csci3280-assignment3-lzw-compression
<br>
In 1984, Terry Welch proposed the LZW algorithm. The LZW algorithm is based on the LZ77 algorithm, which is proposed by A. Lempel and J. Ziv in 1977. Like LZ77 and LZ78, LZW is a dictionary-based compression algorithm and does not perform any analysis on the input text. LZW is widely known for its application in GIF and in the V.42 communication standard. The idea behind the LZW algorithm is simple but there are implementation details that should be taken care of. In this assignment, you are required to write a variant of the LZW algorithm (both the compressor and decompressor). The following sections explain the details.

1. Algorithm  for Compression

<strong>CodeDict </strong>: A dictionary which maps a given char. or sequence of char. to a CODE.

<strong>P </strong>: Prefix string, to store a sequence of characters

<strong>C </strong>: The latest SINGLE character read from the input text file

<strong>X </strong>: A matched code to be output to Archive

<ol>

 <li>Initialize the dictionary <strong>CodeDict</strong> with the first 256 ASCII codes (i.e. 0255). ii. Let <strong>P</strong> = NULL.</li>

 <li>While there are still characters to be read from input file:</li>

 <li>Get a new character B. Search for the string <strong>C</strong> from the input file.<strong>&lt;P,C&gt;</strong> in <strong>CodeDict</strong>:

  <ol>

   <li>if <strong>FOUND</strong><strong>: </strong></li>

  </ol></li>

</ol>

Let Let <strong>XP = &lt;P,C&gt;</strong> = <strong>CodeDict[&lt;P,C&gt;].</strong>        <strong>. </strong>

<ol>

 <li>if <strong>NOT FOUND: </strong></li>

</ol>

Output the code <strong>X</strong> that corresponds to <strong>P </strong>Add a new entry <strong>&lt;P,C&gt; </strong>to <strong>CodeDict. </strong>Let <strong>P = C.</strong>

<ol start="3">

 <li>Output the code that corresponds to</li>

</ol>

The string <strong>P</strong> denotes a prefix. During compression, we create a dictionary <strong>CodeDict</strong> of strings on the fly. For each entry of the dictionary, there is a corresponding code to the string (an arbitrary example: string “abc” has a code of 280). Assume we are at a particular instant of compression, a new character <strong>C</strong> is read from the input file. Then, we search in the dictionary for the presence of the new string <strong>&lt;P,C&gt; </strong>that is created by appending the character <strong>C</strong> to the prefix <strong>P</strong> (<strong>step 2.B</strong>). If this string <strong>&lt;P,C&gt; </strong>could be found (<strong>step 2.B.i</strong>), the code found is memorized as <strong>X</strong>, and we will use the string <strong>&lt;</strong> <strong>P,C&gt;</strong> as a new prefix. The search is then repeated by appending another new character from the input file.

Conceptually, the iteration is equivalent to reading the longest string that is already contained in the dictionary. When the string could not be found (<strong>step 2.B.ii</strong>), we will output the memorized codeword <strong>X</strong> of its prefix and add a new entry to the dictionary for this string.

A practical issue about the implementation is how to store the dictionary which allows efficient lookup. Obviously, a linear array suffices, but the performance (i.e. the execution speed) will be unacceptable since the dictionary lookup step (<strong>step 2.B</strong>) will take too much time. Alternatives will be to use a tree structure, hashing function or some clever data structure you may design.

2. Algorithm for Decompression

<strong> </strong>

<strong>StrDict</strong>: A dictionary which maps a given CODE to a char. or sequence of char.

<strong>PW</strong>: Previous code read from the archive

<strong>CW</strong>: Current code read from the archive

<strong>S</strong>: String to be output to output file

<ol>

 <li>Initialize the dictionary <strong>StrDict</strong> with the first 256 ASCII codes (i.e. 0-255 ).</li>

 <li>Let <strong>PW</strong> = first code read from the archive. iii. Let <strong>C</strong> = <strong>StrDict</strong>[<strong>PW</strong>] and output <strong>C</strong>.</li>

 <li>While there are still codes to be read from the archive:</li>

 <li>Get a new code B. Search for the code <strong>CW</strong> from the archive.<strong>CW</strong> in <strong>StrDict</strong>:

  <ol>

   <li>if <strong>FOUND</strong><strong>: </strong></li>

  </ol></li>

</ol>

Let <strong>C</strong> = First character of <strong>StrDict[CW]</strong>. Let <strong>S</strong> = <strong>StrDict[CW</strong>].

<ol>

 <li>if <strong>NOT FOUND: </strong></li>

</ol>

Let Let <strong>CS</strong>  == First character of  <strong>&lt;StrDict[PW],C&gt;.</strong> <strong>StrDict[PW]</strong>.

<ol>

 <li>Output</li>

 <li>Let <strong>P</strong> = <strong>StrDict[PW]. </strong></li>

 <li>Add a new entry <strong>&lt;P,C&gt;</strong> to</li>

 <li>Let <strong>PW</strong> = <strong>CW</strong>.</li>

</ol>

The decompression process is even easier to understand. It is basically the reverse of the compression process. For a code read from the input stream, the decompression routine will output the corresponding entry in the dictionary and update the dictionary. In closer examination, one would find that the decompression process actually lags behind the compression process. Hence, there will be the case when a code refers to an entry that has not yet been created. To handle this, we just need to follow the routines (<strong>step 2.B.ii</strong>)..

NOTE: We will be using 12-bit codewords. The first 256 entries are reserved for all onecharacter-long (ASCII) code. Apart from the first 256 entries, the last code is also reserved. The code 4095 is used to denote “End-of-file”.

<h2>Standard Requirements</h2>

<ol>

 <li>Program must be coded in ANSI C/C++ and uses standard libraries only.</li>

 <li>The program should be able to archive multiple files.</li>

 <li>The compressor should be able to compress a file of any length. Also, your program should be able to decompress the compressed file to the original file.</li>

 <li>When the 12-bit code or string dictionary is full, you should delete the current dictionary and create a new dictionary, start with the 256 entries.</li>

 <li>A source skeleton program called <strong>“lzw_skeleton.c”</strong> is provided. The complete I/O interface is complete. We have already provided two functions <strong>readCode()</strong> and <strong>writeCode()</strong> for reading and writing N-bit codewords of various lengths, you will use 12bit. You are required to implement <strong>compress()</strong> and <strong>decompress()</strong> functions in the program. The function <strong>compress()</strong> is used to compress a file using LZW compression while the function <strong>decompress()</strong> is used to decompress the data file. You should put all</li>

</ol>

of your implementations in <strong>“lzw.c”.</strong>

<ol start="6">

 <li>Your program should be able to support compression of multiple files into one compressed archive. Therefore, you have to save a header in your compressed file with the following format:</li>

</ol>

<strong>      &lt;filename1&gt;
       &lt;filename2&gt;
 </strong>

<strong>      &lt;filename3&gt;
 </strong>

<strong>      … </strong>

<strong>      &lt;filenameN&gt;
  </strong>

<strong>      
  </strong>

Two convenience functions namely <strong>readArchiveHeader()</strong> and <strong>writeArchiveHeader()</strong> are also included. This header is in stored in plain text, as it will be able to query what is in the file before decompression. Following the header is the compressed files, one after another. When a file is compressed, you have to insert the code “End-of-file” (with value 4095) which indicates a file is ended. While starting to compress a new file, the current dictionary is kept (if not full) instead of reconstruct a new one.

<ol start="7">

 <li>The command line to run your program should have the following format :</li>

</ol>

<strong>Compression:  </strong>

<strong>&gt; lzw –c &lt;lzw filename&gt; &lt;a list of files&gt; Decompression:  </strong>

<strong>&gt; lzw –d &lt;lzw filename&gt;</strong>

<ol start="8">

 <li>You are required to <strong>submit source code only</strong>. We will use Visual Studio 2015 C++ compiler and have your program compiled via visual studio command prompt (ToolsàCommand Prompt) and the following command line (<strong><em>Please make sure your source code gets compiled well with it</em></strong>).</li>

</ol>

<strong>C:&gt; cl lzw.c </strong>

If you use MacOS or Linux, you can compile with clang or gcc.

<ol start="9">

 <li>A example execute file is also provided <strong>“lzw_example.exe”.</strong> You can use it to compress or decompress data and compare the results with your results.</li>

</ol>




<h2>Enhanced Part (20 point)</h2>

You are required to <u>implement the full version of the algorithm described above</u>. Besides, you are also encouraged to use any data structures to implement the dictionary so as to speed up the dictionary lookup process. There is an enhanced part (20%) allotted to the speed of execution. Marks will be rewarded to those who have done any optimization.

Please state your improvement in “README.txt”.