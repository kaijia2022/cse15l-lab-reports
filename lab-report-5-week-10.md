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
    ![the method](https://kaijia2022.github.io/cse15l-lab-reports/getOuterParen.png)
  - however, it is only called in `getLinks` whenever there is a `nested linked`. 
    ![where it is called](https://kaijia2022.github.io/cse15l-lab-reports/Where%20the%20method%20is%20called.png)

  -where as for a regular link, it does not call the `getOuterParen` method.
    ![regular link](https://kaijia2022.github.io/cse15l-lab-reports/Inner%20link.png)

  - So to fix the bug, all I have to do is to call it to make sure we get all the parentheses even if there are no `nested linked`.

  - for my output for `516.md`, the symptom is that my code included both the inner linkk `moon.jpg` and the outer link `/uri` for the testfile containing the line `[![moon](moon.jpg)](/uri)`, in the preview, we know that the expected should only be `moon.jpg`. In fact, I did this on purpose when I first tried to solve the nested link problem, bbcause back then I thought we ought to parse all links inside a parenthesis. 

  - looking at the part of my code that adds the link:
    ![adds the link](https://kaijia2022.github.io/cse15l-lab-reports/code%20that%20adds%20links%20to%20output.png)

  - The method in the first if statement checks if there is a square bracket between `closeParen` and the next newLine characeter `/n`, so this if statement basically adds the link inside the parenthesis inside the square bracket. 

  - the else statement simply adds the link, if the `if` condition is not satisfied. 

  - the next `if` statement checks for link outside the outer close bracket, or the outer link. However, as we can see in the markdown preview, if there is an inner link, the other link should not be included. Therefore, we can simply delete this last `if` clause to fix the bug.




  

