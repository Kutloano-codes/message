<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Artsy Memories App</title>
<style>
    body {
        font-family: 'Comic Sans MS', cursive, sans-serif;
        background: repeating-linear-gradient(45deg, #ffe5e5, #ffe5e5 20px, #fff0f5 20px, #fff0f5 40px);
        min-height: 100vh;
        margin: 0;
        padding: 30px;
        text-align: center;
    }
    h1 { font-size: 2.5em; color: #ff4b2b; text-shadow: 2px 2px #ffe0b2; }
    input, button { padding: 10px; margin: 10px 0; border-radius: 10px; border: 2px solid #ff4b2b; font-size: 16px; outline: none; box-shadow: 2px 2px #ffd6a5; }
    input { width: 80%; max-width: 400px; }
    button { background: linear-gradient(45deg, #ff4b2b, #ff416c); color: white; cursor: pointer; transition: transform 0.2s; }
    button:hover { transform: scale(1.1); background: linear-gradient(45deg, #ff416c, #ff4b2b); }
    .memory, .secret { margin-top: 20px; padding: 20px; border-radius: 20px; font-size: 18px; max-width: 600px; margin-left: auto; margin-right: auto; box-shadow: 5px 5px #f0c27b; line-height: 1.5em; font-weight: bold; }
    .memory { background-color: #fff8e1; color: #ff6f00; border: 2px dashed #ffb74d; }
    .secret { background-color: #e0f7fa; color: #006064; border: 2px dashed #4dd0e1; }
</style>
</head>
<body>

<h1>🎨 Memories  🎨</h1>

<input type="text" id="name" placeholder="Enter your name"><br>
<button onclick="chooseMemory()">Next</button>

<div id="memoryChoice" style="display:none;">
    <p>Do you want to:</p>
    <button onclick="userMemory()">Tell your fondest memory</button>
    <button onclick="myMemory()">Let me tell you mine</button>
</div>

<div id="memoryDisplay"></div>

<div id="secretChoice" style="display:none; margin-top: 20px;">
    <p>Do you want to:</p>
    <button onclick="userSharesSecret()">I want to share my secret 🤫</button>
    <button onclick="iShareSecret()">I want to hear your secret 💌</button>
</div>

<div id="secretDisplay"></div>

<button id="downloadBtn" style="display:none;" onclick="downloadResponses()">💾 Download Responses</button>

<script>
let userName = "";
let responses = []; // store all responses

function chooseMemory() {
    userName = document.getElementById("name").value.trim();
    if (!userName) { alert("Please enter your name!"); return; }
    document.getElementById("name").style.display = "none";
    document.querySelector("button").style.display = "none";
    document.getElementById("memoryChoice").style.display = "block";
}

// User enters their own memory
function userMemory() {
    let memory = prompt("Please share your fondest memory:");
    if (memory) {
        displayMemory(memory);
        responses.push(`${userName} shared memory: ${memory}`);
        showSecretOptions();
    }
}

// Your memory function with special names
function myMemory() {
    let memoryText = ""; 
    const lowerName = userName.toLowerCase();

    if (lowerName === "thando") {
        memoryText = "💖 My fondest memory of us was when we were playing eFootball and you'd beat me. Well, I did not care as long as I did something that connected me to you... else I loved every moment I shared with you. 💖";
    } else if (lowerName === "lerato") {
        memoryText = "👭 Walking to school and back with you was amazing. I love you big sis, thank you for everything you are the best!";
    } else if (lowerName === "katleho") {
        memoryText = "🏡 Growing up and visiting Vrede you made it interesting. You'd take me with whenever you were going to your friends. Thank you for that Kat, I cherish every laughter and late night talks we had.";
    } else if (lowerName === "nhlanhla") {
        const options = [
            
            "😄 Thank you for being funny and kind and amazing! "
        ];
        const randomIndex = Math.floor(Math.random() * options.length);
        memoryText = "🎉 Growing up with you was amazing. " + options[randomIndex];
    } else {
        memoryText = "✨ My fondest memory of us is every little moment we spent laughing and connecting. ✨";
    }

    displayMemory(memoryText);
    responses.push(`Memory for ${userName}: ${memoryText}`);
    showSecretOptions();
}

// Display memory
function displayMemory(text) {
    const memoryDiv = document.getElementById("memoryDisplay");
    memoryDiv.innerHTML = `<div class="memory">${text}</div>`;
}

// Show secret options after memory
function showSecretOptions() {
    setTimeout(() => { document.getElementById("secretChoice").style.display = "block"; }, 300);
}

// User chooses to share their secret
function userSharesSecret() {
    const secret = prompt("Enter your secret:");
    if (secret) {
        displaySecret(secret);
        responses.push(`${userName} shared secret: ${secret}`);
    }
    document.getElementById("secretChoice").style.display = "none";
    document.getElementById("downloadBtn").style.display = "block"; // enable download
}

// User chooses to hear your secret
function iShareSecret() {
    const mySecret = "💌 My secret: For the first time in my life I don't want to die :)";
    displaySecret(mySecret);
    responses.push(mySecret);
    document.getElementById("secretChoice").style.display = "none";
    document.getElementById("downloadBtn").style.display = "block"; // enable download
}

// Display secret
function displaySecret(text) {
    const secretDiv = document.getElementById("secretDisplay");
    const div = document.createElement("div");
    div.className = "secret";
    div.innerText = text;
    secretDiv.appendChild(div);
}

// Download all responses
function downloadResponses() {
    const blob = new Blob([responses.join("\n")], {type: "text/plain"});
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = `memories_${userName}.txt`;
    link.click();
}
</script>

</body>
</html>
