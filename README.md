<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chatbot</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      height: 100vh;
      transition: background 0.3s, color 0.3s;
    }
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px;
      background: #4CAF50;
      color: white;
    }
    #chatbox {
      flex: 1;
      padding: 10px;
      overflow-y: auto;
    }
    .user, .bot {
      margin: 5px 0;
      padding: 8px 12px;
      border-radius: 12px;
      max-width: 70%;
    }
    .user {
      background: #4CAF50;
      color: white;
      margin-left: auto;
    }
    .bot {
      background: #ddd;
      color: black;
      margin-right: auto;
    }
    #inputArea {
      display: flex;
      border-top: 1px solid #ccc;
    }
    #inputArea input {
      flex: 1;
      padding: 10px;
      border: none;
    }
    #inputArea button {
      padding: 10px;
      border: none;
      background: #4CAF50;
      color: white;
      cursor: pointer;
    }
    .dark {
      background: #222;
      color: white;
    }
    .dark .bot {
      background: #444;
      color: white;
    }
    .dark .user {
      background: #008CBA;
    }
    .toggle-btn {
      background: white;
      color: #4CAF50;
      border: none;
      padding: 5px 10px;
      border-radius: 6px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
    <h2>Chatbot</h2>
    <button class="toggle-btn" onclick="toggleMode()">🌙</button>
  </header>
  <div id="chatbox"></div>
  <div id="inputArea">
    <input type="text" id="userInput" placeholder="Savolingizni yozing..." onkeydown="if(event.key==='Enter'){sendMessage()}">
    <button onclick="sendMessage()">Yuborish</button>
  </div>

  <script>
    const chatbox = document.getElementById('chatbox');
    const userInput = document.getElementById('userInput');
    const toggleBtn = document.querySelector('.toggle-btn');

    const rules = {
      "salom": "Salom, xush kelibsiz!",
      "qalesan": "Yaxshi, rahmat! Sizchi?",
      "isming nima": "Men chatbotman.",
      "rahmat": "Arzimaydi 🙂"
    };

    function sendMessage() {
      const text = userInput.value.trim();
      if (!text) return;
      addMessage(text, "user");
      userInput.value = "";
      setTimeout(() => {
        const reply = getBotReply(text.toLowerCase());
        addMessage(reply, "bot");
      }, 500);
    }

    function addMessage(text, sender) {
      const msg = document.createElement("div");
      msg.className = sender;
      msg.innerText = text;
      chatbox.appendChild(msg);
      chatbox.scrollTop = chatbox.scrollHeight;
    }

    function getBotReply(text) {
      for (let key in rules) {
        if (text.includes(key)) return rules[key];
      }
      return "Kechirasiz, tushunmadim.";
    }

    function toggleMode() {
      document.body.classList.toggle("dark");
      if (document.body.classList.contains("dark")) {
        toggleBtn.textContent = "🌞";
        localStorage.setItem("mode", "dark");
      } else {
        toggleBtn.textContent = "🌙";
        localStorage.setItem("mode", "light");
      }
    }

    window.onload = () => {
      if (localStorage.getItem("mode") === "dark") {
        document.body.classList.add("dark");
        toggleBtn.textContent = "🌞";
      }
    };
  </script>
</body>
</html>
