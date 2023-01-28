
# Agent Sudo Walkthrough
## Box available at: https://tryhackme.com/room/agentsudoctf


# Reconnaissance
The first step for any ctf is to do a network scan using nmap. The results show the existence of several open ports. As always, an web server is always an interesting thing to have a look at.
![image](https://user-images.githubusercontent.com/20043220/215260178-5a25c881-d8b2-4db3-b801-30fe56bfc3d8.png)

We are presented with a static page with a simple message. Looking at the source of the page doesn't show any dynamic integration. The message mentions the 'user_agent'. There are several ways of changing the user-agent. You can use a browser addon,  or you can just use curl and send a modified header.
![image](https://user-images.githubusercontent.com/20043220/215260571-2324931a-71c8-4d11-ba16-7ba88016198e.png)


# Compromise
Iterating through the agents (A, B, C e.tc) will give us the hidden page alongside the name for one of our answers.
![image](https://user-images.githubusercontent.com/20043220/215261115-266e0ff2-3c0d-41f2-8ddb-677a7b74db2e.png)

As observed during the enumeration stage, there is a ftp server on the machine. The password can be bruteforced using Hydra and the rockyou txt file.
![image](https://user-images.githubusercontent.com/20043220/215261517-5bc425c9-63a0-49f2-9d66-1605feb63267.png)

After getting access to the ftp server. We can download all the files using the mget * command.
The message left for us mentions the existence of credentials in the files. THere are several stegnatography programs out there. In this case, binwalk can automatically extract files hidden within images. Doing so reveals the existence of a zip file. 
![image](https://user-images.githubusercontent.com/20043220/215262052-099800c8-81df-42bc-b2ba-3b7746389e23.png)

The created folder contains several files. THere is a zip file which requires a password, and a txt file that is empty. We can brute the zip file by running zip2john to get a hash. We can then run john against the hash using rockyou.txt. THe password of the zip file can then be recovered.
![image](https://user-images.githubusercontent.com/20043220/215262403-24786b95-abee-4db3-b1fa-97d8cff7be9d.png)

After going through the txt file, we get a base64 password. This can easily be reversed by using somthing like cyberchef. Since there are two image files. One gave us the hidden files, perhaps the other one contains more hidden files. THis can be cracked by using steghid and our newly discovered password.
![image](https://user-images.githubusercontent.com/20043220/215262768-96d76543-d9b6-4e1e-9bb6-1ed5edb748a6.png)

The third and final port that we discovered from our enumeration stage was SSH. We can use our newly discovered credentials to SSH into the machine. The rest of the answers can be found by viewing the files containted within the home folder.
![image](https://user-images.githubusercontent.com/20043220/215262929-c0b98e53-5d70-4a6d-a747-f9c7d6fb3105.png)

Doing a reverse image search of the jpg file will give the name of the incident.
![image](https://user-images.githubusercontent.com/20043220/215263383-239acb8c-1069-47a4-905a-503f14b87c9f.png)


# Priviledge Escalation
Running the sudo -l command allows us to see what the user can do. The result doesn't make too much sense. Searching for sudo CVEs will give us the answer to the CVE.

Upon running the syntax found after a google search, we now escalate into root!
![image](https://user-images.githubusercontent.com/20043220/215263948-ba7b0872-3d90-494f-9aad-58db40923b96.png)


PWNED!
