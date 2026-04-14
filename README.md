# Index.C-C-python-

The AI chat box
# 🤖 AI Chatbox

A modern AI chat application inspired by ChatGPT with memory, voice support, and a clean UI.

## 🚀 Features
- 💬 Real-time AI chat  
- 🧠 Chat history & memory  
- 🎤 Voice input & output  
- 🔐 Secure backend API  
- 📱 Responsive designing system 

## 🛠️ Tech Stack
- Frontend: React.js, Tailwind CSS  
- Backend: Python (Flask/FastAPI)  
- Database: SQLite / MongoDB  

## ⚙️ Setup

```bash
git clone https://github.com/your-username/ai-chatbox.git
cd ai-chatbox

cd backend
pip install -r requirements.txt
python app.py

cd frontend
npm install
npm start

{ "message": "Hello AI" }

{ "response": "Hello! How can I help you?" }

---

If you want even **[shorter (like 3–4 lines for portfolio)](reference-followup:935)** or **[premium GitHub README with badges](reference-followup:981)**, tell me 

from flask import Flask, request, jsonify, render_template_string
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

# Simple memory
chat_history = []

# Frontend + Backend in ONE file
HTML_PAGE = """
<!DOCTYPE html>
<html>
<head>
<title>AI Chatbox</title>
<style>
body {
  font-family: Arial;
  background: #0f172a;
  color: white;
  margin: 0;
}
.container {
  max-width: 600px;
  margin: auto;
  padding: 20px;
}
.chat-box {
  height: 400px;
  overflow-y: auto;
  background: #1e293b;
  padding: 10px;
  border-radius: 10px;
}
.message {
  margin: 10px 0;
}
.user { color: #38bdf8; }
.ai { color: #34d399; }
.input-box {
  display: flex;
  margin-top: 10px;
}
input {
  flex: 1;
  padding: 10px;
  border-radius: 5px;
  border: none;
}
button {
  padding: 10px;
  margin-left: 5px;
  background: #6366f1;
  border: none;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
</style>
</head>

<body>
<div class="container">
  <h2>🤖👾👾 AI Chatbox</h2>

  <div class="chat-box" id="chat"></div>

  <div class="input-box">
    <input id="input" placeholder="Type a message..." />
    <button onclick="sendMessage()">Send</button>
  </div>
</div>

<script>
async function sendMessage() {
  const input = document.getElementById("input");
  const chat = document.getElementById("chat");

  const message = input.value;
  if (!message) return;

  chat.innerHTML += `<div class="message user">You: ${message}</div>`;
  input.value = "";

  const res = await fetch("/chat", {
    method: "POST",
    headers: {"Content-Type": "application/json"},
    body: JSON.stringify({message})
  });

  const data = await res.json();

  chat.innerHTML += `<div class="message ai">${data.response}</div>`;
  chat.scrollTop = chat.scrollHeight;
}
</script>
</body>
</html>
"""

@app.route("/")
def home():
    return render_template_string(HTML_PAGE)

@app.route("/chat", methods=["POST"])
def chat():
    data = request.json
    user_message = data.get("message")

    if not user_message:
        return jsonify({"error": "No message"}), 400

    # Dummy AI response (safe fallback)
    response = f"AI: You said '{user_message}'"

    chat_history.append({"user": user_message, "ai": response})

    return jsonify({
        "response": response,
        "history": chat_history
    })

if __name__ == "__main__":
    app.run(debug=True)
