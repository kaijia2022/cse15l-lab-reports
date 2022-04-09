# Lab Report Week 1
## CSE 15L Week 1 Tutorial--Connect to the _ieng6_ Server
### Author: _Bran Zhang_

* **Step 1**: 
    - Install the [VScode](https://code.visualstudio.com/Download) that corresponds to your PC operating system and set it up on your PC.

![VScode]()

* **Step 2**: 
    - Open VScode, on the top tool box, look for terminal
    - Place your Cursor on terminal, a dropdown menu will appear. Click  _New Termial_. Now a new terminal will appear on your screen.

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

        [a screenshot of my first login]()

     - Now you are in the terminal of the ieng6 remote server. We can use [Unix Commands](https://en.wikipedia.org/wiki/List_of_Unix_commands) to play with this server computer. 

        for example: type the command `pwd`, which stands for "**print working direction**", and you will get something like this:

        [pwd]()

        Now try `ls`, which stands for "**list**" and all the files in the current directory will be returned. It looks something like this, though the files in your directory might differ from mine.

        [ls]()

        Mess around with some other commands yourself. When you are done, type `exit` to quit the server computer.
    
* **Step 4**
    - Now we have successfully logged into **ieng6** server, our next goal is to copy files from our local computer to the ieng6 server. To achieve this, we need to use the `scp` command, or "**secure copy**" command.

    - In your local work folder, create a new `.txt` file and change the extention to `.java`, then open it for edit in VSCode. 

        for example, I created a new java class called HowDoYouDo.java, inside this class, there is a main method that prints "**How Do You Do, ieng6?**".

        [HowDoYouDo.java]()

    - Now, open Command Prompt or open another terminal in VScode, use the `cd` or "**change directory**" command and go to the folder where `HowDoYouDo.java` resides,  type the following Command and enter your password: 

        `$ scp HowDoYOuDo.java cs15lsp22zz@ieng6.ucsd.edu:~/`

        where again, replace `zz` by your own username, and `~` means the home directory of the user, and `/` means its root directory, so together, they represent your root director on the ieng6 server computer.

        [scp]()
    
    - Log back into ieng6 server computer as you did in step 2, and try the `ls` command again:

        [lst again]()

        and you see `HowDoYouDo.java` is added in here.
    
    - Lets try compile and run this file on the ieng6 server computer using `javac` and `java`:

        [run HowDoYouDo.java]()

* **Step 5**
    
    Every time we want to log into ieng6, we need to enter our password








    
    


