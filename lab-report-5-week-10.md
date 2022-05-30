# Lab Report 5 Week 10
## CSE 15L Week 10 -- vimdiff, compare testfiles and debugging
### Author: _Bran Zhang_

- How I compared the test results?

  - on ieng6, I runned the bash script [script.sh] on both markdown repositories. I used output redirection `>` to redirect the output for both repos to two files `results.txt` within both repos' directory respectively. Then I used `vimdiff` to compare the results. 

- Links for two test files.

  - [test-files/495.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/495.md)

  - [test-files/516.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/516.md)

- for both outputs, my implementation produced the wrong one, while the given parser produces the expected output. 

- actual outputs, in vimdiff

    - ![495.md](https://kaijia2022.github.io/cse15l-lab-reports/vimdiff%20testfile-495.png)

    - ![516.md](https://kaijia2022.github.io/cse15l-lab-reports/vimdiff%20testfile-516.png)

- Where for testfile 495, the expected output is `foo(and(bar))`, and for testfile 516, the expected output is `moon.jpg`

- Symptom & bugs 

  - for my output for `495.md` , the symtom is obviously that I neglected two close parentheses at the end. In my code, I do have a method called `getOuterParen` defined:
  ![the method]()
  however, it is only called in `getLinks` whenever there is a `nested linked`. 
  ![where it is called]()

  So to fix the bug, all I have to do is to call it to make sure we get all the parentheses even if there is no `nested linked`.
