# spam
```
import re

# Function to load spam keywords from a file
def load_keywords_from_file(file_path):
    try:
        with open(file_path, 'r') as file:
            keywords = [line.strip().lower() for line in file.readlines()]
        return keywords
    except FileNotFoundError:
        print(f"Error: The file {file_path} was not found.")
        return []

# Function to classify an email based on rules
def classify_email_rule_based(email, spam_keywords):
    # Rule 1: Check for spam keywords
    if any(keyword in email.lower() for keyword in spam_keywords):
        return "spam"
    
    # Rule 2: Check for common spam patterns (e.g., excessive punctuation)
    if len(re.findall(r"[!$%^&*()]+", email)) > 5:
        return "spam"
    
    # Rule 3: Check for links (URLs)
    if re.search(r"http[s]?://", email):
        return "spam"
    
    # Rule 4: Check for phishing phrases
    phishing_phrases = ["bank account", "credit card", "social security", "password"]
    if any(phrase in email.lower() for phrase in phishing_phrases):
        return "spam"
    
    # If none of the rules matched, it's considered "ham"
    return "ham"

# Main function to get input from the user and classify the email
def main():
    # File path with the given location
    file_path = r'C:\new project\methods\rule based\spam_keywords.txt'  # Correct file path
    
    # Load keywords from the file
    spam_keywords = load_keywords_from_file(file_path)  # Use the correct file path
    
    if not spam_keywords:
        print("No keywords found, exiting.")
        return
    
    # Get email content from the user
    email_content = input("Enter the email content: ")
    
    # Classify the email based on the loaded keywords
    result = classify_email_rule_based(email_content, spam_keywords)
    
    print(f"The email is classified as: {result}")

# Run the main function to interact with the user
if __name__ == "__main__":
    main()
```
