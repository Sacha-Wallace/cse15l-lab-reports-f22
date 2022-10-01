**How to Use Your Course Specific Account on ieng6**

1. **Installing VSCode**

First off we'll need a text editor. Click on [this](https://code.visualstudio.com/) link to download VSCode.

Follow the instructions on the website, and eventually you should end up with a screen similar to this.

![VSCodePhoto](https://github.com/Sacha-Wallace/cse15l-lab-reports-f22/blob/main/VSCodePhoto.png)

2. **Remotely Connecting**

First off, open the terminal on your operating system and type in the following command. Replace the asterisks with your course specific login.

`$ ssh cs15l*****@ieng6.ucsd.edu`

There may be a message if its your first time connecting, you will just have to press enter. You should see an output similar to this, depicting a successful connection.

![RemoteConnectionPhoto](https://github.com/Sacha-Wallace/cse15l-lab-reports-f22/blob/main/RemoteConnectionPhoto.png)

3. **Trying Some Commands**

[This](https://www.guru99.com/linux-commands-cheat-sheet.html) is a list of common terminal commands:



Here you can see I created a folder with my name on the account with mkdir, and then changed directories into it with cd. I used mkdir again to create another folder, and used cd to navigate into it. Finally I used the pwd command, which prints out your current path of directories.

![SomeCommandsPhoto](https://github.com/Sacha-Wallace/cse15l-lab-reports-f22/blob/main/SomeCommandsPhoto.png)

4. **Moving Files With scp**

The scp command takes three arguments and copies a file from a client to a remote host. 

Make sure you are logged out of the server, and then you can use the command by filling in the arguments denoted by asterisks.

`$ scp *FileName* cs15l*****@ieng6.ucsd.edu:*NewFilePath*`

It will request your password, and then notify you that the copy has been completed.

The output should look similar to this:

![SCPCompletedPhoto](https://github.com/Sacha-Wallace/cse15l-lab-reports-f22/blob/main/SCPPhoto.png)

5. **Setting an SSH Key**

By creating an SSH key, you will save countless time spent inputting your password any time you want to sign in or copy a file. 

On the client type in:

`$ ssh-keygen`

When prompted about the file location, hit enter to keep it in the default directory. After it will ask for a passphrase, just hit enter again to skip it. 

You should see multiple lines of output, some including the key's map like this:

![SSHKeygenPhoto](https://github.com/Sacha-Wallace/cse15l-lab-reports-f22/blob/main/SSHKeygenPhoto.png)

Using the following commands, log onto the server and create a folder for the public key. Then use the scp command to copy the key.

```
$ ssh cs15l*****@ieng6.ucsd.edu

$ mkdir .ssh

$ exit

$ scp /Users/*Username*/.ssh/id_rsa.pub cs15l*****@ieng6.ucsd.edu:~/.ssh/authorized_keys
```

You are now able to connect to the remote server without having to enter your password. 

6. **Optimizing Remote Running**

To make your workflow even more efficient, here are two syntax tricks.

Adding a semicolon on a line between statements will allow multiple statements to run per line. 

In addition, you can use the ssh command with a statement surrounded by quotes at the end. It will run the statement on the server without being logged in.

![TricksPhoto](https://github.com/Sacha-Wallace/cse15l-lab-reports-f22/blob/main/TricksPhoto.png)