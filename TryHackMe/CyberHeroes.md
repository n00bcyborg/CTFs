
# Cyber Heroes Walkthrough
## Video walkthrough available at: https://youtu.be/qvzDJkLVD_4

# Reconnaissance
The first step for any ctf is to do a network scan using nmap. The results show the existence of a web server on port 80.

After looking through the website, there is a login page.

Looking through the source code, we find our credentials

# Comprimise
The code shows a function that reverses the entered password and compares to a hardcoded one. Reversing this hardcoded password gives us our real password

PWNED!
