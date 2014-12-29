Project #2: Remote Working Ground (rwg).

Implement a shell conosle with server-client architecture and new pipe subsystem.

This shell console allows online users to communicate to each other. 
Some parts of this RWG are like RAS but more chat-like commands are implemented.

Commands [who], [tell], [yell], [name] are supported.

Format of command [tell]: 
   % tell (client id) (message)
   And the client will get the message with following format:
   *** (sender's name) told you ***: (message)
   
   e.g., Assume my name is 'IamUser'.
   [terminal of mine]
   % tell 3 Hello World.
   
   [terminal of client id 3]
   % *** IamUser told you ***: Hello World.

   If the client you want to send message to does not exist, print the following message:
   *** Error: user #(client id) does not exist yet. *** 
   
   e.g.,
   [terminal of mine]
   % tell 3 Hello World.
   *** Error: user #3 does not exist yet. *** 
   % 

Format of command [yell]: 
   % yell (message)
   All the clients will get the message with following format:
   *** (sender's name) yelled ***: (message)
   
   e.g., Assume my name is 'IamUser'.
   [terminal of mine]
   % yell Hi everybody
   
   [terminal of all clients]
   % *** IamUser yelled ***: Hi everybody
   
Format of command [name]: 
   % name (name)
   All the clients will get the message with following format:
   *** User from (IP/port) is named '(name)'. ***
   
   eg.
   [terminal of mine]
   % name IamUser
   
   [terminal of all clients]
   % *** User from 140.113.215.62/1201 is named 'IamUser'. ***
   
   Notice that the name CAN NOT be the same as the name which on-line users have,
   or you will get the following message:
   *** User '(name)' already exists. ***
   
   e.g.,
   Mike is on-line, and I want to have the name "Mike" too.
   
   [terminal of mine]
   % name Mike
   *** User 'Mike' already exists. ***
   % 
   
The output format of [who]:
   You have to print a tab between each of tags. 
   Notice that the first column does not print socket fd but client id.
   
   <ID>[Tab]<nickname>[Tab]<IP/port>[Tab]<indicate me>
   (1st id)[Tab](1st name)[Tab](1st IP/port)([Tab](<-me))
   (2nd id)[Tab](2nd name)[Tab](2nd IP/port)([Tab](<-me))
   (3rd id)[Tab](3rd name)[Tab](3rd IP/port)([Tab](<-me))
   ...   

   For example:
   % who 
   <ID>	<nickname>	<IP/port>	<indicate me>
   1	IamStudent	140.113.215.62/1201	<-me
   2	(no name)	140.113.215.63/1013
   3	student3	140.113.215.64/1302
   
   Notice that
   The client's id should be assigned in the range of number 1~30. 
   The server should always assign a smallest unused id to new connected client.
   
   eg.
   <new client login> // server assigns this client id = 1
   <new client login> // server assigns this client id = 2
   <client 1 logout>
   <new client login> // server assigns this client id = 1, not 3

