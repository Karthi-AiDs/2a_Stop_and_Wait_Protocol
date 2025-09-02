# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

### Client.py
```
import socket
import time

# Create client socket
client = socket.socket()
client.connect(("localhost", 9999))

frame_size = int(input("Enter number of frames to send: "))

for i in range(frame_size):
    frame = "Frame " + str(i + 1)
    client.send(frame.encode())
    print("Sent:", frame)

    # Wait for ACK
    ack = client.recv(1024).decode()
    print("Received:", ack)
    time.sleep(1)

# End connection
client.send("exit".encode())
client.close()


```

### server.py

```
import socket

# Create server socket
server = socket.socket()
server.bind(("localhost", 9999))
server.listen(1)

print("Server is waiting for connection...")
conn, addr = server.accept()
print("Connected with:", addr)

while True:
    frame = conn.recv(1024).decode()
    if frame == "exit":
        print("Connection closed by client.")
        break
    print("Received Frame:", frame)
    
    # Send ACK back to client
    ack = "ACK for " + frame
    conn.send(ack.encode())

conn.close()
server.close()


```
## OUTPUT

### client side
<img width="945" height="454" alt="image" src="https://github.com/user-attachments/assets/d4eb3b15-76af-47c9-b646-4c27e2d2f483" />

### server side
<img width="791" height="371" alt="image" src="https://github.com/user-attachments/assets/de7699a3-d983-402d-ad2f-d469ac6dbb21" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
