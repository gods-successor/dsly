import random


1) passworrd cracker
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
