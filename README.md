# Task-3-C-

#include <iostream>
#include <vector>
using namespace std;

void print_board(vector<vector<char>>& board) {
    for (auto& row : board) {
        for (auto& cell : row) {
            cout << cell << " | ";
        }
        cout << endl;
        cout << "---------" << endl;
    }
}

bool check_winner(vector<vector<char>>& board, char player) {
    for (auto& row : board) {
        bool win = true;
        for (auto& cell : row) {
            if (cell != player) {
                win = false;
                break;
            }
        }
        if (win) {
            return true;
        }
    }
    
    for (int col = 0; col < 3; col++) {
        bool win = true;
        for (int row = 0; row < 3; row++) {
            if (board[row][col] != player) {
                win = false;
                break;
            }
        }
        if (win) {
            return true;
        }
    }
    
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player) {
        return true;
    }
    
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player) {
        return true;
    }
    
    return false;
}

bool is_full(vector<vector<char>>& board) {
    for (auto& row : board) {
        for (auto& cell : row) {
            if (cell == ' ') {
                return false;
            }
        }
    }
    return true;
}

bool play_again() {
    string choice;
    cout << "Do you want to play again? (yes/no): ";
    cin >> choice;
    return choice == "yes";
}

void tic_tac_toe() {
    vector<char> players = {'X', 'O'};
    int current_player = 0;
    vector<vector<char>> board(3, vector<char>(3, ' '));
    bool game_over = false;
    while (!game_over) {
        print_board(board);
        char player = players[current_player];
        cout << "Player " << player << "'s turn." << endl;
        while (true) {
            int row, col;
            cout << "Enter row (0, 1, 2): ";
            cin >> row;
            cout << "Enter column (0, 1, 2): ";
            cin >> col;
            if (board[row][col] == ' ') {
                board[row][col] = player;
                break;
            } else {
                cout << "Invalid move! That cell is already taken. Try again." << endl;
            }
        }
        if (check_winner(board, player)) {
            print_board(board);
            cout << "Player " << player << " wins!" << endl;
            game_over = true;
        } else if (is_full(board)) {
            print_board(board);
            cout << "It's a draw!" << endl;
            game_over = true;
        }
        current_player = (current_player + 1) % 2;
    }
    if (play_again()) {
        tic_tac_toe();
    } else {
        cout << "Thanks for playing!" << endl;
    }
}

int main() {
    tic_tac_toe();
    return 0;
}

