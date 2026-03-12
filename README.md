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
## Server.py
~~~
mport socket

s = socket.socket()
s.bind(("localhost",8080))
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

  
~~~
## client.py
~~~
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
~~~
## cn.html
~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Page</title>
</head>
<body>
    <h1>Welcome to the Python HTTP Server!</h1>
    <p>This is the default page served by the server.</p>

</body>
</html>
~~~
## OUTPUT
## DOWNLOAD
<img width="809" height="95" alt="Screenshot 2026-03-12 084910" src="https://github.com/user-attachments/assets/7e7161ad-1ed7-431e-8dd5-dbb245e339cb" />
<img width="814" height="493" alt="Screenshot 2026-03-12 084637" src="https://github.com/user-attachments/assets/fd6c8a55-c08e-47bb-95cd-fcad116b869e" />

## UPLOAD
<img width="805" height="353" alt="Screenshot 2026-03-12 085245" src="https://github.com/user-attachments/assets/52573975-45d9-4166-9f36-6418994c241a" />
<img width="807" height="235" alt="Screenshot 2026-03-12 084811" src="https://github.com/user-attachments/assets/2108e4c3-12c1-4202-a1bd-7f0afdfd3798" />

## RESULT
Thus the socket for HTTP for web page upload and download created and Executed
