# 📡 ft_irc – École 42 | Paris

An IRC server developed in **C++98**, following the [IRC Protocol RFC 1459](https://datatracker.ietf.org/doc/html/rfc1459), and designed to handle multiple simultaneous client connections via TCP/IP in non-blocking mode.

---

## 📌 Project Goals

- Implement a functional IRC server in C++98
- Handle multiple clients concurrently (non-blocking I/O, no threads/fork)
- Parse and handle essential IRC commands:
  - `NICK`, `USER`, `JOIN`, `PRIVMSG`, `KICK`, `INVITE`, `TOPIC`, `MODE`, etc.
- Require password authentication from clients
- Support channel operators and related command privileges

---

## 🧠 Key Features

- **TCP/IP communication** using `poll()` and raw sockets (IPv4/IPv6 support)
- **Channel management**: join, leave, set topic, manage modes
- **Non-blocking architecture**: handles all input/output without blocking any clients
- **Authentication**: requires a password on connection
- **Multi-client support**: no threads, no forks — pure multiplexing
- **Bot-ready**: the structure allows easy integration of basic IRC bots

---

⚙️ Compilation
```
make         # Build the project
make clean   # Remove object files
make fclean  # Remove all binaries and object files
make re      # Recompile the project from scratch
```
⚠️ Compiled using C++98 with flags: -Wall -Wextra -Werror

🚀 Usage
```
./ircserv <port> <password>
```
<port>: the port on which the server will listen
<password>: required for any client trying to connect

Example:

| Command   | Description                                        |
| --------- | -------------------------------------------------- |
| `PASS`    | Authenticate with the server password              |
| `NICK`    | Set/change the nickname                            |
| `USER`    | Register the username                              |
| `JOIN`    | Join or create a channel                           |
| `PRIVMSG` | Send a message privately or to a channel           |
| `KICK`    | Kick a user from a channel (operator only)         |
| `INVITE`  | Invite a user to a channel                         |
| `TOPIC`   | Set or view a channel topic                        |
| `MODE`    | Set channel/user modes (e.g., operator privileges) |


🧪 Testing & Tools
🔧 With netcat (basic)
```
nc <server_ip> <port>
```
Then manually send commands:

```
PASS secret123
NICK Ayoub
USER ayoub 0 * :Ayoub Khamassi
JOIN #42
PRIVMSG #42 Hello, world!
```
💬 With irssi (recommended)
```
sudo apt install irssi  # or brew install irssi on macOS
```
Method 1 (interactive)
```
irssi
/connect <server_ip> <port>
```
Method 2 (one-liner)
```
irssi -c <server_ip> -p <port> -n <nickname> -w <password>
```
Commands inside irssi:
 ```
/join #42
/msg #42 hello everyone
 ```
🧪 Advanced Debug & Tools

 
| Command                                                              | Purpose                           |
| -------------------------------------------------------------------- | --------------------------------- |
| `lsof -i :<port>`                                                    | Check open connections on a port  |
| `kill -9 $(lsof -t -i :<port>)`                                      | Kill active processes on the port |
| `valgrind --leak-check=full --track-fds=yes ./ircserv <port> <pass>` | Memory + file descriptor check    |


## 👨‍💻 Author
  
- [machouba](https://github.com/Machoub) 
- [gdoubrem](https://github.com/GinoDbm)
- [ayoubkhm](https://github.com/ayoubkhm)
42 Paris 

## Ressources Utilisées

- [Documentation officielle de l'IRC](https://tools.ietf.org/html/rfc2812)
- [Documentation des sockets en C++](https://www.boost.org/doc/libs/1_76_0/doc/html/boost_asio.html)
- [Tutoriel sur les sockets Unix](https://beej.us/guide/bgnet/)
