# Multithreaded-Dictionary-Server-Java
This repository contains the code of the Java based Dictionary Server-Client Application. This is implemented through Socket Programming. Swing is used to implement the GUI for the server, client and the dictionary.

# Context

The server, being multithreaded, can support multiple concurrent clients and is able to handle requests at the same time. A GUI based client application is also required which can connect with the server and provide some operations. Server supports multiple operations like searching words, adding words and definitions of the words, updating word’s definition and deletion of words and their meanings. The server is designed in a way to handle same requests from different clients at the same time without raising clashes. The server and client are both equipped with any failures that may happen during the course of their operation. A custom protocol has also been setup to establish communication between the client and server. 
