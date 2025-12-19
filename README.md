#index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch Web App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="container">
    <h1>Stopwatch</h1>

    <div class="display" id="display">00:00:00</div>

    <div class="buttons">
        <button onclick="start()">Start</button>
        <button onclick="stop()">Stop</button>
        <button onclick="lap()">Lap</button>
        <button onclick="reset()">Reset</button>
    </div>

    <div class="laps">
        <h3>Lap Times</h3>
        <ul id="lapList"></ul>
    </div>
</div>

#style.css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
}

body {
    height: 100vh;
    background: linear-gradient(135deg, #1e1e2f, #2b2b4f);
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
}

.container {
    background: #121225;
    padding: 30px;
    border-radius: 15px;
    width: 320px;
    text-align: center;
    box-shadow: 0 10px 30px rgba(0,0,0,0.6);
}

h1 {
    margin-bottom: 20px;
}

.display {
    font-size: 36px;
    margin-bottom: 20px;
    letter-spacing: 2px;
}

.buttons {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
}

button {
    padding: 10px 15px;
    border: none;
    border-radius: 8px;
    background: #00f0ff;
    color: #000;
    font-weight: bold;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #00c0cc;
}

.laps {
    text-align: left;
    max-height: 150px;
    overflow-y: auto;
}

.laps ul {
    list-style: none;
}

.laps li {
    padding: 5px 0;
    border-bottom: 1px solid #444;
}

.buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
}

button {
    padding: 10px 14px;
    border: none;
    border-radius: 8px;
    background: #00f0ff;
    font-weight: bold;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #00c0cc;
}

#script.js
let timer = null;
let seconds = 0;
let minutes = 0;
let hours = 0;
let isRunning = false;

const display = document.getElementById("display");
const lapList = document.getElementById("lapList");

function updateDisplay() {
    display.innerText =
        (hours < 10 ? "0" : "") + hours + ":" +
        (minutes < 10 ? "0" : "") + minutes + ":" +
        (seconds < 10 ? "0" : "") + seconds;
}

function start() {
    if (!isRunning) {
        timer = setInterval(() => {
            seconds++;
            if (seconds === 60) {
                seconds = 0;
                minutes++;
            }
            if (minutes === 60) {
                minutes = 0;
                hours++;
            }
            updateDisplay();
        }, 1000);
        isRunning = true;
    }
}

function stop() {
    clearInterval(timer);
    isRunning = false;
}

function reset() {
    clearInterval(timer);
    isRunning = false;
    seconds = minutes = hours = 0;
    updateDisplay();
    lapList.innerHTML = "";
}

function lap() {
    if (isRunning) {
        const li = document.createElement("li");
        li.textContent = display.innerText;
        lapList.appendChild(li);
    }
}

<script src="script.js"></script>
</body>
</html>
