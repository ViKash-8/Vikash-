# Tic-Tac-Toe game in Python

# Function to print the board
def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 9)

# Function to check if someone has won
def check_winner(board, player):
    for row in board:
        if all(s == player for s in row):
            return True
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

# Function to check if the board is full
def is_full(board):
    return all(cell != " " for row in board for cell in row)

# Main function
def play_game():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

    while True:
        print_board(board)
        print(f"Player {current_player}, it's your turn!")

        # Input position
        try:
            row, col = map(int, input("Enter row and column (0-2) separated by space: ").split())
            if board[row][col] != " ":
                print("This cell is already occupied. Try again.")
                continue
        except (ValueError, IndexError):
            print("Invalid input. Enter row and column numbers between 0 and 2.")
            continue

        # Update board
        board[row][col] = current_player

        # Check winner
        if check_winner(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break

        # Check if the board is full
        if is_full(board):
            print_board(board)
            print("It's a draw!")
            break

        # Switch player
        current_player = "O" if current_player == "X" else "X"

# Run the game
play_game()
