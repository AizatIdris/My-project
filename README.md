`MUHAMMAD HARIZ AIZAT BIN IDRIS [2022461302] [M3CDCS2554A]`
# HOW TO SEND AND RECEIVE UDP PACKET USING PYTHON *[SOCKET PROGRAMMING]*
------------------------------------------------------------------------

## `What is socket programming?`  
One method of establishing a communication channel between two nodes on a network is using socket programming. As one socket (node) reaches out to the other to establish a connection, the other socket listens on a specific port at an IP. As the client connects to the server, the server creates the listener socket.  

### Element in Socket Programming  
* socket() - `Command to create socket`. It requires arguments that define the protocol (often 0 by default), socket type (like SOCK_DGRAM for UDP or SOCK_STREAM for TCP), and address family (like AF_INET for IPv4).
* bind() -  `Command to associate a socket with a specific IP address and port number`. It is typically used by servers to bind to a well-known port so that clients can connect to it.
* listen() - `Comamand to put socket into listening mode`. This command is used in server code.
* accept() - `Command use for server accept request from clients`. It returns a new socket object and the address of the client connecting to the server.
* connect() - `Command to establish connection to the server`.  It takes the server's IP address and port number as parameters.
* send() - `Command to send data over connected socket`. It takes the data to be sent as a parameter and returns the number of bytes sent.
* recv() -`Command to receive data from connected socket`.  It takes the maximum amount of data to be received as a parameter and returns the received data.
* close() - `Command to close socket`. It releases the resources associated with the socket and terminates the connection.

 ## Different between TCP and UDP  
 |TCP|UDP|
 |----|----|
 |connection-oriented protocol|connectionless protocol|
 | used for applications where data integrity and order are crucial|used for applications where speed and efficiency are more important than reliability|
 |has higher overhead and latency|has minimal overhead|



## Server Code  
----------------------------------------------------------------------  

```
import socket

//Define the server IP address and port
SERVER_IP = "192.168.0.108"
SERVER_PORT = 4010

//Create a UDP socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

//Bind the socket to the IP address and port
server_socket.bind((SERVER_IP, SERVER_PORT))

print("UDP server is running on {}:{}".format(SERVER_IP, SERVER_PORT))

//Receive messages from clients
while True:
    # Receive message and client address
    message, client_address = server_socket.recvfrom(1024)
    
// Print the received message and client address
    print("Received message from {}: {}".format(client_address, message.decode()))
    
// Acknowledge the receipt of the message
    response = "Message received by server"
    server_socket.sendto(response.encode(), client_address)

// Welcome message for the client
    print("Welcome UDP client at {}".format(client_address))
//close socket
    server_socket.close();
```  
## Client code  
-----------------------------------------------------  
```
import socket

//Define the server IP address and port
SERVER_IP = "192.168.0.108"
SERVER_PORT = 4010

//Create a UDP socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

//Send messages to the server
while True:
    message = input("Enter message to send to server (type 'exit' to quit): ")
    if message.lower() == 'exit':
        break
    
// Send message to server
    client_socket.sendto(message.encode(), (SERVER_IP, SERVER_PORT))
    
// Receive acknowledgment from server
    response, server_address = client_socket.recvfrom(1024)
    print("Server response:", response.decode())

//Close the socket
client_socket.close()
```

