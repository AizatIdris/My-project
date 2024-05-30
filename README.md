`MUHAMMAD HARIZ AIZAT BIN IDRIS [2022461302] [M3CDCS2554A]`
# HOW TO SEND AND RECEIVE UDP PACKET USING PYTHON *[SOCKET PROGRAMMING]*
------------------------------------------------------------------------

## `What is socket programming?`  
One method of establishing a communication channel between two nodes on a network is using socket programming. As one socket (node) reaches out to the other to establish a connection, the other socket listens on a specific port at an IP. As the client connects to the server, the server creates the listener socket.  

# Server Code  
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

print("Server is listening on {}:{}".format(SERVER_IP, SERVER_PORT))

//Handle incoming messages
while True:
    //Receive data from client
    message, client_address = server_socket.recvfrom(1024)
    
    print("Connection established with:", client_address)
    print("Message from client:", message.decode())
    
    //Send acknowledgment to client
    response = "Message received"
    server_socket.sendto(response.encode(), client_address)

//Close the socket (unreachable code in this infinite loop example)
server_socket.close()
```
