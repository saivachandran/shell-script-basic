# shell script

sequence of system commands pasted in single file and executed it's called shell script.

vim script1.sh

#!/bin/bash

ls
pwd
date

# chmod a+x script1.sh

./script1.sh 
script1.sh
1  install-redis.sh  passwd.txt  python-tut  script1.sh  snap
/root
Sat Sep  4 05:36:52 UTC 2021


export PATH=$PATH:$(pwd)


echo $PATH

/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/root


# run script on any folder

cd /tmp


script1.sh

script1.sh 
snap.lxd
systemd-private-e5ee3cb61a514c14a45b26b8b5015c76-apache2.service-cgrf5h
systemd-private-e5ee3cb61a514c14a45b26b8b5015c76-redis-sentinel.service-kyg7Re
systemd-private-e5ee3cb61a514c14a45b26b8b5015c76-systemd-logind.service-yzk1Og
systemd-private-e5ee3cb61a514c14a45b26b8b5015c76-systemd-resolved.service-zO5sbf
systemd-private-e5ee3cb61a514c14a45b26b8b5015c76-systemd-timesyncd.service-Hf6ZQe
/tmp


# we have assign variable in 3 ways in script

Explicit defintion var=value

Read command read VAR

command substitution VAR $(pwd)

when we assign variable in bash we can't have space 


# variables in shell script


vim var.sh

#!/bin/sh
MY_MESSAGE="Hello World"
echo $MY_MESSAGE

./var.sh

Hello World

# We can interactively set variable names using the read command; the following script asks you for your name then greets you personally:

var2.sh

#!/bin/sh
echo What is your name?
read MY_NAME
echo "Hello $MY_NAME - hope you're well."

./var2.sh



vim var3.sh

#!/bin/sh
echo "What is your name?"
read USER_NAME
echo "Hello $USER_NAME"
echo "I will create you a file called ${USER_NAME}_file"
touch "${USER_NAME}_file"

./var3.sh 
What is your name?
daksha
Hello daksha
I will create you a file called daksha_file


cat read.sh 

#!/bin/bash

echo -n Enter Your name:

read Name

echo -n Enter Your age:

read Age


echo ==== Employ Details ====


echo Name: $Name

echo Age: $Age


root@ip-172-31-86-0:~# ./read.sh 
Enter Your name:saiva
Enter Your age:31
==== Employ Details ====
Name: saiva
Age: 31


# read file in shell script with hidden password

cat read2.sh 
#!/bin/bash

read -p "Your Name:" NAME

read -sp "Your Age" AGE

echo "Name: $NAME, Age: $AGE "



 ./read2.sh 

Your Name:saiva
Your AgeName: saiva, Age: 31 


cat read_from_file.sh 

#!/bin/bash

read HOSTNAME < /etc/hostname

echo Hostname: $HOSTNAME


 ./read_from_file.sh 

Hostname: ip-172-31-86-0



# command subsitution and time management

cat command_sub.sh 
#!/bin/bash

CURRENT_DIRECTORY=$(pwd)

echo "Script run from" $CURRENT_DIRECTORY


./command_sub.sh 
Script run from /root



cat time.sh 
#!/bin/bash

# start time measurement from here

START=$(date +%s)

CURRENT_DIRECTORY=$(pwd)

sleep 2

END=$(date +%s)

# End time measurement

DIFFERNECE=$(( END - START ))

echo 

echo Time elapsed: $DIFFERNECE seconds.

./time.sh 

Time elapsed: 2 seconds.


# argument

cat argument.sh 
#!/bin/bash

echo "Script name: $0"

echo "First argument: $1"

echo "Second argument: $2"

echo "All arguments with \$@: $@"

echo "All arguments with \$*"


./argument.sh 
Script name: ./argument.sh
First argument: 
Second argument: 
All arguments with $@: 
All arguments with $*


# Redirection and piping
------------------------

STDIN(0) standard input

STDOUT(1) standard output

STDERR(2) standard error


# create multiple file
----------------------

for i in {1..30}; do touch file$i.txt; done

# list file range
--------------

ls file[1-9].txt


# check file exist or not
-------------------------

cat exist.sh 

#!/bin/bash

if [ -f read.sh ]; then 
	
  echo exists

else
    echo does not exist

fi


./exist.sh 
exists


[ -f read.sh ] && echo exists
exists


cat if.sh 

#!/bin/bash

echo -n Enter age:

read AGE

[ $AGE -lt 20 ] && { echo your not allowed; exit 1; } || echo welcome

./if.sh 

Enter age:25
welcome


./if.sh 
Enter age:12
your not allowed



#shell script awk command
-------------------------

awk  '{print $3}' table

dept

IT
admin
Hr
dev


awk  '{print $1 " " $3}' table

name dept
 
sai IT
hassan admin
krish Hr
vijay dev


#awk serarch pattern print
---------------------------

cat table  | awk '/hassan/ {print $1 " " $3}'
hassan admin


cat table  | awk '/sai/ {print $1 " " $3}'
sai IT

cat table  | awk '/admin/ {print $1 " " $3}'
hassan admin


cat table | awk '!/name/ {print $0 } ' 

sai      31    IT
hassan   40    admin
krish    35     Hr
vijay    29     dev 

cat table | awk '!/name/ {print $0 } '  | awk '/IT/ {print $0}'
sai      31    IT


# print line in awk
--------------------

 cat table | awk '$1 == "sai"'
sai      31    IT

cat table | awk '$1 != "name"'

sai      31    IT
hassan   40    admin
krish    35     Hr
vijay    29     dev 

# Number of fields
------------------

cat table | awk '{print NF}'
3
0
3
3
3
3


# Number of records
-------------------

cat table | awk '{print NR}'
1
2
3
4
5
6

# field seperator
-----------------

cat /etc/passwd | awk 'BEGIN{FS=":"} {print $1 " " $7}'





