# Challenge Title
hashcrash

## Description
Find the secret stored in the server.

## Tools Used
- hash-identifier
- john the ripper

## Steps to Solve
1. Go to the server, provided in the link.
  - Copy and paste the server on your machine.
  ```
  nc verbal-sleep.picoctf.net 57192
  ```
  <img width="901" height="113" alt="image" src="https://github.com/user-attachments/assets/8096c1d3-d253-41a5-8c21-ecacde7840be" />

2. Identify the hash
  - Now we need to identify the hash to decrypt it
      - For that used the tool `hash-identifier`
      - Type `hash-identifier` in the terminal and paste the hash.
      <img width="902" height="351" alt="image" src="https://github.com/user-attachments/assets/467b1afe-e047-4698-b5ec-95dac0c4993f" />
      - ctrl + C --> exit the `hash-identifier`

3. Decrypt the hash.
   - Save the hash inside the file
    ```
     echo "482c811da5d5b4bc6d497ffa98491e38" > hash.txt
    ```
   - Use John the ripper to crack the hash.
       ```
       john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
       ```
        `john`
           - This runs the John the Ripper program.

        `--wordlist=/usr/share/wordlists/rockyou.txt`
           - This tells John to use the RockYou wordlist — a big list of common passwords.
           - It tries each word in this file as a possible password.
           - This is called a dictionary attack (faster and smarter than brute force).

        `hash.txt`
           - This is the file that contains the hash you want to crack.
           - John reads this file, loads the hash, and compares each word from the wordlist after hashing it the same way.


## Flag
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_29028be8}

## Notes
What you learned

# Helpful Resources
https://primer.picoctf.org/#_hashing
