<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Impress Crush 💖</title>
<style>
    body {
        text-align: center;
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #ffdde1, #ee9ca7);
        margin: 0;
        padding: 0;
        overflow: hidden;
    }
    .heartImg {
        font-size: 80px;
        margin-top: 20px;
        animation: fadeIn 0.8s ease-in-out;
    }
    h1 {
        color: #ff1a75;
        margin: 20px;
        animation: fadeIn 0.8s ease-in-out;
    }
    button {
        font-size: 18px;
        padding: 10px 20px;
        margin: 10px;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    #yesBtn {
        background-color: #ff66b2;
        color: white;
    }
    #noBtn {
        background-color: #999;
        color: white;
        position: relative;
    }
    @keyframes fadeIn {
        from {opacity: 0;}
        to {opacity: 1;}
    }
    .heart {
        position: fixed;
        font-size: 20px;
        animation: floatUp 5s linear infinite;
        opacity: 0.6;
    }
    @keyframes floatUp {
        0% {transform: translateY(100vh);}
        100% {transform: translateY(-10vh);}
    }
</style>
</head>
<body>

<div id="heartSymbol" class="heartImg">❤️</div>
<h1 id="text">Will you be mine? 🥰</h1>

<button id="yesBtn" onclick="sayYes()">Yes</button>
<button id="noBtn" onclick="nextPhase()">No</button>

<script>
let phase = 0;
const phrases = [
    "Will You Be Mine? 🥰",
    "Ka Nhi G? 🥺",
    "Kiti Bhav Khanar 😢",
    "I Know You Love Me 😎 ",
    "Aikun Ghe Na Yaar ❤️",
    "Me Khup Prem Karto Tujhyavar 💕"
];

function nextPhase() {
    if (phase < phrases.length - 1) {
        phase++;
        document.getElementById("text").innerHTML = phrases[phase];
        document.getElementById("heartSymbol").innerHTML = "❤️";
    } else {
        runAwayNo();
    }
}

function runAwayNo() {
    const noBtn = document.getElementById("noBtn");

    function moveButton() {
        const x = Math.floor(Math.random() * (window.innerWidth - noBtn.clientWidth));
        const y = Math.floor(Math.random() * (window.innerHeight - noBtn.clientHeight));
        noBtn.style.position = "absolute";
        noBtn.style.transition = "left 0.2s, top 0.2s";
        noBtn.style.left = x + "px";
        noBtn.style.top = y + "px";
    }

    noBtn.addEventListener("mouseover", moveButton);
    noBtn.addEventListener("touchstart", moveButton);
}

function sayYes() {
    document.body.innerHTML = `
        <div style="font-size:120px; margin-top:40px;">❤️</div>
        <h1>I knew it ❤️ Love you too, Pramod!</h1>
    `;
    createHearts();
    sendNotification();
}

function sendNotification() {
    fetch("https://api.web3forms.com/submit", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            Accept: "application/json"
        },
        body: JSON.stringify({
            access_key: "YOUR_ACCESS_KEY_HERE",  // Replace with your Web3Forms Access Key
            subject: "She clicked YES! 💖",
            from_name: "Crush Website",
            message: "Your crush clicked YES on your page!"
        })
    }).then(res => res.json())
      .then(data => console.log(data))
      .catch(err => console.error(err));
}

function createHearts() {
    setInterval(() => {
        const heart = document.createElement("div");
        heart.classList.add("heart");
        heart.innerHTML = "💖";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.fontSize = Math.random() * 20 + 20 + "px";
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 5000);
    }, 300);
}
</script>

</body>
</html>
