from http.server import SimpleHTTPRequestHandler, HTTPServer

class CustomHandler(SimpleHTTPRequestHandler):
    def end_headers(self):
        # Add the necessary headers for SharedArrayBuffer support
        self.send_header('Cross-Origin-Opener-Policy', 'same-origin')
        self.send_header('Cross-Origin-Embedder-Policy', 'require-corp')
        # Call the original end_headers method to finish sending headers
        super().end_headers()

# Set the port (e.g., 8000)
port = 8000
server_address = ('', port)

# Create the server
httpd = HTTPServer(server_address, CustomHandler)
print(f"Serving on port {port}...")

# Start the server
httpd.serve_forever()
