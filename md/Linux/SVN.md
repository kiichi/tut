
##SVN

###Starting SVN Server
Starting svn server with /repo local directory and listen port 10100.
-d indicates run as a deamon.
```linux
 ```

Create repository
```linux
 ```
```linux
 ```

###Stop Server
Just Kill the process like
```linux
 ```
```linux
 ```
###Set Authentication
Edit
```linux
 ```
```linux
 anon-access = read
 anon-access = write 
 ```
```linux
 ```
Edit
```linux
 ```
```linux
 ```
###Create a directory
```linux
 ```
###Import (Create project for the first time)
Let's assume you have a sub directory called testprj
```linux
 ```
You should see all inside testprj folder were uploaded.

###Commit (Save your files)
Let's assume you made changes on your program and you want to save them.
Just go to testprj directory and
```linux
 ```
###Checkout (Download the latest project)
Let's assume your co-worker need to download and work on the same project.
In his directory,
```linux
 ```
You need to create another account for him.















