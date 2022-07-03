
# Cyber Heroes Walkthrough
## Box available at: https://tryhackme.com/room/cyberheroes
## Video walkthrough available at: https://youtu.be/qvzDJkLVD_4

# Reconnaissance
The first step for any ctf is to do a network scan using nmap. The results show the existence of a web server on port 80.
![image](https://user-images.githubusercontent.com/20043220/177040901-6b2f046a-78d9-4278-a0b1-9a4465c09f88.png)

After looking through the website, there is a login page.
![image](https://user-images.githubusercontent.com/20043220/177040947-bbb0c4aa-f2f4-404d-98f8-3398d909ee03.png)

Looking through the source code, we find our credentials.
![Untitled](https://user-images.githubusercontent.com/20043220/177041041-28a7fa50-d890-42ed-818a-bcd079b5836e.png)

# Comprimise
The code shows a function that reverses the entered password and compares to a hardcoded one. Reversing this hardcoded password gives us our real password.
![Untitled](https://user-images.githubusercontent.com/20043220/177041127-0cd5eaaa-0403-4909-ae9a-efb06c97b983.png)

PWNED!
