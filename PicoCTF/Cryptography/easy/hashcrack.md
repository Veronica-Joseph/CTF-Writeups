# Challenge Title
hashcrash

## Description
Find the secret stored in the server.

## Tools Used
- hash-identifier
- john the ripper

## Steps to Solve
1. Connect to the Server.
  - Copy and paste the following command in your terminal to access the challenge server (which was provided in the description of the challenge): 
  ```
  nc verbal-sleep.picoctf.net 57192
  ```
  <img width="901" height="113" alt="image" src="https://github.com/user-attachments/assets/8096c1d3-d253-41a5-8c21-ecacde7840be" />


2. Identify the Hash Type
  - To crack the hash, you first need to know what type it is.
      - Run `hash-identifier` in the terminal.
      - Paste the hash when prompted.
      - The tool will suggest possible algorithms based on the hash format.
      - Press Ctrl + C to exit.
      <img width="902" height="351" alt="image" src="https://github.com/user-attachments/assets/467b1afe-e047-4698-b5ec-95dac0c4993f" />
      

3. Crack the Hash
   - Save the hash in a text file:
    ```
     echo "482c811da5d5b4bc6d497ffa98491e38" > hash.txt
    ```
   - Use john with the RockYou wordlist to try and crack it:
       ```
       john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
       ```
       **Breakdown of the command:**
        `john`
           - Runs the John the Ripper tool.
     
        `--wordlist=/usr/share/wordlists/rockyou.txt`
           - This tells John to use the RockYou wordlist — a big list of common passwords.
           - It tries each word in this file as a possible password.
           - This is called a dictionary attack (faster and smarter than brute force).

        `hash.txt`
           - This is the file that contains the hash you want to crack.
           - John reads this file, loads the hash, and compares each word from the wordlist after hashing it the same way.

        `--format=Raw-MD5`
           - Under format add the identified hash type.
           - should adjust this based on what `hash-identifier` stated.
     
      <img width="896" height="188" alt="image" src="https://github.com/user-attachments/assets/183cabc8-3857-468f-92cc-8698a27f2099" />


4. Submit the Password
   Paste the cracked password back into the server prompt.
  <img width="907" height="183" alt="image" src="https://github.com/user-attachments/assets/a9d75067-14b4-4449-a8e0-6f01776b5d27" />


6. Repeat for All Hashes
   Repeat steps 2 to 4 for each new hash.
   
   1. Hash vavlue: `482c811da5d5b4bc6d497ffa98491e38`
      Type: MD5
      Decrypted value: `password123`

   2. Hash vavlue: `b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3`
      Type: SHA1
      Decrypted value: `letmein`
      <img width="902" height="183" alt="image" src="https://github.com/user-attachments/assets/ecb78511-96db-4828-8142-c6d3ed60c0a5" />

   3. Hash vavlue: `916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745`
      Type: SHA256
      Decrypted value: `qwerty098`
      <img width="897" height="263" alt="image" src="https://github.com/user-attachments/assets/900b0903-c6fc-4131-bb1c-20cd01cc44d8" />
      
## Flag
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_29028be8}

## Notes
- A hash is a fixed-length string generated from data using a hash function. Even a tiny change in the input produces a completely different hash.

- Hashes are used to verify data integrity. For example, if you download a file, you can hash it and compare it to the known hash to see if it was tampered with.

- Passwords are stored as hashes in databases—not plain text. Even if someone accesses the database, they won’t directly see the passwords.

- Hashes are one-way—you can't reverse them to get the original data.

- That said, many common passwords and their hashes are publicly available in password lists like rockyou.txt or rainbow tables, which makes weak passwords easy to crack.

- That’s why strong passwords matter. A password like Hello123 might be in a list. But something like g7#J2sQ!z4%R? Much harder to guess or find in any list.

**Some common hash algorithms:**

  - MD5 – Very fast, but broken and easy to crack. Don’t use for security.
  - SHA1 – Slightly better than MD5, but also broken. Not safe for serious use.
  - SHA256 – Strong and widely used. Part of the SHA-2 family.
  - SHA512 – Like SHA256 but produces longer hashes. More secure in some contexts.
  - bcrypt – Slower on purpose. Great for hashing passwords securely.
  - SHA3 – Newer standard with a different design. Secure and future-ready.


# Helpful Resources
What is Hash : https://primer.picoctf.org/#_hashing
Hash-identifier : https://github.com/blackploit/hash-identifier
How to decrypt Hash using John the ripper : https://www.youtube.com/shorts/9-YfKU45qng
