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
server
```
import socket

s = socket.socket()
s.connect(('localhost', 8001))

print("Connected to client")

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

f = s.makefile('r')

s.sendall(f"{n}\n{w}\n".encode())

for i in range(0, n, w):
    count = min(w, n - i)

    for j in range(count):
        frame = i + j + 1
        s.sendall(f"{frame}\n".encode())
        print("Frame sent:", frame)

    ack = f.readline().strip()
    print("Acknowledgement:", ack)

s.close()
```
client
```

import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(1)

print("Waiting for connection...")
c, addr = s.accept()
print("Connected!")

f = c.makefile('r')

n = int(f.readline())
w = int(f.readline())

for i in range(0, n, w):
    count = min(w, n - i)

    for j in range(count):
        frame = f.readline().strip()
        print("Received Frame:", frame)

    c.sendall("ACK Received\n".encode())

c.close()
s.close()
```
## OUPUT
<img width="1081" height="382" alt="image" src="https://github.com/user-attachments/assets/f3ece352-644f-4087-ac81-600d4d4f76b3" />
<img width="1140" height="300" alt="image" src="https://github.com/user-attachments/assets/ad5fa3bd-9022-4a46-9381-decf4872c0b6" />
## Result
Thus, python program to perform stop and wait protocol was successfully executed.

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
