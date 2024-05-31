# tic-tak-toe-game
This is the c language project
Header Inclusion:
                #include <stdio.h>
•	This line incorporates the standard input/output library (stdio.h), providing functions for formatted input (scanf) and output (printf).
Constant Definition:
              #define SIZE 3
•	This line defines a symbolic constant named SIZE with a value of 3. This constant is used throughout the code to represent the size of the Tic-Tac-Toe board (a 3x3 grid).
Draw Board Function:
 
This function takes a 2D character array board (representing the Tic-Tac-Toe board) as its argument.
•	It iterates through the board array using nested loops to print the current state of the game board to the console. 
o	Each inner loop (j loop) prints a cell value ('X', 'O', or '-') followed by a space.
o	If the cell is not the last one in a row, a vertical bar ('|') is printed to create a grid-like visual.
o	Each outer loop (i loop) prints a newline character (\n) after each row.
o	If the row is not the last one, a horizontal separator line ("-----------") is printed using printf.
Check Win Function:
 
•	This function takes a 2D character array board and a character c (representing the player's symbol) as its arguments.
•	It checks if the player with symbol c has achieved a winning condition on the Tic-Tac-Toe board. 
o	It iterates through the rows and columns using a loop (i). 
	Inside the loop, it uses conditional statements (OR operators ||) to check if all three cells in a row (board[i][0], board[i][1], and board[i][2]) or column (board[0][i], board[1][i], and board[2][i]) match the player's symbol (c). 
	If a match is found, the function returns 1, indicating a win.
o	Additionally, it checks for diagonal wins. 
	It uses conditional statements to check if all three cells in the first and second diagonals match the player's symbol. 
	If a diagonal match is found, the function returns 1.
•	If no winning condition is found, the function returns 0.

code;
#include <stdio.h>
//size is defined to 3 because we want to make the 3x3 matrix
#define SIZE 3
void drawBoard(char board[SIZE][SIZE]) {
    int i, j;
    for (i = 0; i < SIZE; i++) {
        for (j = 0; j < SIZE; j++) {
            printf(" %c ", board[i][j]);
            //j+1 is use to print 2 times "|".
            if (j+1 < SIZE)
                printf("|");
        }
        printf("\n");
         // this if statement will make a between two rows.
        // the i+1 is used to run and print the loop 2 times.
        if (i+1 < SIZE)
            printf("-----------\n");
    }
}
int checkWin(char board[SIZE][SIZE], char c) {
    int i;
    for (i = 0; i < SIZE; i++) {
          // the first statement covers the horiontal wins and 
        //the statement after or operator covers  the vertical wins of both patyers.
        // c is the player.
        if ((board[i][0] == c && board[i][1] == c && board[i][2] == c) ||
            (board[0][i] == c && board[1][i] == c && board[2][i] == c))
            return 1;
    }
    if ((board[0][0] == c && board[1][1] == c && board[2][2] == c) ||
        (board[0][2] == c && board[1][1] == c && board[2][0] == c))
        return 1;
    return 0;
}

int main() {
    // initialing a 2D  charcters array 
    char board[SIZE][SIZE];
    int i, j, player = 0;
    int moves = 0; // count the number of moves
    for (i = 0; i < SIZE; i++)
        for (j = 0; j < SIZE; j++)
         // THIS LINE (board[i][j] = '-';) is used to print - in every box.
            board[i][j] = '-';
    while (1) {
        drawBoard(board);
        int x, y;
        printf("Player %d, enter your move: ", player + 1);
        scanf("%d%d", &x, &y);
        x--; y--;
        if (x < 0 || x >= SIZE || y < 0 || y >= SIZE || board[x][y]!= '-') {
            printf("Invalid move, try again.\n");
            continue;
        }
         // the below statement is used to automatically 
        //assigned  "X" to 1st player and "O" to 2nd player.
        board[x][y] = (player == 0)? 'X' : 'O';
        moves++; // increment the move count
        if (checkWin(board, (player == 0)? 'X' : 'O')) {
            printf("Player %d wins!\n", player + 1);
            break;
        }
        if (moves == SIZE * SIZE) {
            printf("It's a tie!\n");
            break;
        }
         // this statement is used for switching between players
        // the player = 0 then the 1st player turn
        //and after the move of 1st player than the this below 
        //statement will make 0 to 1 the the turn for 2nd palyer.
        player =!player;
    }
    return 0;
}

Explanation of the Flowchart:
1.	Start (A): The program starts here.
2.	Initialize board (B): A 3x3 character array board is initialized with each cell containing a '-'.
3.	Draw board (C): The drawBoard function is called to display the current state of the game board on the console.
4.	Player turn (D): It's determined whose turn it is (player 0 or 1).
5.	Get player move (E): The player enters their move coordinates (row and column) using scanf.
6.	Validate move (F): The move is checked for validity (within board boundaries and not already occupied). 
o	If invalid, an error message is displayed, and the loop continues back to step D.
o	If valid, the move proceeds to step G.
7.	Assign symbol (G): Based on the current player (0 or 1), the corresponding symbol ('X' or 'O') is assigned to the entered board position.
8.	Check win (H): The checkWin function is called to check if the recent move resulted in a win (three matching symbols in a row, column, or diagonal). 
o	If no win, the loop continues back to step C.
o	If win, a victory message is displayed in step I.
9.	Check for tie (J): It's checked if all cells are filled (number of moves equals the total number of board cells). 
o	If not a tie, the loop continues back to step C.
o	If a tie, a tie message is displayed in step I.
10.	End (K): The program exits.

