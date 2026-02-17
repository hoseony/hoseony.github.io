---
layout: default
title: SystemVerilog on macOS
permalink: /notes/c/terminalControl
lastmod: 2026-02-17
---
[← ../C Miscellaneous](../c)

## Printf and Terminal Control
_Last modified: {{ page.lastmod | date: "%b %d, %Y" }}_ \

So today, I was coding SOS on c just because. And I really wanted to make cleaner board for obvious reasons. After some prowsing, I found a good [website](https://student.cs.uwaterloo.ca/~cs452/terminal.html) that had everything that I needed.

This is where I was using if you are curious:
```c
void draw_board(void) {
    printf("\033[H"); 
    printf("\033[2J"); 

    for (int row = 0; row < B_SIZE; row ++) {
        for (int col = 0; col < B_SIZE; col ++) {
            printf("%c|", board[row][col]);
        }
        printf("\n");

        for (int col = 0; col < B_SIZE; col ++) {
            printf("-+");
        }
        printf("\n");
    }
}

void init_board(void) {

    int row, col;

    for (row = 0; row < B_SIZE; row++) {
        for (col = 0; col < B_SIZE; col ++) {
            board[row][col] = ' ';
        }
    } 
}

int main() {
    printf("\033[2J"); 
    init_board();
    draw_board();

    board[3][3] = getchar();

    draw_board();
    draw_board();

    return 0;
}
```
