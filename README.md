from datetime import datetime

# Function to save messages
def save_message(name, message):
    with open("memory_messages.txt", "a", encoding="utf-8") as file:
        file.write(f"{datetime.now()} - {name}: {message}\n")

# Greeting
name = input("Enter your name: ").strip()
print(f"\nHello {name}! 🌟\n")

# Choice menu
choice = input("Do you want to (1) tell me your fondest memory of us, or (2) have me tell you mine? (Enter 1 or 2): ")

# Special message for Thando (case-insensitive)
if name.lower() == "thando":
    sweet_message = ("💖 My fondest memory of us was when we were playing eFootball "
                     "and you'd beat me. Well, I did not care as long as I did something "
                     "that connected me to you... else I loved every moment I shared with you. 💖")
    print("\n" + sweet_message)
    save_message(name, sweet_message)
else:
    if choice == "1":
        user_memory = input("Please share your fondest memory: ")
        print(f"\nThank you for sharing, {name}! 🌟")
        save_message(name, user_memory)
    elif choice == "2":
        my_memory = "✨ My fondest memory of us is every little moment we spent laughing and connecting. ✨"
        print("\n" + my_memory)
        save_message(name, my_memory)
    else:
        print("\nInvalid choice. Please restart and select 1 or 2.")

# Ask if they want to share a secret
share_secret = input("\nDo you want to share a secret? (yes/no): ").strip().lower()
if share_secret == "yes":
    user_secret = input("Okay, what's your secret? 🤫: ")
    print("\nThank you for trusting me with your secret! 🌟")
    save_message(name, f"Secret: {user_secret}")

# You share your secret
my_secret = "💌 I want to share my secret too: For the first time in my life I don't want to die :)"
print("\n" + my_secret)
save_message("Me", my_secret)

print("\n✨ All memories and secrets are saved in 'memory_messages.txt' ✨")
