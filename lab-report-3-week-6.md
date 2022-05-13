# Lab Report Week 6
## CSE 15L Week 6 -- ssh configure; github access from ieng6; scp -r
### Author: _Bran Zhang_

* **Streamlining ssh Configuration**
    - Screenshot of .ssh/config file:
    ![ssh config](https://kaijia2022.github.io/cse15l-lab-reports/ssh%20configure.png)
        Where the first line is the alias we use for the host and username. I just used ieng6. 
    
    - Screenshot of login using configured alias:
    ![configured login](https://kaijia2022.github.io/cse15l-lab-reports/Configured%20login.png)

    - Scrrenshot of using configured login to copy file:
    ![configured scp](https://kaijia2022.github.io/cse15l-lab-reports/Configured%20scp.png)
        Where I copied a file from my computer to `ieng6` using scp

* **Setup Github Access from ieng6**
    - Screenshot of public key location on github
    ![public key on github](https://kaijia2022.github.io/cse15l-lab-reports/ssh%20key%20on%20github.png)
        Where the first one is the key for my `laptop` to `github`, and the second one is from `ieng6` to `github`
    
    - Screenshot of public and private key location on my ieng6 account
    ![key location on ieng6](https://kaijia2022.github.io/cse15l-lab-reports/public%20and%20private%20key%20location%20on%20ieng6.png)
        Where the `id_rsa` is the private key and the `id_rsa.pub` is the public key
    
    - Screenshot of running git commands to commit and push a change to `github` from `ieng6`
        - first, create a change: I created a new file on `ieng6`
        ![create new file on ieng6](https://kaijia2022.github.io/cse15l-lab-reports/create%20a%20new%20file%20on%20ieng6.png)

        - Then, add, commit and push to `github`
        ![add, commit and push](https://kaijia2022.github.io/cse15l-lab-reports/add%2C%20commit%20and%20push%20to%20github.png)
            Where the `git add` command adds this new file to commit queue, and the `git commit` command commits this change, with `-m` representing the commit message. And finally. `git push` pushes this commit to github.
        
        - a link to the result commit file:
        [commit link] (https://kaijia2022.github.io/cse15l-lab-reports/ieng6SaysHi.txt), which is an empty `.txt` file

* **Copy whole directoriess with scp -r**
    - Screenshot of copying whole directory to ieng6
    ![copying whole dirtectory](https://kaijia2022.github.io/cse15l-lab-reports/copy%20directory%20to%20ieng6.png)
        Where the `-r` command copies recursively and therefore copies every file in the current directory, denote `.` to `ieng6`--the alias we configured for the ieng6.ucsd.edu server.
    
    And it was successful:
    ![successfully copied](https://kaijia2022.github.io/cse15l-lab-reports/successfully%20scp%20-r.png)
    - Screenshot of compiling and running test on ieng6
    ![compile and run test on ieng6](https://kaijia2022.github.io/cse15l-lab-reports/run%20markdownTest%20on%20ieng6.png)
        Where I entered the `markdown-parse` directory, and runned the `Makefile` using `make` command (constructed in lab 6). It checks for changes and compiles the target file and runs it, which in this case is the `markdownParseTest.java`
    - Screenshot of combining the above two steps to one
    ![run is one line 01](https://kaijia2022.github.io/cse15l-lab-reports/Correct%20SCP%20in%20one%20line%2001.png)

        Where the `;` seperates two different commands. The order of execution is:
        copy the directory using `scp -r`; log into ieng6 using configured login `ssh ieng6` and inside the `""` is the argument of the command ssh ieng6. Where we change the directory to `markdown-parse` using `cd` and then compile and run the tests.

     ![run in one line 02](https://kaijia2022.github.io/cse15l-lab-reports/Correct%20SCP%20in%20one%20line%2002.png)

        and it runs successfully!!
    

