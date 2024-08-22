# tic_tac_toe
# game set up
def print_board(board):
    """Print the Tic-Tac-Toe board."""
    for row in board:
        print("|".join(row))
        print("-" * 5)

def check_winner(board, player):
    """Check if the current player has won."""
    # Check rows, columns, and diagonals
    for row in board:
        if all([spot == player for spot in row]):
            return True

    for col in range(3):
        if all([board[row][col] == player for row in range(3)]):
            return True

    if all([board[i][i] == player for i in range(3)]) or all([board[i][2 - i] == player for i in range(3)]):
        return True

    return False

def check_draw(board):
    """Check if the game is a draw."""
    return all([spot != ' ' for row in board for spot in row])

def tic_tac_toe():
    """Run the Tic-Tac-Toe game."""
    board = [[' ' for _ in range(3)] for _ in range(3)]
    current_player = 'X'

    while True:
        print_board(board)
        print(f"Player {current_player}'s turn")

        # Get the player's move
        while True:
            try:
                row = int(input("Enter the row (0, 1, 2): "))
                col = int(input("Enter the column (0, 1, 2): "))
                if board[row][col] == ' ':
                    board[row][col] = current_player
                    break
                else:
                    print("That spot is already taken. Try again.")
            except (ValueError, IndexError):
                print("Invalid input. Please enter numbers between 0 and 2.")

        # Check for a winner or a draw
        if check_winner(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break

        if check_draw(board):
            print_board(board)
            print("It's a draw!")
            break

        # Switch players
        current_player = 'O' if current_player == 'X' else 'X'

if __name__ == "__main__":
    tic_tac_toe()
