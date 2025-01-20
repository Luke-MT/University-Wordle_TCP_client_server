# Wordle Game TCP_client_server

A client-server implementation of the popular word-guessing game Wordle, built in C using socket programming. This networked version allows players to connect to a server and play the game through a command-line interface.

## Description

This project implements a networked version of Wordle where:
- The server maintains a list of possible words and randomly selects target words
- Clients connect to the server and attempt to guess the word
- The server provides feedback using special characters to indicate correct letters and positions
- Players have a limited number of attempts to guess the word correctly

## Features

- TCP/IP socket-based client-server architecture
- Configurable number of attempts (6-10, defaults to 6)
- Interactive command-line interface
- Real-time feedback on guess attempts
- Proper error handling for invalid inputs
- Clean disconnection handling

### Prerequisites

- GCC compiler
- UNIX-like operating system

### Installation

Compile the server and client:
```bash
gcc -o wordle_server server.c
gcc -o wordle_client client.c
```

## Usage

### Starting the Server

```bash
./wordle_server <port> [attempts]
```
- `port`: The port number to listen on
- `attempts`: (Optional) Number of attempts allowed (6-10, defaults to 6)

Example:
```bash
./wordle_server 8080 8
```

### Starting the Client

```bash
./wordle_client <server_ip> <port>
```
- `server_ip`: The IP address of the server
- `port`: The port number the server is listening on

Example:
```bash
./wordle_client 127.0.0.1 8080
```

## Game Rules

1. The server selects a random 5-letter word from its dictionary
2. Players have a limited number of attempts to guess the word
3. After each guess, the server responds with:
   - `*`: Letter is correct and in the right position
   - `+`: Letter is in the word but in the wrong position
   - `-`: Letter is not in the word
4. The game ends when either:
   - The player guesses the word correctly
   - The player runs out of attempts
   - The player chooses to quit

## Protocol Specification

### Server Messages
- Welcome: `OK <attempts> <welcome_message>`
- Correct guess: `OK PERFECT`
- Incorrect guess: `OK <attempt_number> <feedback>`
- Game over: `END <attempts> <target_word>`
- Error: `ERR <error_message>`
- Quit response: `QUIT <goodbye_message>`

### Client Messages
- Guess: `WORD <5_letter_word>`
- Quit: `QUIT`

## Error Handling

The implementation includes robust error handling for:
- Invalid word length
- Non-alphabetic characters
- Connection issues
- Invalid commands
- Socket errors
