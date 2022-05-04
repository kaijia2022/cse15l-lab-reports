# Lab Report 2--Week 4
## Bran Zhang

* Bug #1--subString method IndexOutofBoundException
    - Due to [test3-file.md](https://kaijia2022.github.io/markdown-parser/test4-file.md) is a file with one empty line. the int variables `openBracket`, `closeBracket`, `openPran` and `closePran` we get from calling the `indexOf` method are all `-1`, thus when we call the `subString` method, with the start index being `openPran + 1 = -1 + 1 = 0`
    and end index `closePran = -1` , we have the starting index is greater than the ending index, which causes an error. 
    - The Symptom looked something like this:
        ```
        Exception in thread "main" java.lang.StringIndexOutOfBoundsException: begin 0, end -1, length 2
        at java.base/java.lang.String.checkBoundsBeginEnd(String.java:3734)
         at java.base/java.lang.String.substring(String.java:1903)
        at MarkdownParse.getLinks(MarkdownParse.java:21)
        at MarkdownParse.main(MarkdownParse.java:34)
         ```
    - the fix for this bug is to add an additional if-else statement that checks whether 'openPran + 1 <= closePran` and add the subString or break the loop. 

    ![Fix](https://kaijia2022.github.io/cse15l-lab-reports/Bug1%20code%20fix.png)

* Bug #2--Produces the Wrong link
    - Square Brankets and parenthese behind Escape characters within the square brackets like this in [test2-file.md] (https://kaijia2022.github.io/markdown-parser/test3-file.md)causes the code to mistake charaters that don't belong to the link to the output.  
    - The Symptom looked something like this:

        expected output: [https://www.overleaf.com/?gclid=EAIaIQobChMIgsPeyfTU9QIVmR-tBh22xwaZEAAYASAAEgLDOfD_Bw]

        actual output: [ok?](https://www.overleaf.com/?gclid=EAIaIQobChMIgsPeyfTU9QIVmR-tBh22xwaZEAAYASAAEgLDOfD_Bw]
    
    - A fix to this problem would be to check four each of the symbols we find, whether there is an `\` in front of it, if it does, then we will not take that symbol into account.

    ![fix](https://kaijia2022.github.io/cse15l-lab-reports/Bug%202%20code%20fix.png)  

* Bug #3--Infinite loop resulting from broken links
    - [test1-file.md](https://kaijia2022.github.io/markdown-parser/test2-file.md) contains linkes with only Parenthese and two sets of square brackets right next to each other with no links in between. Since there are no square brackets between the two links, during the second iteration in the while loop. We get `openBracket` and `closeBracket` to be both `-1`, which would break the code if we then call 

        ```
        int openBracket = markdown.indexOf("(",closeBracket);
        ```

        Where we start the search from index `-1` again, which would add the first link to the output list again, so we are stucked inside the while loop because we are never able to increment and get to the second link, and in time the computer will run of memory and pop an error message.

    - the Symptom looked something like this:
        ```
        Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
        at java.base/java.lang.StringLatin1.newString(StringLatin1.java:764)
        at java.base/java.lang.String.substring(String.java:1908)
        at MarkdownParse.getLinks(MarkdownParse.java:34)
        at MarkdownParse.main(MarkdownParse.java:60)
        ```
    - The fix to this bug is to check that after we get both `openBracket` and `closeBracket`, if both of these two variables are of value `-1`, then we call `indexOf` method for `openBracket` starting from `currentIndex`, which was incremented in the previous iteration, or `0` if it is the first iteration. This ensures we are moving on in the file and get to every possible link. 

    ![fix](https://kaijia2022.github.io/cse15l-lab-reports/Bug%203%20code%20fixed.png)


