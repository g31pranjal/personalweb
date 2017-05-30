---
title : "Hearts over TCP network"
date : 2017-04-20T20:00:00Z+0530
startdate : 2017-03-23T16:00:00Z+0530
desc : A synchronous, multi-player, multi-level game of cards that can be played over TCP network.
author : in-arena
keyword : computer networks, internet, TCP, cards, game, hearts
layout : projectTemplate
---

*This was done as a term project for the partial fulfillment of course 'Computer Networks'*

*In case, you want a little background, <a href="https://en.wikipedia.org/wiki/Hearts">https://en.wikipedia.org/wiki/Hearts</a>*

Based on the server-client paradigm, the game requires a server to listen to a TCP port for incoming connections while the client modules bind to the server at the specified address. 

The server is capable of handling clients till a definite memory space, after which it rejects the connection, till it has room for connecting new incoming connections. An instance of game can be played by exactly 4 players, while multiple instances of game can be created and run simultaneously by the server. Each instance is a spawned child process of the parent server process with the connection details of its players. We say this child process, a **'Game room'**.

### # Game room 

The Game Room is responsible for dealing with the players. The communication is simple. Each communication to any of the client module follows the following paradigm : 
1. **COMMAND** : It is an integer number that is used to indicate the action required by the server. The command can mean a simple message, requiring some information from the end-player or conveying some information from some other player. Each command has a specific action sequence in the client and may carry a chunk of data.
1. **DATA** : If the command requires some data to be sent to the server or received from the server, by client, then it is done accordingly. 

The server communicates data between players by a sequence of commands. Each client is expected to respond accordingly to each command, as required. 

### # Client module

The client module is implemented as a Definite Finite Automata (DFA), which moves between states at the advent of a command by the server. DFA perfectly ensures a proper and correct flow of game and simplifies implementation of the game logic to a great extent. We have also tried to handle errors by means of the DFA, wherein any unexpected signals from the server or unrecognised assosiated data is dealt with appropriate actions. 

<img style="width: 100%;padding: 1% 4% 4% 4%" src="/assets/img/proj-net-1.png" />
   
### # Structural design and implementation

The game will require proper synchronisation between the turns of players, handling connection drops. Highlights of the game are as follows :

- **4 users have to play at a time on different machines**
	1. 4 players will have to connect to the server. If more than 4 players request for a connection, a new game room will get created for other players, in multiples of 4. All the users should be connected to a common network. 

- **Card distribution**
	1. Cards are distributed randomly by the servers. 
	2. They have been numbered from 1 to 52, where first set of 13 cards being of Clubs, followed by Diamond, Hearts, and Spade.

- **Score of each user, each player move, handling game levels**
	1. Score of each user is maintained on the server. The card set is also stored on the server as well as on the respective client. This has been done to ensure fair gameplay on the side of server.  
	2. As one level ends, the user gets upgraded to play the next level. At the end of the three levels, the overall winner is declared. 
	3. As per the signalling, each player has to wait until his chance comes. He will be updated as per whose chance is going on, and what card he/she has played. This signaling is well-handled using the DFA.

- **Levels and Rounds**
	1. There are 3 levels, with increasing level of difficulty, with each level having 13 rounds. 
	2. The rounds progress sequentially, with each player waiting for 3 other players to play their turn and playing its own turn in a pre-defined order. 
	3. At the end of each round, the server update points scored by all the players in a particular round, also total cumulative score till that round.
	4. Scores are maintained at server for each round and levels consequently. The scores are sent to clients at the end of each round.
	5. The server also ensures fair play in game. The client checks if the card played by the player is a valid move based of the previous cards played by other players. This is cross checked at server. The server also notes the sequence of cards played and the collection of cards at hand for each player. 

- **Description of Levels:**
	1. Level I: Vanilla version of Hearts. No special rules. 
	2. Level II: Each player has to pass two of its cards to the adjacent player in the beginning of the round. Hence, the player can pass its “risky” cards to its opponent. Post this change in hands, the normal gameplay continues.
	3. Level III: In addition to the rules added in Level II, three new rules are added here:
		1. The first card of a round can’t be of Hearts deck, until some points have been scored by any player.
		2. The Queen of Club, which earlier had no points, now has (-10) points. This reduces the player points and hence, must be sought for.
		3. If a player gets both, The Queen of Hearts and The Queen of Spades, then the total points are nullified, i.e., -14 points are awarded.

### # Possible improvements 
- We can involve flexible player requirements in a game room. 
- An AI-based bot to play against a player.
- Better error handling and recovery.
- Reduced communications between the server and client.

### <i class="fa fa-github"></i>&nbsp;Github
<a href="https://github.com/g31pranjal/online-hearts" target="_blank">https://github.com/g31pranjal/online-hearts</a>

### # made with passion by an awesome team :)
- Akshit Bhatia, Neel Kasat, Rishabh Jain and, me ! at BITS Pilani.
