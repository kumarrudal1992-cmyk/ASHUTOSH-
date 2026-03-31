<!DOCTYPE html>
<html>
<head>
    <title>GURUKUL AI</title>
    <style>
        body {
            font-family: Arial;
            text-align: center;
            color: white;
            background: radial-gradient(circle, rgba(255,140,0,0.2), #0f172a);
        }

        body::before {
            content: "🕉️";
            font-size: 200px;
            position: fixed;
            top: 30%;
            left: 40%;
            opacity: 0.1;
        }

        h1 {
            color: orange;
        }

        #chatbox {
            width: 60%;
            height: 400px;
            margin: auto;
            border: 2px solid orange;
            overflow-y: scroll;
            padding: 10px;
            background: rgba(0,0,0,0.6);
        }

        input {
            width: 50%;
            padding: 10px;
        }

        button {
            padding: 10px;
            background: orange;
            color: black;
            border: none;
            cursor: pointer;
        }
    </style>
</head>

<body>

<h1>🕉️ GURUKUL AI</h1>

<div id="chatbox"></div><br>

<input type="text" id="input" placeholder="Ask me anything...">
<button onclick="send()">Send</button>

<script>
function send() {
    let input = document.getElementById("input").value;
    let chatbox = document.getElementById("chatbox");

    if (!input) return;

    // Create message elements safely
    let userMsg = document.createElement("p");
    userMsg.innerHTML = "<b>You:</b> " + escapeHtml(input);
    chatbox.appendChild(userMsg);

    let reply = getReply(input.toLowerCase());

    setTimeout(() => {
        let aiMsg = document.createElement("p");
        aiMsg.innerHTML = "<b>Gurukul AI:</b> " + reply;
        chatbox.appendChild(aiMsg);
        chatbox.scrollTop = chatbox.scrollHeight;
    }, 400);

    document.getElementById("input").value = "";
}

function escapeHtml(text) {
    let map = {
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        '"': '&quot;',
        "'": '&#039;'
    };
    return text.replace(/[&<>"']/g, m => map[m]);
}

function getReply(input) {

    // Greeting
    if (input.includes("hello") || input.includes("hi")) {
        return "🙏 Namaste! I am Gurukul AI. How can I guide you today?";
    }

    // Emotion / Life advice
    if (input.includes("sad") || input.includes("depressed")) {
        return "😔 I understand your feelings. Life has ups and downs. Stay strong, you are capable of overcoming this.";
    }

    if (input.includes("happy")) {
        return "😊 That's wonderful! Keep spreading positivity and joy.";
    }

    if (input.includes("problem") || input.includes("life")) {
        return "🧠 Every problem has a solution. Stay calm, think wisely, and take one step at a time.";
    }

    // Motivation
    if (input.includes("motivate") || input.includes("motivation")) {
        return "🔥 Believe in yourself. Hard work and patience always bring success.";
    }

    // Math solving (safe alternative to eval)
    if (input.match(/^[\d+\-*/().\s]+$/)) {
        try {
            let result = Function('"use strict"; return (' + input + ')')();
            return "📘 Solution: " + result;
        } catch {
            return "❌ I cannot solve this math problem.";
        }
    }

    // Time & Date
    if (input.includes("time")) {
        return "⏰ Current time: " + new Date().toLocaleTimeString();
    }

    if (input.includes("date")) {
        return "📅 Today: " + new Date().toLocaleDateString();
    }

    // Default
    return "🤔 I am still learning. Please ask about maths, life, or emotions.";
}
</script>

</body>
</html>
