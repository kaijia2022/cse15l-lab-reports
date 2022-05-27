# Lab Report 4 Week 8
## CSE 15L Week 8 -- Running Junit tests On markdown-parsers and Debugging
### Author: _Bran Zhang_

* **link to my markdown-parser page**: [my markdown-parser](https://github.com/kaijia2022/markdown-parser)

* **link to the markdown-parser page I reviewed**: [reviewed parser](https://github.com/cmy0357/markdown-parser)

* **Junit test Code I wrote for the three test files**
    - Code Snippet 1: 
    ![test method 1](https://kaijia2022.github.io/cse15l-lab-reports/fixed%20test%201%20expected%20output.png)
        
        - expected output: [url.com, `google.com, goole.com, ucsd.edu]

    - Code Snippet 2:
    ![test method 2](https://kaijia2022.github.io/cse15l-lab-reports/test-method-2.png)

        - expected output: [a.com, b.com, a.com(()), example.com]

    - Code Snippet 3:
    ![test method 3](https://kaijia2022.github.io/cse15l-lab-reports/test-method-3.png)

        - expected output: [https://www.twitter.com, https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/scheduleb.com, github.com, https://cse.ucsd.edu/]


* **Output running my markdown-parser**
    - Test Method 1: `FAILED`
        -failier message:
        ![failing feedback](https://kaijia2022.github.io/cse15l-lab-reports/test%201%20fail%20on%20my%20parser.png)

    - Test Method 2: `FAILED`
        -failer message:
        ![failing feedback](https://kaijia2022.github.io/cse15l-lab-reports/test-method-2-failed(my%20parser).png)

    - Test Method 3: `FAILED`
        - failer message:
        ![failing feedback](https://kaijia2022.github.io/cse15l-lab-reports/test-method-3-failed%20(my%20parser).png)


* **Output running reviewed markdwon-parser**
    - Test Method 1: `FAILED`
        -failier message:
        ![failing feedback](https://kaijia2022.github.io/cse15l-lab-reports/test%201%20fail%20on%20reviewed%20parser.png)

    - Test Method 2: `FAILED`
     - failer message:
        ![failing feedback](https://kaijia2022.github.io/cse15l-lab-reports/test-method-2-failed(reviewed%20parser).png)
    
    - Test Method 3: `FAILED`
     - failer message:
        ![failing feedback](https://kaijia2022.github.io/cse15l-lab-reports/test-method-3-failed(reviewed%20parser).png)


* **Questions**
    - for the `backticks` :
        - initially I thought all links inside paranthesis should be in the expected output, it is only now that I know only those in blue in the preview are valid links. The fix for this is simple though. 

        - Case 1: check whether there is a backtick before the `openbracket` and a backtick in between `openbracket` and `closebracket`

        - Case 2: check whether there is a backtick before the `closebracket` and a backtick in between `closebracket` and `openparen`

        - if either of the above case satisfies, set `currentIndex` to `closebracket + 1` and use `continue` to go straight to the next iteration. 

        - wrap the above into a helper method, and call it right after we get the `openbracket` and `closebracket` indices. 

        - given the above steps, I am pretty sure they can be done in less than 1o lines of code change.

    - for the `nested parenetheses`, `nested brackets`, and `escaped brackets`: 
        - My original code takes account for all escaped characters. So what I need to fix is to take into account links that have `nested parenetheses` or `nested brackets`. However, it is not possible, at least for my implementation, to change less than 10 lines to fix this feature. 

        - Below are the codes I added to take into account `nested parenetheses` and `nested brackets`. 

        ![fixed code 1](https://kaijia2022.github.io/cse15l-lab-reports/fix%20nested%20parens%26bracks2.png)

        - In the above Image, I added two helper methods `isNestedLink` and `getOuterParen`, to help me determine wheter there is a `nested link` and whether there are `nested parenthesis`. These two methods already took over ten lines. 

        ![fixed code 2](https://kaijia2022.github.io/cse15l-lab-reports/fix%20nested%20parens%26bracks3.png)

        - Then in the above image, I also wrote the helper method `beforeNewLine` to help me determine wheter a parenthesis is at the end of the line. Not accounting the `print statements` I used to debug the code, this added 4 more lines. 

        ![fixed code 3](https://kaijia2022.github.io/cse15l-lab-reports/fix%20nested%20parens%26bracks.png)
        
        - This image above shows how I actually used these methods in my `parser method`. And besides the outer `if` statement. All below I lines I added. (`Note: the argument I passed into the toReturn.add method is actually change for fixing newLines and spaces introduced in the third test file`)

        - In total, I took about `25` lines of changes for fixing the `nested brackets and parenthesis` problem

    - for the `newLines in brackets and parenthesis` issue
        - for this one, I actually was able to fix it with less than 10 lines of change in my code.

        ![fixed code](https://kaijia2022.github.io/cse15l-lab-reports/fixs%20space%20and%20newline.png)

        - in the above picture, I added the helper method `trimSpaces`, which is called every time I add a new link to the `toReturn` arrayList. It removes all `spaces` and `new line characters` after the `openParen` and before the `closeParen`. This helper method takes 3 additional lines. 

        - And as I noted above, calling this helper method in my main parse algorithm takes another `2` lines. So I was able to fix this within 10 lines. 

        - **HOWEVER, `my fixed code do not work accumulatively, which means if a link has both spaces before the closeParen and have nested parenthesis, it might break`, AND `my code does not fix every bugs raised by the third test file--it does not take into account links that has only one paranthesis as a seperate link`** 


    