# Multithreaded Dictionary Server Implemented through Java
This repository contains the code of the Java based Multithreaded Dictionary Server-Client Application. This is implemented through Socket Programming. Swing is used to implement the GUI for the server, client and the dictionary.

# Context

The server, being multithreaded, can support multiple concurrent clients and is able to handle multiple requests at the same time. A GUI based client application is also provided which can connect with the server and provide some operations. Server supports multiple operations like searching words, adding words and definitions of the words, updating word’s definition and deletion of words and their meanings. The server is designed in a way to handle same requests from different clients at the same time without raising clashes. The server and client are both equipped with any failures that may happen during the course of their operation. A custom protocol has also been setup to establish communication between the client and server.

# Components

My project has three components. 
1.	Multithreaded Dictionary Server Application (GUI) that provides multithreading per connection (threads per connection)
2.	Dictionary Client Application (GUI)
3.	Dictionary (File and GUI).

GUI based Server Application first launches the Server’s GUI window. That window asks for the port to start the server on. Once it receives the port, it starts the server and launches a main thread on which the server listens. This means that the server application can be extended to include multiple servers features to launch different servers on different ports at the same time from the same GUI.  That main thread listens for connections. Once it receives a connection request from a client, it processes that connection request and launches a child thread that is dedicated for that connection. The client then can perform different operations which are. 
1.	Search the word
2.	Add a new word and its meaning to the dictionary 
3.	Add a new meaning to a word that is already available in the dictionary. 
4.	Update the meanings of the word. 
5.	Delete the word.
Each operation is followed by saving the changes to the file. This is done so that every client always has the most up-to-date information even when that information that is just recently added or updated. The protocol of communication is implemented using Strings. All the operations and the data are passed through strings to the server and the server sends the status of the operation and the result through the strings as well. The operation and the data are sent as a single string to eliminate the mismatch of operations and data. Both, server and client, are programmed to segregate the control part and data part from the strings. Finally, when the clients want to disconnect, it can just close its application which lets the server know that client has closed the connection, so server also closes the connections from its side and deletes the thread that it had associated with the client. 

# Class Design

![image](https://user-images.githubusercontent.com/12232515/174495086-6e756b51-5732-47f7-88d2-8abc16ce4d80.png)

The ServerGUI is started up first. It has the main function and all the ServerGUI related code. Upon pressing the Connect button, an object of DictionaryServer class is created. DictionaryServer then spins up object of DictionaryDisplay class which creates the GUI for the dictionary. DictionaryServer class also creates the object of DictionaryServerMainThread. DictionaryServerMainThread creates the serversocket and listens for connection requests. Once client tries to connect with the Server it then creates the object of dictthreads class and create a seprate thread for that client. Dicthreads class then parse the requests according to the protocol mentioned below and performs each operations through the object of dictionary class. Dictionary class has all the methods for the allowed operations as well as the methods to read and write from the dictionary file. DictionaryServer class also use dictionary class to initialize the dictionary. 

![image](https://user-images.githubusercontent.com/12232515/174495108-d84251e4-dce4-48e1-9cba-6dbfb465829a.png)

Above UML diagram shows the class structure for the client. ClientGUI class has the main function. This class calls the functions from the DictionaryClient, which has all the operation functions along with the sending and receiving data function, when the operator buttons are clicked on the client GUI application

# Protocol

Following protocol has been implemented between the client and the server.
* For Add operation
  - Client - > Server: “write@Word@Meaning” 
  - Server - > Client:
    - In case of success: status(success)@Meaning1@Meaning2@...MeaningN
    - In case of failure: status(failure)@StatusMessage
* For Delete operation
  - Client-> Server: “delete@Word”
  - Server - > Client:
    - In case of success: status(success)@StatusMessage
    - In case of failure: status(failure)@StatusMessage
* For update operation:
  - Client - > Server: “update@Word@Meaning”
  -	Server - > Client:
    *	In case of success: status(success)@Meaning1@Meaning2@...MeaningN
    *	In case of failure: status(failure)@StatusMessage
* For Search operation:
  - Client -> Server: “read@Word”
  - Server - > Client:
    -	In case of success: status(success)@Meaning1@Meaning2@...MeaningN
    -	In case of failure: status(failure)@StatusMessage
* For Disconnect operation:
  - Client -> Server: “Disconnect”

# GUI
The GUI is implemented in the following way
## Server
![image](https://user-images.githubusercontent.com/12232515/174496443-2e4141d2-2e99-4bb5-b04e-b91f4b1843e6.png)

As shown in the pic, the Server GUI contains a textField to get the port number. There is a connect button to connect to the server running at localhost. There is a logs portion which shows the logs of every user along with the status messages from the server. Important exceptions are shown through the Message box while and shown in the logs as well. The GUI also show the number of words in the dictionary and the number of clients connected. These numbers are updated on a real time basis. 

![image](https://user-images.githubusercontent.com/12232515/174496453-94b1fc2c-da46-44a4-86ea-38c67f935045.png)

![image](https://user-images.githubusercontent.com/12232515/174496458-12df59e9-3ce1-4296-b2bf-17d506bb98cb.png)

![image](https://user-images.githubusercontent.com/12232515/174496462-12bf3310-325c-4691-bb69-da25b79a9562.png)

The server also has a GUI of the Dictionary. All the words and their meanings are displayed over here. This GUI is updated on a real time basis. 

![image](https://user-images.githubusercontent.com/12232515/174496469-28063f4c-84c8-4ed4-94b4-45da90bf49da.png)

Above is the pic of client GUI. It indicates when the client is not connected with the server. 

![image](https://user-images.githubusercontent.com/12232515/174496483-b1e9aff0-3cb6-43c4-8fb7-f1d5105924d7.png)

![image](https://user-images.githubusercontent.com/12232515/174496488-d0feb187-7d27-4439-b6d6-828c8a9cd925.png)

![image](https://user-images.githubusercontent.com/12232515/174496490-40f19ef7-0927-49fa-b54f-6f5e9ab8b08a.png)

Above are the results of the search and write operations done through client application. The above diagrams are for reference. They don’t show all operations and errors handled by the Server and Client applications.


