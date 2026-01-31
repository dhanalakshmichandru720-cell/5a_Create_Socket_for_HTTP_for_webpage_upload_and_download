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
import socket

def download_file(host, port, filename):
    req = f"GET /{filename} HTTP/1.1\r\nHost: {host}\r\nConnection: close\r\n\r\n"

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(req.encode())

        response = b""
        while True:
            data = s.recv(4096)
            if not data:
                break
            response += data

    body = response.split(b"\r\n\r\n", 1)[1]

    out = f"downloaded_{filename}"
    with open(out, "wb") as f:
        f.write(body)

    print(f"File '{filename}' downloaded successfully as '{out}'")

if __name__ == "__main__":
    download_file("127.0.0.1", 8080, "example.txt")
```
## OUTPUT
<img width="1093" height="131" alt="Screenshot 2026-01-31 203436" src="https://github.com/user-attachments/assets/1639f9cb-be14-4d9f-864f-f039e3851266" />
<img width="1178" height="166" alt="Screenshot 2026-01-31 203424" src="https://github.com/user-attachments/assets/f9fc6110-fdcf-43b6-952f-a8c5f0762c4a" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
