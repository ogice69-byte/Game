import random

# Mixed Flirty + Naughty Questions (50 total)
questions = [
    "Tell me something about yourself that would surprise me in a good way.",
    "What's your idea of the perfect flirty first date?",
    "If I saw you across the room, what would make me want to approach you?",
    "What's one thing about your personality that people find irresistible?",
    "What's your favorite way to tease someone you're attracted to?",
    "Tell me about a time you felt instantly attracted to someone. What sparked it?",
    "What's your go-to flirty compliment that actually works?",
    "If we were texting right now, what would your first naughty emoji be?",
    "What's something innocent about you that secretly turns you on?",
    "Describe your perfect kiss in detail.",
    "What's a hobby or interest that makes you feel sexy and confident?",
    "If I asked you out right now, what would you wear to impress me?",
    "What's the most adventurous thing you've done on a date?",
    "Tell me a secret talent you have that could be useful in the bedroom.",
    "What's your favorite body part on yourself that you love showing off?",
    "Have you ever had a crush that turned into something much hotter?",
    "What's the flirtiest message you've ever sent or received?",
    "If we were alone on a beach at night, what would you want to do?",
    "What's something about your past that still makes you blush?",
    "Do you prefer slow teasing flirting or bold and direct?",
    "What's your favorite way for someone to touch you casually?",
    "Tell me about your wildest 'what if' fantasy involving a stranger.",
    "What's the hottest compliment you've ever given or received?",
    "Have you ever been told you have a sexy voice? Do you use it on purpose?",
    "What's your signature move when you want to turn up the heat?",
    "If you could redesign your bedroom for maximum seduction, what would it look like?",
    "What's the most playful way you've ever seduced someone?",
    "Tell me about a dream (sleep or daydream) that involved intense chemistry.",
    "What's your favorite spot to be kissed that drives you crazy?",
    "Have you ever mixed food and flirting in a fun way?",
    "What's the naughtiest thought you've had about someone you just met?",
    "Do you like being chased or doing the chasing when flirting?",
    "What's your favorite dirty talk starter phrase?",
    "Tell me something personal that makes you feel vulnerable but excited.",
    "What's the wildest place you've ever flirted with someone?",
    "If we played truth or dare right now, what dare would you give me?",
    "What's your biggest turn-on that starts with just eye contact?",
    "Have you ever had sex somewhere you definitely shouldn't have?",
    "What's the best way for someone to make you feel desired?",
    "Describe your ideal mix of sweet romance and naughty fun.",
    "What's a fantasy you've never shared because it's 'too much'?",
    "Do you prefer long teasing foreplay or jumping straight in?",
    "Tell me about a time flirting led to something unforgettable.",
    "What's your favorite position and why does it feel amazing?",
    "Have you ever sent a risky photo or text that made things exciting?",
    "If I whispered something naughty in your ear right now, how would you react?",
    "What's the kinkiest thing on your 'maybe someday' list?",
    "Do you like being dominant, submissive, or switching it up?",
    "What's one naughty question you've always wanted to ask someone on a date?",
    "If we were together alone right now, what's the first flirty or dirty thing you'd do or say?"
]

def play_game():
    print("🔥 Flirty & Naughty Questions Game 🔥\n")
    print("Choose mode:")
    print("1. Single Player")
    print("2. Two Player Mode (with score tracking)")
    mode = input("Enter 1 or 2: ").strip()

    is_two_player = mode == "2"
    
    if is_two_player:
        player1_name = input("Enter Player 1 name: ").strip() or "Player 1"
        player2_name = input("Enter Player 2 name: ").strip() or "Player 2"
        scores = {player1_name: 0, player2_name: 0}
        print(f"\n🎮 Two Player Mode Activated! Take turns and rate each other's answers.\n")
    else:
        player1_name = "You"
        scores = {player1_name: 0}

    print("Commands: 'r' = random question, 'next' = sequential, 'all' = show all,")
    print("'scores' = show current scores, 'quit' = exit\n")
    
    used = []
    index = 0
    turn = 0  # For alternating players
    
    while True:
        if is_two_player:
            current_player = player1_name if turn % 2 == 0 else player2_name
            print(f"\n📍 {current_player}'s turn!")
        
        cmd = input("Command (r / next / all / scores / quit): ").strip().lower()
        
        if cmd == "quit":
            print("\n🏆 Final Scores:")
            for p, s in scores.items():
                print(f"  {p}: {s} points 🔥")
            print("See you next time... 😏")
            break
        elif cmd == "all":
            for i, q in enumerate(questions, 1):
                print(f"{i}. {q}")
            continue
        elif cmd == "scores":
            print("\nCurrent Scores:")
            for p, s in scores.items():
                print(f"  {p}: {s} points")
            continue
        elif cmd in ["r", "next"]:
            if len(used) == len(questions):
                print("All questions used! Restarting list...")
                used.clear()
                index = 0
            
            if cmd == "r":
                q = random.choice(questions)
                while q in used and len(used) < len(questions):
                    q = random.choice(questions)
            else:  # next
                if index >= len(questions):
                    index = 0
                q = questions[index]
                index += 1
            
            used.append(q)
            current_player = player1_name if not is_two_player else (player1_name if turn % 2 == 0 else player2_name)
            print(f"\n🔥 Question for {current_player}: {q}\n")
            print("💬 Answer the question out loud or in chat!")
            
            # Rating for points
            while True:
                try:
                    rating = int(input(f"Rate {current_player}'s answer (1-10 spice level): "))
                    if 1 <= rating <= 10:
                        points = rating * 10
                        scores[current_player] += points
                        print(f"💥 {current_player} earns {points} points! Total: {scores[current_player]}\n")
                        break
                    else:
                        print("Please enter a number between 1 and 10.")
                except ValueError:
                    print("Invalid input. Enter a number 1-10.")
            
            if is_two_player:
                turn += 1
        else:
            print("Invalid command. Try r, next, all, scores, or quit.")

if __name__ == "__main__":
    play_game()
