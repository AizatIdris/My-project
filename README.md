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
SERVER_IP = "192.168.47.130"  //server IP address
SERVER_PORT = 4010

 //Create a UDP socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server_socket.bind((SERVER_IP, SERVER_PORT))

print(f"UDP server up and listening on {SERVER_IP}:{SERVER_PORT}")

while True:
    //Receive message from client
    message, client_address = server_socket.recvfrom(1024)
    print(f"Connection from {client_address}")
    print(f"Message from client: {message.decode()}")

    //Acknowledge receipt of the message
    ack_message = "Message received"
    server_socket.sendto(ack_message.encode(), client_address)
    print(f"Acknowledgment sent to {client_address}")


```    
## Client code  
-----------------------------------------------------  
```
import socket

//Define the server IP address and port
SERVER_IP = "192.168.47.130"  # Connect to server IP address
SERVER_PORT = 4010

//Create a UDP socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

while True:
    //Get message from user
    message = input("Enter message to send to server (type 'exit' to quit): ")
    if message.lower() == 'exit':
        break
    
    //Send message to server
    client_socket.sendto(message.encode(), (SERVER_IP, SERVER_PORT))
    
    //Receive acknowledgment from server
    response, server_address = client_socket.recvfrom(1024)
    print(f"Server response: {response.decode()}")

//Close the socket
client_socket.close()

```
### SAMPLE INPUT OUTPUT  
---------------------------------------------------------------  

 `Server.py `  
 
 ![git1copy](https://github.com/AizatIdris/My-project/assets/166004721/3112cf52-67ad-45fa-88eb-11b15f2a0e23)  
 `Client.py`  
 
 ![git2copy](https://github.com/AizatIdris/My-project/assets/166004721/3cdbfc1e-8dd7-433b-8491-68ccd5c3b7d7)  
 `Input Client.py`  
 
![git3copy](https://github.com/AizatIdris/My-project/assets/166004721/44abd43c-565c-4aee-b30f-a8e630725d76)  
`Output Server.py`  

![git4copy](https://github.com/AizatIdris/My-project/assets/166004721/890edf2d-32e2-4e06-9fae-1e75d149f76b)  

### VIDEO DEMONSTRATION  






