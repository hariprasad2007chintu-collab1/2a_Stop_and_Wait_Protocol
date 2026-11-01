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
```
import socket

s = socket.socket()
s.bind(('127.0.0.1', 5000))
s.listen(1)

print("Server waiting for connection...")

conn, addr = s.accept()
print("Client connected")

with conn:
    reader = conn.makefile('r')
    writer = conn.makefile('w')

    n = int(reader.readline())

    for i in range(1, n + 1):
        frame = reader.readline().rstrip('\n')

        print("Frame received:", frame)

        writer.write("ACK " + str(i) + "\n")
        writer.flush()

        print("ACK sent")

    print("All frames received successfully")

s.close()
```
### Client Program
```
import socket

s = socket.socket()
s.connect(('127.0.0.1', 5000))

n = int(input("Enter the number of frames: "))

s.sendall((str(n) + "\n").encode())

reader = s.makefile('r')

for i in range(1, n + 1):
    frame = input("Enter frame " + str(i) + ": ")

    s.sendall((frame + "\n").encode())

    ack = reader.readline().strip()

    print("Acknowledgement received:", ack)

print("All frames sent successfully")

s.close()
```
## OUTPUT
```
Server waiting for connection...
Client connected
Frame received: Hello
ACK sent
Frame received: World
ACK sent
Frame received: Python
ACK sent
All frames received successfully

Enter the number of frames: 3
Enter frame 1: Hello
Acknowledgement received: ACK 1
Enter frame 2: World
Acknowledgement received: ACK 2
Enter frame 3: Python
Acknowledgement received: ACK 3
All frames sent successfully
## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
