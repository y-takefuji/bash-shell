# preprocessing using bash for machine leaning

This repository is for novice programmers how to use terminal commands 
(bash or zsh) for machine learning preprocessing an d data manipulations.
<pre>
commands.pptx.crypted: basic bash commands
keyword.crypted: keywords search basic methods
strength.docx.crpyted: how to make strong statements using data
deduct_induct.pptx.crypted: reasoning for data scientist
twitterEncrypted.docx: twitter search
They were all encrypted. Use openssl command for decrypting.
openssl command can be automatically installed by miniconda.
</pre>


# Exercises for students
<pre>
You should practice the following questions.

0. What is a single character, a string?

1. Show your bash script on how many files and how many directories in the current directory respectively.
Hint: ls command

2. "ls -lt" shows a list of detailed files in time order. Show the list in English instead of in Japanese.

3. Delete blank lines in text
Hint: sed -i '/^$/d'

4. String replace using sed
$ echo 'i am a good boy'|sed 's/good/bad/g'
i am a bad boy

5. Show your script on how many commas in the first line of new_deaths.csv:

https://raw.githubusercontent.com/owid/covid-19-data/master/public/data/jhu/new_deaths.csv

Hints: 
A. $ head -1
B. $ cat file|tr -cd ,
or $ cat file|awk -F ',' '{print NF-1}'
or $ grep -o \, file  
or $ cat file|sed 's/[^,]//g'
C. $ wc -c or wc

6. Show only "Mounted on" column from result of df:
$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
rootfs         233465860 105665500 127800360  46% /
none           233465860 105665500 127800360  46% /dev
none           233465860 105665500 127800360  46% /run
none           233465860 105665500 127800360  46% /run/lock
none           233465860 105665500 127800360  46% /run/shm
none           233465860 105665500 127800360  46% /run/user
tmpfs          233465860 105665500 127800360  46% /sys/fs/cgroup
C:\            233465860 105665500 127800360  46% /mnt/c
Hints: 
A. reduce multiple spaces to a single space per line using "tr -s ' '"
B. cut -d ' ' -f 6

7. Convert minus numbers to positive numbers in csv file.
https://raw.githubusercontent.com/owid/covid-19-data/master/public/data/jhu/new_deaths.csv

8. Explain "history|grep wget"

9. Explain $  ls -d \.[a-z]* |grep /

10. Create a list of unique IPs from /var/log/apache2/access.log
Hints: awk '{print $1}'
or
Hints: cut -d '-' -f 1
delimitter "-d" is a single character.
Hints: awk -F 'XXX' is equivalent to multiple characters as delimitter.

11. How to decrypt keyword.crypted file.
$ openssl enc -d -aes256 -pbkdf2 -in keyword.crypted >keyword.pptx
or
$ openssl enc -d -aes256 -pbkdf2 -in keyword.crypted >keyword.pptx -md sha256

12. How to encode a file
$ openssl enc -e -aes256 -pbkdf2 -in commands.pptx >comm.pptx

13. grep Failed auth.log|cut -d ' ' -f 11|grep  '\.'|sort|uni

14.  cat /var/log/auth.log|grep Failed|awk -F'from' '{print $2}'|cut -d ' ' -f 2|sort|uniq

15. counting the number of unique values
$ cat countries|sort|uniq -c|sort -nr

16. check /var/log/auth.log or /var/log/auth.log.1 and make a table of the number of attacks 
    by country in order of frequency of attacks.
Hints: x.y.z.w is an IP address.
A. python ip2city.py  x.y.z.w
B. whois x.y.z.w
C. curl ipinfo.io/x.y.z.w
D. curl http://ipwhois.app/json/x.y.z.w
E. curl https://ipapi.co/x.y.z.w/json

17. How to silence output in a Bash?
Hint: 2>/dev/null
$ bash country3.sh >ttt 2>/dev/null 

18. Count the number of commas in text.
Hints: 
$ cat text
South Korea,India,Brazil,France,New Zealand,Taiwan,Sweden,Japan,United States,Canada,United Kingdom,Israel
A.
grep -o \, text
wc -l
B.
cat text|tr -cd , 
wc -c
C.
awk -F "," '{print NF-1}' text
D.
sed 's/[^,]//g'
</pre>
E.
<i> i=$(sed 's/,/\n/g' <text|wc -l);((i-=1));echo $i  </i>
<pre>
19. Remove the first 3 lines and the last two lines from text. 
Hint: head and sed command
$ cat text

