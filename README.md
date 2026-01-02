# ☾ Midnight Chat

> A full-stack, real-time collaboration suite built from scratch using Raw Java Sockets and Native WebSockets. No external frameworks.

![Java](https://img.shields.io/badge/Backend-Java_Sockets-orange)
![JavaScript](https://img.shields.io/badge/Frontend-Vanilla_JS-yellow)
![Protocol](https://img.shields.io/badge/Protocol-WebSockets_(RFC_6455)-blue)

## 📖 About
Midnight Chat is a robust communication platform designed to demonstrate low-level networking concepts. Unlike typical chat apps that rely on libraries like Socket.io or Firebase, this project implements the WebSocket protocol manually on the backend.

It features a split-view interface for simultaneous group and private messaging, along with a real-time collaborative whiteboard for visual teamwork.

## ✨ Key Features

### 💬 Communication
* **Real-Time Group Chat:** Instant messaging with custom usernames.
* **Split-View Private Messaging:** Whisper to specific users in a dedicated side-window without leaving the group chat.
* **Rich Media Support:** Drag-and-drop image sharing (handled via binary WebSocket frames).
* **Markdown Support:** Text formatting for **bold**, *italics*, and `code blocks`.

### 🎨 Collaboration (Whiteboard)
* **Live Drawing:** Multi-user canvas synchronization.
* **Tooling:** Color selection, dynamic brush size slider, and eraser tool.
* **Export:** Save your collaborative sketches as PNG files.

### 💎 UI/UX
* **Midnight Theme:** A modern dark mode aesthetic using CSS variables.
* **Glassmorphism:** Translucent, blurred sidebars and headers.
* **Responsive Design:** Flexbox layout that adapts to different window sizes.

## 🛠️ Tech Stack

### Backend (Java)
* **`ServerSocket` & `Socket`:** For handling raw TCP connections.
* **Multi-threading:** `Runnable` ClientHandlers to support multiple concurrent users.
* **Custom Protocol:** Manually implements the WebSocket Handshake and Frame Decoding/Encoding (including support for 64-bit large payloads for images).

### Frontend (Web)
* **HTML5 & CSS3:** Modern Flexbox layout and CSS animations.
* **Vanilla JavaScript:** Native `WebSocket` API for bi-directional communication.
* **HTML5 Canvas API:** For the drawing board logic.

## 🚀 Getting Started

### Prerequisites
* Java Development Kit (JDK) 8 or higher.
* A modern web browser (Chrome, Firefox, Edge).

### Installation
1.  **Clone the repository**
    ```bash
    git clone [https://github.com/yourusername/midnight-chat.git](https://github.com/yourusername/midnight-chat.git)
    cd midnight-chat
    ```

2.  **Compile the Java Server**
    ```bash
    javac *.java
    ```

3.  **Run the Server**
    ```bash
    java ChatServer
    ```
    *You should see: `Chat server started on port 5000`*

4.  **Launch the Client**
    * Open `index.html` in your web browser.
    * (Optional) Open it in multiple tabs to test the multi-user functionality.

## 🧩 Architecture Overview

1.  **Handshake:** The server listens on Port 5000. When a browser connects, the server reads the HTTP GET request, computes the `Sec-WebSocket-Accept` key, and upgrades the connection to WebSocket.
2.  **Framing:** All messages (Text and Binary) are decoded byte-by-byte according to RFC 6455 standards. This includes handling masking keys and variable payload lengths.
3.  **Routing:** * `DRAW|...` commands are broadcasted to update the canvas.
    * `PRIV|...` commands are routed to specific client threads.
    * `IMG|...` commands serve Base64 image data.
  
#note:
*To use in your browser, please allow insecure content.*
