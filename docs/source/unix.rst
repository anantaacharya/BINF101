############
Introduction to Unix
############

Learning Objectives
With the things covered in class today, you will be able to:

* Log into a Unix machine remotely
* Create directory, files and move files around directory
* Download files from internet
* Use command line programs to inspect and manipulate files
* download/upload files using winscp



Log into a Unix machine remotely
---------------------------------

Login to cloud using putty:

you should see after you login

``(base) bioinfo@afurampur:~$``

know where you are

``pwd``

list files and directories

``ls``
``ls -l``

go to students directory

``cd students``
``pwd``


Create directory, files and move files around directory
--------------------------------------------------------
create directory of you name

``mkdir <yourname>``

go to your directory

``cd <yourname>``

``pwd``

go one step up

``cd ..``

go to home (/home/bioinfo)


``cd ~``

Go back to your directory

``cd /students/<yourname>``

Create a file

``echo "Hello People">myfirstfile.txt``

Explore more

``mv

cp

rm

rmdir

cat``

Download files from internet
-------------------------------

``wget https://molb7621.github.io/workshop/_downloads/SP1.fq``

``curl https://molb7621.github.io/workshop/_downloads/sample.fa>test.sample1.fa``

Use command line programs to inspect and manipulate files

relavant commands:
``head

tail

wc

wc -l

grep

uniq``


download/upload files using winscp
-----------------------------------
Login to winscp as documented. We will demo on how to move around