インターフェイス: 192.168.1.12 --- 0xd
  インターネット アドレス 物理アドレス           種類        
  192.168.1.1           00-25-36-e9-ff-c5     動的
  192.168.1.3           38-78-62-59-75-ad     動的        
  192.168.1.5           00-80-80-8e-92-e9     動的
  192.168.1.8           04-20-9a-42-af-14     動的
  192.168.1.10          00-bb-c1-6b-11-a5     動的
  192.168.1.11          62-db-d1-94-bf-53     動的
  192.168.1.20          ac-5f-3e-5d-9c-5a     動的
  192.168.1.27          60-02-b4-af-03-1e     動的
  192.168.1.30          3c-8d-20-1c-ff-fb     動的
  192.168.1.255         ff-ff-ff-ff-ff-ff     静的
  224.0.0.22            01-00-5e-00-00-16     静的
  255.255.255.255       ff-ff-ff-ff-ff-ff     静的
</pre>
<!-- cat text|head -n -2|sed '1,3d'      -->

# bash shell or zsh

bash or zsh is very important for running a variety of programs. 
You should fill every command described in this list.

<pre>
Operating systems including Windows, Mac, and Linux have a default shell.
WSL (Windows Subsystem for Linux) and Linux (Ubuntu, Debian,...) 
have a default bash shell.
Mac has a default zsh. zsh is similar to bash.

In order to run shell, open terminal on your operating system.
Whenever starting shell, terminal window will be opened with 
the following prompt:
</pre>

<img src='wsl.png' width=260 height=66>
<img src='cygwin.png' width=180 height=80>


# List of minimum commands

We can run any line commands (bash, apt, Python, Firefox,...). 
You must exercise yourself with the following commands. The followings 
are basic bash or zsh commands:

<pre>
apt cache search:

awk: a scripting language used for manipulating data and generating reports
  head -1 new_deaths.csv |awk -F ',' '{print NF-1}'

bc:

cat: to read and concatenate files and give their content as output

cd: to change directory

cmake:

crontab -e: an editor creating cron jobs

cut: a command for cutting out the sections from each line of files 
     and writing the result to standard output
  cut -d ' ' -f 6

df -h: to display information related to file systems about total 
       space and available space

dpkg -l:

echo: to display line of text/string that are passed as an argument

expect:

export DISPLAY=:0: to export a display to remote client

find:

find / -size +100M

find / -size -1G

gcc:

grep -rn "example" . --> search for the word “example” in all
                     text files within the current directory
grep -o "example" file|wc --> how many times of example
grep -v '^#' reinfo.py >rein.py --> remove lines with first
                                    character of #

gzip -d file.gz: expanding .gz file 

hcitool scan:

head -x: reads first x lines of the file
  head -1 new_deaths.csv
  To show the first 10 lines
  head -n 10 
  To show all lines without the last 2 lines
  head -n -2

ifconfig:

iwconfig:

kill -9:

ls: to list files or directories (folders)

make:

mkdir: to make directory

nmap:

nslookup:

ntp:

openssl:

pkill –f xxx:

ps: to provide information about the currently running processes 

pwd: to print working directory

rm:

scp:

sed: stream editor
  sed -n '3,4p' text
  sed '1,$s/  */ /g' text
  To delete the first 3 lines,
  sed '1,3d' text
  sed '/^"""/,/^"""/d' reinforcement_q_learning.py >reinfo.py
    
sort:

source:

split:

split -b 25M large_file  xxx.

ssh:
  ssh -Y
  
sshfs:

sudo apt install:

tar xvf xxx.tar:
  tar cvf xxx.tar dir

top:

touch: to create a file

tr -s : to transform string or delete characters from the string
  echo "my     is  432234" | tr -s ' '
  my is 432234
  echo "my username is 432234" | tr -cd ' a-z'
  my username is 

uniq: to report or filter out repeated lines in a file

unzip:

vi: screen editor 

wc:

wget:

while:

xargs: to read items from standard input as separated by blanks 
       and execute a command once for each argument
</pre>


