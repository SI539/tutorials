# Setup Git at People Server
# Mac
## Set Up the Git Server
#### Step 1. Connect to the people.si server through SSH
(1) In your terminal, connect to people.si server through SSH.

```
$ ssh your_uniqname@your_uniqname.people.si.umich.edu
```

(2) You will be prompted to enter the password, enter the Kerberos password and enter. While enetering the password, you will see nothing (no * or any indication). It is normal. Just enter your password and press the enter.

---

#### Step 2. Create a folder to be your git-server repository
(1) Type the following command. One line at a time

```
$ mkdir website.git
$ cd website.git
$ git init --bare
```
---

#### Step 3. Hook the git-server repository to the folder actually display the web pages
(1) Remember to change your_uniqname to your actual uniqname

```
$ echo '#!/bin/sh
GIT_WORD_TREE=/home/your_uniqname/public_html git checkout -f' > hooks/post-receive
```

(2) Change the permission of the file we just created.

```
$ chmod +x hooks/post-receive
```

Now everything on the server side is set. You can close the terminal window.

---

## Create a Git Repo on your own computer
* Note: This part of the tutorial assumes you already have git installed on your computer  

(1) Create a folder where you wants to keep all of the files that will be used in your website. You can do it either through Finder or Terminal. In this tutorial, I'll assume you put the folder which is named `website_539` under your home folder.

```
$ mkdir ~/website_539
```

(2) Open your terminal and change directory to the folder you just created.

```
$ cd ~/website_539
```

(3) Initiate a git repo and connect it with the git server

```
$ git init .
$ git remote add origin ssh://your_uniqname@people.si.umich.edu:/home/your_uniqname/website.git
```

(4) Create an `index.html` file and put `Hello World!` in `website_539` folder. You can create it through any text editor, or through terminal

```
$ echo 'Hello World!' > index.html
```

(5) Commit the change we made and push it back to the server. You might be prompted to enter your password again. Enter your Kerberos password.

```
$ git add .
$ git commit -m "init commit"
$ git push origin master
```

(6) Open your browser and enter the URL `your_uniqname.people.si.umich.edu`. You can see the `Hello World!` show up in your browser.




## Generate SSH keys [Optional]The server can recognize the user through the SSH key, so we don’t need to enter our password every time we connect to the server or push new commits to the git server.  
The procedure is similar to the GitHub’s tutorial. The only deference is GitHub handles the server side automatically, but here we need to add the key to the server by ourselves. [GitHub tutorial](https://help.github.com/articles/generating-ssh-keys/)  

---
#### Step 1. Check for SSH Directory
(1) On your personal computer open the terminal and change the directory to ~/.ssh  

```
$ cd ~/.ssh
```  

(2) If the directory does not exist (which is not likely), create one by yourself.  

```
$ mkdir ~/.ssh & cd ~/.ssh
```

(3) You can check for existing SSH keys on your computer

```
$ ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

For example
> id_rsa  
> id_rsa.pub  
> github_rsa  
> github_rsa.pub  



---
#### Step 2. Generate a new SSH key
(1) Within terminal, type the following command. Remember to subsitute in your Uniqname

```
$ ssh-keygen -t rsa -b 4096 -C "your_uniqname"
```

(2) When you're prompted to "Enter a file in which to save the key", name the file as `id_rsa_people_si` and press enter

```
Enter file in which to save the key (/Users/you/.ssh/id_rsa): id_rsa_people_si
```

(3) <a name="passphrase"></a>You'll be asked to enter a passphrase (for safety issue, like a password). You will need to enter the passphrase later.

```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```

---
#### Step 3. Add your key to the ssh-agent
(1) Ensure ssh-agent is enabled:  

```
	# start the ssh-agent in the background
	$ eval "$(ssh-agent -s)"
	Agent pid 59566
```

(2) Add your SSH key to the ssh-agent.

```
	$ ssh-add ~/.ssh/id_rsa_people_si
```
---

#### Step 4. Modify your config file
(1) Type the following command in the terminal window.  
	* Remember to change your_uniqname to your actual uniqname  
	* Remember to have two space in the beginning of each line after second line ( ```Host people.si``` ).

```
$ echo '
Host people.si
  HostName your_uniqname.people.si.umich.edu
  User your_uniqname
  IdentityFile ~/.ssh/id_rsa_people_si' >> config
```
---

#### Step 5. Upload your SSH Key to the server

(1) Type the following command in the terminal  
* Remember to change your_uniqname to your actual uniqname
* Remember to upload the file with `.pub`.

```
$ scp id_rsa_people_is.pub your_uniqname@your_uniqname.people.si.umich.edu:/home/your_uniqname
```

(2) You will be prompted to enter the password, enter the Kerberos password and enter. While enetering the password, you will see nothing (no * or any indication). It is normal. Just enter your password and press the enter.

---

#### Step 6. Setting up the SSH key on people.si server
(1) In your terminal, connect to people.si server through SSH.

```
$ ssh your_uniqname@your_uniqname.people.si.umich.edu
```

(2) You will be prompted to ask enter a password again. Enter your Kerberos password.

(3) Type `ls -la` and see if you can find the `id_rsa_people_si.pub` file you just uploaded

```
$ ls -la

    ...
    drwxr-x---.  3 uniqname mail      4096 Sep 29  2014 etc/
    -rw-r--r--   1 uniqname uniqname   733 Sep  1 17:21 id_rsa_people_si.pub
    drwx------.  2 uniqname uniqname  4096 Sep  1 08:12 logs/
    ...
```

(4) Type the following lines one by one.
* Remember to change your_uniqname to your actual uniqname
* You might be prompted to enter the passphrase. Enter the passphrase you entered in [Step 2-3] (#passphrase)

```
$ mkdir .ssh && chmod 700 .ssh
$ touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
$ cat /home/you_uniqname/id_rsa_people_si.pub >> ~/.ssh/authorized_keys
```

Now we finished setting up the SSH key. Next time you connect to the server with ssh or git from this computer, You don't need to enter the password again.
