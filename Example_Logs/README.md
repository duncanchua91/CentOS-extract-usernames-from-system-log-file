# Project Approach
Step by step procedures to produce project results, which is to extract usernames that attackers used to establish unauthorized connections to gain remote access into the computers. 

## Project Approach 1 = [usernames.txt](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/10600a3687713e2b0058bb235cd4fb20d1a25072/Example_Logs/usernames.txt)
This is approach reflects my attempt to the project.
* Step 1: extract the log.tar.gz file, which contains the auth.log file.
  *  CentOS Command: tar xf log.tar.gz

* Step 2: **review the log file** to find any common patterns from the unauthorized connection attempts e.g. "POSSIBLE BREAK-IN ATTEMPT !" followed by the unauthorized username.
  * CentOS Command: cat auth.log OR vim auth.log OR nanos auth.log OR head auth.log OR tail auth.log OR less auth.log

* Step 3: Noticed that the username is usually located 1 sentence below the "POSSIBLE BREAK-IN ATTEMPT !" key word. The username is usually **"user=spring"** or "... **Invalid user spring** from 172.20.1.6".

* Step 4: Only grep the attacker's username from failed connection attempts.
  * CentOS Command: grep -A 1 "POSSIBLE" auth.log | grep -v "POSSIBLE" | grep -oP "user\s+\K\w+" auth.log | sort -u > usernames.txt

    * grep -A 1 "POSSIBLE" auth.log <-- print the lines that contain "POSSIBLE BREAK-IN ATTEMPT" and the 1 line below it, which contain usernames(see step 3).

    * grep -v "POSSIBLE" <-- inverse grep, which removes the lines that contain "POSSIBLE BREAK-IN ATTEMPT", and only print the line with usernames.

    * grep -oP "user\s+\K\w+" auth.log <-- using Perl Regular Expression (Regex) within the " " to only return usernames (see Step 5 for explanation of the Regex syntax. 

    * sort -u > usernames.txt <-- to print out usernames in alphabetical order, and the -u flag means unique values only (remove duplicate). 

* Step 5: grep -oP "user\s+\K\w+" auth.log <-- in detail
  * using grep **-o** flag to print only **"user"** part of the line.
  * using **-P** flag which is **perl-regexp**.
  * using **\s+** to match and capture any number (1 or more) of non-space characters followed by a space character to get the username. 
  * using **\K** flag will tell the engine to pretend that match attempt started at the position e.g. **user spring** which will **only print** the **spring**.
  * using **\w+** flag is used to match a word character that is **alphanumeric**, e.g. **=** of the **user=spring**.

## Project Approach 2 = [solution.txt](https://github.com/duncanchua91/CentOS-extract-usernames-from-system-log-file/blob/10600a3687713e2b0058bb235cd4fb20d1a25072/Example_Logs/solution.txt)
This approach is the actual solution provided by the LinkedIn Course Instructor, Scott Simpson. 
Reference: [Learning Linux Command Line](https://www.linkedin.com/learning/learning-linux-command-line-14447912/learning-linux-command-line?autoAdvance=true&autoSkip=false&autoplay=true&resume=true&u=36492188)
* Step 1: extract the log.tar.gz file, which contains the auth.log file.
  *  CentOS Command: tar xf log.tar.gz

* Step 2: **review the log file** to find any common patterns from the unauthorized connection attempts e.g. "POSSIBLE BREAK-IN ATTEMPT !" followed by the unauthorized username.
  * CentOS Command: cat auth.log OR vim auth.log OR nanos auth.log OR head auth.log OR tail auth.log OR less auth.log
  * Lines that contain string "input_userauth_request" indicates attacker's attempt to remote login with username.

* Step 3: cat auth.log | grep "input_userauth_request" | awk '{print $9}'
  * **cat** command to view the auth.log file 
  * **grep** to match string with "input_userauth_request"
  * **awk** to only return the 9th column item, which is the username.  
