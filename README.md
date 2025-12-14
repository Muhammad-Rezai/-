import re

def check_password_strength(password):
    score = 0
    feedback = []

    if len(password) >= 8:
        score += 2
    else:
        feedback.append("Password should be at least 8 characters long.")

    if re.search(r"[a-z]", password):
        score += 1
    else:
        feedback.append("Add at least one lowercase letter.")

    if re.search(r"[A-Z]", password):
        score += 1
    else:
        feedback.append("Add at least one uppercase letter.")

    if re.search(r"[0-9]", password):
        score += 1
    else:
        feedback.append("Add at least one number.")

    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        score += 2
    else:
        feedback.append("Add at least one special character.")

    if score <= 3:
        strength = "Weak ❌"
    elif score <= 6:
        strength = "Medium ⚠️"
    else:
        strength = "Strong ✅"

    return strength, score, feedback


def main():
    print("🔐 Password Strength Checker 🔐")
    print("Type 'exit' or 'q' to quit.\n")

    while True:
        password = input("Enter password: ")

        if password.lower() in ["exit", "q"]:
            print("\nGoodbye 👋")
            break

        strength, score, feedback = check_password_strength(password)

        print(f"\nStrength: {strength}")
        print(f"Score: {score}/7")

        if feedback:
            print("Suggestions:")
            for item in feedback:
                print(f"- {item}")
        else:
            print("✔️ Your password is strong.")

        print("\n" + "-" * 40 + "\n")


if __name__ == "__main__":
    main()
