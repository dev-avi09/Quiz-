# Quiz-A multiplayer quiz app built using python.

def ask_question(question, answer):
    print(f"Question: {question}")
    user_answer = input("Your answer: ").strip().lower()
    return user_answer == answer.strip().lower()

def main():
    # List of questions and answers
    questions = [
        {"question": "What is the capital of France?", "answer": "Paris"},
        {"question": "What is 5 + 5?", "answer": "10"},
        {"question": "What is the largest mammal?", "answer": "Blue whale"},
        {"question": "Who wrote 'Romeo and Juliet'?", "answer": "Shakespeare"}
    ]

    # Player names
    players = input("Enter player names, separated by commas: ").strip().split(",")
    players = [player.strip() for player in players]  # Remove extra spaces
    scores = {player: 0 for player in players}  # Initialize scores

    print("\n--- Welcome to the Multiplayer Quiz Game! ---\n")

    # Game loop
    for i, q in enumerate(questions):
        current_player = players[i % len(players)]  # Rotate players
        print(f"{current_player}'s turn!")
        correct = ask_question(q["question"], q["answer"])
        if correct:
            print("Correct!\n")
            scores[current_player] += 1
        else:
            print(f"Wrong! The correct answer was: {q['answer']}\n")

    # Display final scores
    print("--- Final Scores ---")
    for player, score in scores.items():
        print(f"{player}: {score}")

    # Determine winner(s)
    max_score = max(scores.values())
    winners = [player for player, score in scores.items() if score == max_score]
    print("\n--- Winner(s) ---")
    print(", ".join(winners))

if __name__ == "__main__":
    main()