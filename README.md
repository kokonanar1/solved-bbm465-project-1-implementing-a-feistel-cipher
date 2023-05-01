Download Link: https://assignmentchef.com/product/solved-bbm465-project-1-implementing-a-feistel-cipher
<br>
<h1>1                   Experiment</h1>

<strong> </strong>

The aim of this project is to develop a Feistel Cipher and understand the internals of Feistel ciphers e.g. DES, IDEA, RC4/5. You will learn multi round ciphers that enable to encrypt/decrypt data with the right key. You will also learn to implement ECB, CBC and OFB encryption modes for your Feistel Cipher.

A Feistel Cipher has the below format as discussed in the class:




A Feistel Cipher has <em>d</em> rounds of encryption, where in <em>i<sup>th</sup></em> round, a one-way scramble function <em>f</em>  is applied to right half of the data <em>R<sub>i</sub></em> with subkey <em>K<sub>i</sub></em>.

In this project, the main parameters of your Feistel Cipher will be as follows:

<ul>

 <li>10 rounds of encryption/decryption</li>

 <li>96 bit block size</li>

 <li>96 bit key size</li>

</ul>




<u>If the length of the message is less than the block size, the message will padded with all</u> <u>zeros to obtain a 96 bit block.</u>

<strong>Scramble Function: </strong>

In our project, we will assume that scramble functions <em>f<sub>0</sub>, f<sub>1</sub>, f<sub>2</sub> … f<sub>d-1</sub></em> applied on each round are <u>all same</u>. In other words, you will have only one scramble function, which is defined as follows

In the above scramble function, <em>R<sub>i</sub></em> is XORed with <em>K<sub>i</sub></em> first and the result is divided into 8 pieces of 6-bit parts (<em>P1, P2, P3, … P8</em>). Then, P1 and P2 are XORed and saved as the 9<sup>th</sup>  part, P3 and P4  are XORed and saved as the 10<sup>th</sup>  part and so on. As a result of these operations, you will have 12 pieces of 6-bit parts. Then, each 6-bit part is sent to a substitution box like in the DES algorithm. You are expected to use below substitution box:







The substitution box works in similar way to DES boxes. Outer bits of the input are used as the row number, inner bits are used as the column number. The results of 12 substitution box operations will be combined as a 48 bit output and a permutation function will be applied on this output. The permutation function swaps each even digit with the previous odd digit. Assuming <em>B<sub>i</sub></em> represents i<sup>th</sup> bit of the output, the permutation function will do following operation for all bits of the result (0≤ ≤47): Temp = B<sub>2i</sub>

B2i = B2i+1 B<sub>2i+1</sub> = Temp <strong>Subkey Generation: </strong>

In each round, you will do apply a left circular shift on the key and a permuted choice on the key as shown in below figure:




In the even numbered rounds, the permuted choice will output even digits of the key to the related round. In other words, in rounds 0, 2, 4, 6, and 8, the permuted choice function will output 0, 2, 4, 6, 8, …. 94<sup>th</sup>  bits, which is 48 bits in total. In the other (1,3,5,7,9) rounds,  the permuted choice function will output odd digits, which are 1, 3, 5, 7, 9, …. 95<sup>th</sup>  bits.




<strong>Encryption modes: </strong>

You will implement ECB, CBC, and OFB modes for your encryption algorithm. In case, if CBC or OFB modes are selected, your program should use a vector filled with 1s as the Initialization Vector.







<h1>2                  Usage and testing</h1>

<strong><u>Your program</u></strong><u> <strong>must be named as “BBMcrypt”</strong></u> and should run from the command line with the following parameter format:

BBMcrypt enc|dec -K key -I input -O output –M mode

<ul>

 <li><em>enc|dec</em> specifies the action, which can be either encryption or decryption</li>

 <li>–<em>K key</em> specifies the file name that contains encryption/decryption key, which is encoded in base64 encoding</li>

 <li><em>-I input </em>specifies the input file name, which can be either plaintext or ciphertext <em>-O output </em>specifies the output file name, which can be either plaintext or ciphertext</li>

 <li><em>-M mode </em>specifies the encryption mode, which can be ECB, CBC or OFB.</li>

</ul>

<em> </em>

Your program will be tested on different sized files using the above command line format. <strong><u>Thus, it is important to obey this command line format or otherwise, you will lose</u> <u>points.</u>  </strong>




We will not test wrong parameters of users, such as missing input file name, key file name. However, -K, -I, -O, and -M parameters might be given in different orders on the command line (The first parameter must be always <em>enc|dec</em>).










<h1>3                  Notes</h1>

<ol>

 <li>You can ask questions about the experiment via Piazza group:</li>

</ol>

piazza.com/hacettepe.edu.tr/fall2020/bbm465

<ol start="2">

 <li>Late submission will not be accepted!</li>

 <li>You must compile and run your program on Ubuntu operating system before submission.</li>

 <li>You are going to submit your experiment to online submission system:</li>

</ol>

www.submit.cs.hacettepe.edu.tr




The submission format is given below:




&lt;Group id&gt;.zip

−java/

−−*.java