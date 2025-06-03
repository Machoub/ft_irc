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
bash
Copier
Modifier
make         # Build the project
make clean   # Remove object files
make fclean  # Remove all binaries and object files
make re      # Recompile the project from scratch
⚠️ Compiled using C++98 with flags: -Wall -Wextra -Werror

🚀 Usage
bash
Copier
Modifier
./ircserv <port> <password>
<port>: the port on which the server will listen

<password>: required for any client trying to connect

Example:

bash
Copier
Modifier
./ircserv 6667 secret123
🧪 Supported IRC Commands
Command	Description
PASS	Authenticate with the server password
NICK	Set/change the nickname
USER	Register the username
JOIN	Join or create a channel
PRIVMSG	Send a message privately or to a channel
KICK	Kick a user from a channel (operator only)
INVITE	Invite a user to a channel
TOPIC	Set or view a channel topic
MODE	Set channel/user modes (e.g., operator privileges)

🧪 Testing & Tools
🔧 With netcat (basic)
bash
Copier
Modifier
nc <server_ip> <port>
Then manually send commands:

ruby
Copier
Modifier
PASS secret123
NICK Ayoub
USER ayoub 0 * :Ayoub Khamassi
JOIN #42
PRIVMSG #42 Hello, world!
💬 With irssi (recommended)
bash
Copier
Modifier
sudo apt install irssi  # or brew install irssi on macOS
Method 1 (interactive)
bash
Copier
Modifier
irssi
/connect 127.0.0.1 6667
Method 2 (one-liner)
bash
Copier
Modifier
irssi -c 127.0.0.1 -p 6667 -n Ayoub -w secret123
Commands inside irssi:
bash
Copier
Modifier
/join #42
/msg #42 hello everyone
🧪 Advanced Debug & Tools
Command	Purpose
lsof -i :<port>	Check open connections on a port
kill -9 $(lsof -t -i :<port>)	Kill active processes on the port
valgrind --leak-check=full --track-fds=yes ./ircserv <port> <pass>	Memory + file descriptor check

🧠 Tips for irssi
Open irssi raw log:

pgsql
Copier
Modifier
/RAWLOG OPEN ~/debug.log
Switch windows:

Alt + ←/→ or Esc + number

/window goto <number>

🔧 Set correct external IP for DCC:
bash
Copier
Modifier
/set dcc_own_ip <your_local_or_public_ip>
📁 File Transfer (Optional Bonus)
Using irssi (DCC)
bash
Copier
Modifier
/dcc send Pol /path/to/file.txt
/dcc get Raf file.txt
Using netcat
Sender (Raf):

bash
Copier
Modifier
nc -l 12345 < file.txt
Receiver (Pol):

bash
Copier
Modifier
nc <server_ip> 12345 > file.txt
🧪 Suspended Client Test (using netcat)
Start a client in a channel and suspend it:

bash
Copier
Modifier
Ctrl + Z
Send messages from other clients

Resume the suspended one:

bash
Copier
Modifier
fg %<job_id>
Messages received during suspension should appear if your server works correctly.

## 👨‍💻 Author
  
- [machouba](https://github.com/Machoub) 
- [gdoubrem](https://github.com/GinoDbm)
42 Paris 

## Ressources Utilisées

- [Documentation officielle de l'IRC](https://tools.ietf.org/html/rfc2812)
- [Documentation des sockets en C++](https://www.boost.org/doc/libs/1_76_0/doc/html/boost_asio.html)
- [Tutoriel sur les sockets Unix](https://beej.us/guide/bgnet/)
