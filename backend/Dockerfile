FROM python:3.10-slim

WORKDIR /app

RUN echo "from http.server import BaseHTTPRequestHandler, HTTPServer
import socket
class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        hostname = socket.gethostname()
        self.send_response(200)
        self.send_header('Content-type','text/html')
        self.end_headers()
        self.wfile.write(f'Served by {hostname}'.encode())
server = HTTPServer(('0.0.0.0', 8080), Handler)
server.serve_forever()" > server.py

EXPOSE 8080

CMD ["python", "server.py"]
