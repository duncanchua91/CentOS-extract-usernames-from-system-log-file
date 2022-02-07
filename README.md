# CentOS: Extract Usernames from System Log File

## Project Description:
Please refer to auth.log within the Example_Logs folder. 
Attackers can brute force into computers by attempting to log in remotely with randomly generated usernames or with usernames that are commonly used by popular services. These activities can be monitored, captured, and recorded with logging services like the system log. 

## Project Scope:
* To extract the auth.log file from the log.tar.gz file.
* Search for unauthorized connection attempts
* Extract the usernames that the attacker(s) tried to use.
* Organize the extracted usernames, and then print it to a file for review.

## CentOS commands:
* tar
* cat
* vim
* nano
* grep -A | grep -v | grep -oP
* sort -u
* awk '{print $9}'

## Project result
The following files are located in the Example_Logs folder:
* file1
* file2
