our target ip was : 10.130.145.49
the questions they gave us to answer : 
	1. scan and find open ports.
	2. Who wrote the task list?
	3. What service can you bruteforce with the text file found?
	4. What is the users password?
	5. user flag user.txt.
	6. root flag root.txt.

so i run nmap to see the open ports.

![](../images/2026-06-12_16-07.png)

so in the result we see http port open that means there is a website so when i see it.

![](../images/2026-06-12_16-34.png)

it didn't have much it just a conservation, but THM give us hint to go to the ftp service in anonymous.

![](../images/2026-06-12_16-38.png)
 
and in the name part you can write "ftp" or "anonymous" i used "ftp" but two of them work.

![](../images/2026-06-12_16-43.png)

now when i ls i see 2 file called "locks.txt" & "task.txt".

![](../images/2026-06-12_16-45.png)

and used get command to download them and they will be downloaded to the current directory you are in.

![](../images/2026-06-12_16-48.png)

when i see inside the locks.txt file it look like worklist/payload for password & keep it for later.

![](../images/2026-06-12_16-50.png)

and the task.txt have like instructions and the writer was "lin" so we got our 2nd question answer.
so now b/c post 22 or ssh is open we can brute force by that and also that was the 3rd question answer.

![](../images/2026-06-12_17-14.png)
the command used is this : 
```bash
hydra -l lin -P locks.txt 10.130.145.49 ssh
```

used hydra tool to brute force and the username is "lin" the writer and used the wordlist "locks.txt" we downloaded from the ftp server and got the passwd also that was the 4th question answer.

![](../images/2026-06-12_17-23.png)
we successfully login with those credentials.  
when i ls inside /Desktop directory.

![](../images/2026-06-12_17-25.png)
i got file named "user.txt" and inside that i got the  5th question & user flag.
to privilege escalate first i serach what can i run using sudo power using this command : `sudo -l`

![](../images/2026-06-12_17-50.png)

and i can tar command using sudo privilege so search how to privilege escalate using tar command and this command to execute :  
```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

so i executed the command.

![](../images/2026-06-12_17-57.png)

and now we got the root user.
when i go to the /root directory and ls there.

![](../images/2026-06-12_17-59.png)

i see a file name called "root.txt" and inside it we got the last 6th question & the root Flag so Done.

and Thanks for reading my write-up & it's a great room try it out.
Good bye, see you in another room!!!