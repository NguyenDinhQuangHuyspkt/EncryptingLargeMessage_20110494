# 20110494: Nguyễn Đình Quang Huy
# Task 1: Encrypt and Decrypt Text file

Create file plain.txt with content: "Nguyen Dinh Quang Huy: 20110494"

<img src = 'https://github.com/user-attachments/assets/c62d5eea-8343-4180-aa3d-e2634df21d97' alt = 'imageLab'/>

View the file encoded with xxd, then decoded with different aes encodings, in different modes.

Endcode: openssl enc -aes-256-ecb -nosalt -in plain.txt -out ecb_encrypted.txt -K 00112233445566778899AABBCCDDEEFF00112233445566778899AABBCCDDEEFF

<img src = 'https://github.com/user-attachments/assets/e710ded2-4b50-4dea-91f0-4143955db4dc' alt = 'imageLab'/>

Decode: openssl enc -d -aes-256-ecb -nosalt -in ecb_encrypted.txt -out ecb_decrypted.txt -K 00112233445566778899AABBCCDDEEFF00112233445566778899AABBCCDDEEFF

<img src = 'https://github.com/user-attachments/assets/31292fc8-49c6-49d5-87be-413007631686' alt = 'imageLab'/>

With CBC:

Endcode: openssl enc -aes-256-cbc -nosalt -in plain.txt -out cbc_encrypted.txt -K 00112233445566778899AABBCCDDEEFF00112233445566778899AABBCCDDEEFF -iv 0102030405060708090A0B0C0D0E0F10

<img src = 'https://github.com/user-attachments/assets/12693269-b6f6-4609-bc34-9d50ee538415' alt = 'imageLab'/>

Decode: openssl enc -d -aes-256-cbc -nosalt -in cbc_encrypted.txt -out cbc_decrypted.txt -K 00112233445566778899AABBCCDDEEFF00112233445566778899AABBCCDDEEFF -iv 0102030405060708090A0B0C0D0E0F10

<img src = 'https://github.com/user-attachments/assets/7afa91e4-d51f-4bd0-9c14-09397f6660c3' alt = 'imageLab'/>

# Task 2: Encryption Mode – ECB vs. CBC

Install file.bitmap and rename is : 'origin.bmp'

Extract header and body

<ul>
  <li>dd if=origin.bmp of=header.bin bs=1 count=54: </li>
  <li>dd if=origin.bmp of=body.bin bs=1 skip=54</li>
  <li>Endcode Body: openssl enc -aes-256-cbc -nosalt -in body.bin -out encrypted_body.bin -K "00112233445566778899AABBCCDDEEFF00112233445566778899AABBCCDDEEFF" -iv "0102030405060708090A0B0C0D0E0F10"
</li>
</ul>

<image loading={lazy} src = 'https://github.com/user-attachments/assets/6486db93-0f17-431d-a744-a2439b3e29b6' alt = 'imageLab'/>

<img src = 'https://github.com/user-attachments/assets/e978a97a-1433-4d72-9284-97f3e5c2e4cd' alt = 'imageLab'/>

<img src = 'https://github.com/user-attachments/assets/bcbb23c7-96c1-431e-9ae7-b693a7bac036' alt = 'imageLab'/>

Combine header and body encoding:

<img src = 'https://github.com/user-attachments/assets/6018a1ff-31ed-4a7c-9388-0eddb2066969' alt = 'imageLab'/>


# Task 3: Encryption Mode – Corrupted Cipher Text

Create a file and encode:

openssl enc -aes-256-cbc -nosalt -in plain.txt -out encrypted.txt -K 00112233445566778899AABBCCDDEEFF00112233445566778899AABBCCDDEEFF -iv 0102030405060708090A0B0C0D0E0F10

<img src = 'https://github.com/user-attachments/assets/ecd83d34-5db1-4e36-9a1a-6d0cc7c5bda5' alt = 'imageLab'/>

Corrupt one bit of the 5th byte:

dd if=encrypted.txt of=corrupted.txt bs=1 count=4 skip=4 conv=notrunc

<img src = 'https://github.com/user-attachments/assets/f3219920-dbe5-40fd-9a95-890ceb9f858f' alt = 'imageLab'/>

