# Lab Report Week 1
## CSE 15L Week 1 Tutorial--Connect to the _ieng6_ Server
### Author: _Bran Zhang_

* **Step 1**: 
    - Install the [VScode](https://code.visualstudio.com/Download) that corresponds to your PC operating system and set it up on your PC.

    ![VScode](https://kaijia2022.github.io/cse15l-lab-reports/VScode%20official%20website.png)

* **Step 2**: 
    - Open VScode, on the top tool box, look for terminal
    - Place your Cursor on terminal, a dropdown menu will appear. Click  _New Termial_. Now a new terminal will appear on your screen.

    ![new terminal](https://kaijia2022.github.io/cse15l-lab-reports/open_terminal.png)

    ![new terminal](https://kaijia2022.github.io/cse15l-lab-reports/New%20Terminal.png)

    - Now, before you do anything in the new terminal,if you are a Windows user, go to Settings -> apps -> applicable features and check if you have OpenSSH Client service installed. If not, google it and download. OpenSSH is the protocal we use to connect from our PC to a remote server.

* **Step 3**:
     - Get your ieng6 account information from https://sdacs.ucsd.edu/~icc/index.php. and go back to the new Terminal you just invoked. Enter the following command:

         `$ SSH cs15lsp22zz@ieng6.ucsd.edu`
         
         with **zz** replaced by your specific accord name, for example: my account is **cs15lsp22ahr@ieng6.ucsd.edu**, with **zz** replaced by **ahr**

     - Hit `ENTER` to execute. Since this is the first time you log in, you might get something like below:

        ```
        The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
        RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
         Are you sure you want to continue connecting (yes/no/[fingerprint])?
         ```
     - Type `yes` and hit `ENTER` and you will see the following: 

        ![a screenshot of my first login](https://kaijia2022.github.io/cse15l-lab-reports/SSH.png)

     - Now you are in the terminal of the ieng6 remote server. We can use [Unix Commands](https://en.wikipedia.org/wiki/List_of_Unix_commands) to play with this server computer. 

        for example: type the command `pwd`, which stands for "**print working direction**", and you will get something like this:

        ![pwd](https://kaijia2022.github.io/cse15l-lab-reports/PWD%20command.png)

        Now try `ls`, which stands for "**list**" and all the files in the current directory will be returned. It looks something like this, though the files in your directory might differ from mine.

        ![ls](https://kaijia2022.github.io/cse15l-lab-reports/ls.png)

        Mess around with some other commands yourself. When you are done, type `exit` to quit the server computer.
    
* **Step 4**
    - Now we have successfully logged into **ieng6** server, our next goal is to copy files from our local computer to the ieng6 server. To achieve this, we need to use the `scp` command, or "**secure copy**" command.

    - In your local work folder, create a new `.txt` file and change the extention to `.java`, then open it for edit in VSCode. 

        for example, I created a new java class called HowDoYouDo.java, inside this class, there is a main method that prints "**How Do You Do, ieng6?**".

        ![HowDoYouDo.java](https://kaijia2022.github.io/cse15l-lab-reports/HowDoYouDo.png)

    - Now, open Command Prompt or open another terminal in VScode, use the `cd` or "**change directory**" command and go to the folder where `HowDoYouDo.java` resides,  type the following Command and enter your password: 

        `$ scp HowDoYOuDo.java cs15lsp22zz@ieng6.ucsd.edu:~/`

        where again, replace `zz` by your own username, and `~` means the home directory of the user, and `/` means its root directory, so together, they represent your root director on the ieng6 server computer.

        ![scp](https://kaijia2022.github.io/cse15l-lab-reports/scp.png)
    
    - Log back into ieng6 server computer as you did in step 2, and try the `ls` command again:

        ![lst again](https://kaijia2022.github.io/cse15l-lab-reports/ls%20again.png)

        and you see `HowDoYouDo.java` is added in here.
    
    - Lets try compile and run this file on the ieng6 server computer using `javac` and `java`:

        ![run HowDoYouDo.java](https://kaijia2022.github.io/cse15l-lab-reports/runHowDoYouDo.png)

* **Step 5**
    
    Every time we want to log into ieng6, we need to enter our password, luckily, there is a short cut, we can set up a pair of keys--a public key on the ieng6 computer and a private key on our local PC. And all these is done by a single command: `ssh-keygen`:
    
    - Type the command

        $ `ssh-keygen` 
    
        on your client computer, and your should expect something like this below:

        ```
        # on client (your computer)
        $ ssh-keygen
        Generating public/private rsa key pair.
        Enter file in which to save the key (/Users/<user-name>/.ssh/id_rsa): /Users/<user-name>/.ssh/id_rsa
        Enter passphrase (empty for no passphrase): 
        ```
        **Make sure you do not enter any phrase on this line, just hit `ENTER`.**
        ```
        Enter same passphrase again: 
        Your identification has been saved in /Users/<user-name>/.ssh/id_rsa.
        Your public key has been saved in /Users/<user-name>/.ssh/id_rsa.pub.
        The key fingerprint is:
        SHA256:jZaZH6fI8E2I1D35hnvGeBePQ4ELOf2Ge+G0XknoXp0 <user-name>@<system>.local
        The key's randomart image is:
        +---[RSA 3072]----+
        |                 |
        |       . . + .   |
        |      . . B o .  |
        |     . . B * +.. |
        |      o S = *.B. |
        |       = = O.*.*+|
        |        + * *.BE+|
        |           +.+.o |
        |             ..  |
        +----[SHA256]-----+
        ```

    - Now, log back into **ieng6** and type the following  command:

        `$ mkdir .ssh`

        which makes a directory to store .ssh to store the public key on your user account on the ieng6 server.

    - Back to your local PC, use scp to copy that public key to ieng6:

        `$ scp /Users/<user-name>/.ssh/id_rsa.pub cs15lsp22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys`

    Now, try to log back into ieng6 or do a scp command:

    [login without password]()

    and you don't need to enter your password anymore! yeahhhh!.

* **Step 6**
    With the skills we learnt so far, lets see how we can optimize the procedure of: `Modify -- Copy to Server -- Run on Server` process.

    - make change on the HowDoYouDo.java file in CScode IDE.

    ![make change](https://kaijia2022.github.io/cse15l-lab-reports/Change%20HowDoYouDo.png)

    - use `scp` to copy it to the server, this time without the need to enter password.

    ![scp again with no password](https://kaijia2022.github.io/cse15l-lab-reports/SCP%20again.png)

    - use `ssh cs15lsp22zz@ieng6.ucsd.edu "ls"` to login and list and exit the files in one line of command.

    ![login, list and exit](https://kaijia2022.github.io/cse15l-lab-reports/login,lst,exit.png)

    - run multiple commands on one line with `;` semicolons to seperate each command.

    ![use one line to execute HowDoYouDo.java on ieng6 and exit](https://kaijia2022.github.io/cse15l-lab-reports/login,compile,run,exit.png)

With all these six steps, you have successfully mastered connect and file transfer between your PC and the ieng6 server. WHooohooooooo!!!!!!!!














    
    


