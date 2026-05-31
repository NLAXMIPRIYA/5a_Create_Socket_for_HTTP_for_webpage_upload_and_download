# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
```
server.py



import socket

s = socket.socket()
s.bind(("localhost",3024))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()




client.py




import socket

s = socket.socket()
s.connect(("localhost",3024))

ch = input("1.Download 2.Upload : ")

if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()




index.html


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <p>hello world</p>
</body>
</html>





```
## OUTPUT
# For Download Option 
server side



<img width="1399" height="352" alt="image" src="https://github.com/user-attachments/assets/ea04103c-5283-46bc-a586-4e9563e70453" />





client side




<img width="1210" height="429" alt="image" src="https://github.com/user-attachments/assets/1656496e-92bc-4cae-ad0a-f462195e14da" />





# For Upload Option



server side



<img width="1355" height="344" alt="image" src="https://github.com/user-attachments/assets/4acc503d-9089-4609-858c-d7db7cfd8dfd" />



client side




<img width="1117" height="187" alt="image" src="https://github.com/user-attachments/assets/2022b553-b253-492b-aecd-c6d3b852289b" />


upload.txt

Earn the surreal life that comes in your real dreams..


## Result
Thus the socket for HTTP for web page upload and download created and Executed
