---
layout: default
title: SystemVerilog on macOS
permalink: /notes/c/terminalControl
lastmod: 2026-04-18
---
[← ../C Miscellaneous](../c)

## Printf and Terminal Control
_Last modified: {{ page.lastmod | date: "%b %d, %Y" }}_ 

So today, I was coding SOS on c just because. And I really wanted to make cleaner board for obvious reasons. After some browsing, I found a good [website](https://student.cs.uwaterloo.ca/~cs452/terminal.html) that had everything that I needed. Below, I transferred the entire website in .md format.

---

These are the most essential terminal control sequences that you will need for your train program.

| Code            | Effect                                                                 |
|-----------------|------------------------------------------------------------------------|
| `\033[2J`       | Clear the screen.                                                      |
| `\033[H`        | Move the cursor to the upper-left corner of the screen.                |
| `\033[r;cH`     | Move the cursor to row r, column c (both indexed starting at 1).       |
| `\033[?25l`     | Hide the cursor.                                                       |
| `\033[K`        | Delete everything from the cursor to the end of the line.              |


These control sequences can help make your program's display more lively.

| Code        | Effect                                   |
|-------------|------------------------------------------|
| `\033[0m`   | Reset special formatting (such as colour)|
| `\033[30m`  | Black text                               |
| `\033[31m`  | Red text                                 |
| `\033[32m`  | Green text                               |
| `\033[33m`  | Yellow text                              |
| `\033[34m`  | Blue text                                |
| `\033[35m`  | Magenta text                             |
| `\033[36m`  | Cyan text                                |
| `\033[37m`  | White text                               |
