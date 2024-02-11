# Upload Image Server

## Introduction

The Upload Image Server is designed to facilitate easy debugging of cameras on robots by allowing for the quick and secure upload of images directly from the robot to the server.

## Getting Started

Install deps with poetry:

```bash
poetry install
```

### Running the Server

To start the server on your local machine, run:

```bash
poetry shell
python app.py
```

This will start the Flask server, typically listening on `http://localhost:5000`.

## Setting Up Public Access with ngrok

To allow access to your server from the internet, you can use ngrok, a tool that creates a secure tunnel to localhost. This is particularly useful for testing your server with real-world data without deploying it to a public server.

### Installing ngrok

1. Download ngrok from [https://ngrok.com/download](https://ngrok.com/download).
2. Follow the installation instructions on the website to set it up on your system.

### Using ngrok

After installing ngrok, you can expose your server to the internet with the following steps:

1. Open a new terminal window.
2. Navigate to the directory where ngrok is installed.
3. Start an ngrok tunnel to your server's port (default is 5000) using:

   ```bash
   ./ngrok http 5000
   ```

4. ngrok will display a UI in your terminal with the public URLs. You can use these URLs to access your server from anywhere.

## Uploading Images to the Server

To upload an image to the server, you can use a simple `curl` command, a Python script with the `requests` library, or any HTTP client of your choice.

### Using curl

```bash
curl -X POST -F "file=@/path/to/your/image.jpg" http://localhost:5000/upload
```

Replace `/path/to/your/image.jpg` with the actual path to your image.

### Using Python

```python
import requests

url = 'http://localhost:5000/upload'  # Replace with your ngrok URL if accessing publicly
file_path = '/path/to/your/image.jpg'

with open(file_path, 'rb') as file:
    files = {'file': (file.name, file)}
    response = requests.post(url, files=files)

print(response.text)
```
