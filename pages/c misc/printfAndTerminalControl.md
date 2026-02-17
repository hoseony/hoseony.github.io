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
#include <stdio.h>

#define B_SIZE 10

char board[B_SIZE][B_SIZE];

void draw_board(void) {
    printf("\033[H"); 
	// This moves the cursor to the beginning 
	// (I probably need to change this back to \033[2J but it's quite fun to mass around the terminal)

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

    for (int i = 0; i < B_SIZE; i++) {
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
    printf("\033[2J"); //This cleans the entire terminal to initialize it 
    init_board();
    draw_board();

    board[3][3] = getchar();


    draw_board();

    return 0;
}
```
