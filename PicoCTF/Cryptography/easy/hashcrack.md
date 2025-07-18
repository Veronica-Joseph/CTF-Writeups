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
       john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
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

        `--format=Raw-MD5`
           - Under format add the identified hash type.
     
      <img width="896" height="188" alt="image" src="https://github.com/user-attachments/assets/183cabc8-3857-468f-92cc-8698a27f2099" />

4. Enter the decrypted text.
  <img width="907" height="183" alt="image" src="https://github.com/user-attachments/assets/a9d75067-14b4-4449-a8e0-6f01776b5d27" />

5. Continue steps 2 - 4 until completely decrypting all the provided hashes.
   1. Hash vavlue: 482c811da5d5b4bc6d497ffa98491e38
      Type: MD5
      Decrypted value: password123

   2. Hash vavlue: b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
      Type: SHA1
      Decrypted value: letmein
      <img width="902" height="183" alt="image" src="https://github.com/user-attachments/assets/ecb78511-96db-4828-8142-c6d3ed60c0a5" />

   3. Hash vavlue: 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745
      Type: SHA256
      Decrypted value: qwerty098
      <img width="897" height="263" alt="image" src="https://github.com/user-attachments/assets/900b0903-c6fc-4131-bb1c-20cd01cc44d8" />
      
## Flag
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_29028be8}

## Notes

# Helpful Resources
What is Hash : https://primer.picoctf.org/#_hashing
Hash-identifier : https://github.com/blackploit/hash-identifier

