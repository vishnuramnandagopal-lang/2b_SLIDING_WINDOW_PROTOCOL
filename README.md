# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

## SERVER
~~~
import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(5)

c, addr = server.accept()

size = int(input("Enter number of frames to send: "))
l = list(range(size))

w = int(input("Enter Window Size: "))

i = 0

while i < len(l):
    st = i + w
    c.send(str(l[i:st]).encode())

    ack = c.recv(1024).decode()

    if ack:
        print(ack)
        i += w

c.close()
server.close()
~~~
## CLIENT
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    data = s.recv(1024).decode()

    if not data:
        break

    print(data)

    s.send("Acknowledgement received".encode())

s.close()
~~~

## OUPUT
<img width="474" height="215" alt="image" src="https://github.com/user-attachments/assets/1429689d-b0ba-408c-820e-440f6d261c6e" />
<img width="486" height="169" alt="image" src="https://github.com/user-attachments/assets/95201def-9717-4bf9-86c3-ffafd4e45a7f" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
