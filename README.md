# CentOS: Extract Usernames from System Log File

## Project Description:
Please refer to [auth.log](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/82c1e41c368e33595ced06e7b78a6202efb14446/Example_Logs/auth.log) within the [Example_Logs folder](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/tree/main/Example_Logs). 
Attackers can brute force into computers by attempting to log in remotely with randomly generated usernames or with usernames that are commonly used by popular services. These activities can be monitored, captured, and recorded with logging services like the system log. 

## Project Scope:
* To extract the [auth.log file](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/82c1e41c368e33595ced06e7b78a6202efb14446/Example_Logs/auth.log) from the [log.tar.gz file](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/82c1e41c368e33595ced06e7b78a6202efb14446/Example_Logs/log.tar.gz).
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

## Project result with different solutions:
The following files are located in the [Example_Logs folder](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/tree/main/Example_Logs).
* [usernames.txt](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/82c1e41c368e33595ced06e7b78a6202efb14446/Example_Logs/usernames.txt)
* [solution.txt](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/82c1e41c368e33595ced06e7b78a6202efb14446/Example_Logs/solution.txt) 
