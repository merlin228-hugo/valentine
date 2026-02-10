# valentine
index.html
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Валентинка 💘</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: 'Arial', sans-serif;
    background: linear-gradient(135deg, #ff758c, #ff7eb3);
    overflow: hidden;
}

.container {
    position: relative;
    z-index: 10;
    background: white;
    padding: 30px;
    border-radius: 25px;
    max-width: 500px;
    width: 90%;
    margin: auto;
    top: 50%;
    transform: translateY(-50%);
    text-align: center;
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);
}

img {
    width: 100%;
    border-radius: 20px;
}

h1 {
    margin: 20px 0;
}

.buttons {
    position: relative;
    height: 120px;
}

button {
    position: absolute;
    padding: 18px 35px;
    font-size: 20px;
    border-radius: 50px;
    border: none;
    cursor: pointer;
    transition: all 0.3s ease;
}

#yesBtn {
    background: #ff3366;
    color: white;
    left: 50%;
    transform: translateX(-120%);
    animation: pulse 1.2s infinite;
    z-index: 2;
}

#noBtn {
    background: #ccc;
    left: 50%;
    transform: translateX(20%);
    z-index: 1;
}

@keyframes pulse {
    0% { transform: translateX(-120%) scale(1); }
    50% { transform: translateX(-120%) scale(1.1); }
    100% { transform: translateX(-120%) scale(1); }
}

.heart {
    position: fixed;
    bottom: -20px;
    font-size: 24px;
    animation: fly 6s linear infinite;
}

@keyframes fly {
    to {
        transform: translateY(-120vh);
        opacity: 0;
    }
}
</style>
</head>

<body>

<div class="container" id="card">
    <img id="cat" src="https://media.giphy.com/media/JIX9t2j0ZTN9S/giphy.gif">
    <h1 id="text">Екатерина, ты будешь моей валентинкой? 💖</h1>

    <div class="buttons">
        <button id="yesBtn">ДА</button>
        <button id="noBtn">НЕТ</button>
    </div>
</div>

<script>
const texts = [
    "Ну давай, мне грустно 😢",
    "Я старался вообще-то…",
    "Ну пожалуйста 🥺",
    "Это судьба 💘",
    "Я без тебя не смогу 😭"
];

const cats = [
    "https://media.giphy.com/media/JIX9t2j0ZTN9S/giphy.gif",
    "https://media.giphy.com/media/mlvseq9yvZhba/giphy.gif",
    "https://media.giphy.com/media/VbnUQpnihPSIgIXuZv/giphy.gif"
];

let clicks = 0;
const noBtn = document.getElementById("noBtn");
const yesBtn = document.getElementById("yesBtn");
const text = document.getElementById("text");
const cat = document.getElementById("cat");

function vibrate() {
    if (navigator.vibrate) navigator.vibrate(100);
}

noBtn.addEventListener("click", () => {
    vibrate();

    text.textContent = texts[Math.min(clicks, texts.length - 1)];
    cat.src = cats[Math.min(clicks, cats.length - 1)];

    // кнопка НЕТ убегает
    noBtn.style.left = Math.random() * 60 + "%";
    noBtn.style.top = Math.random() * 40 + "px";
    noBtn.style.transform = "scale(0.9)";

    // кнопка ДА растёт
    const scale = 1 + clicks * 0.4;
    yesBtn.style.transform = `translateX(-120%) scale(${scale})`;

    clicks++;

    if (clicks > 4) {
        noBtn.style.display = "none";
        yesBtn.style.position = "fixed";
        yesBtn.style.top = 0;
        yesBtn.style.left = 0;
        yesBtn.style.width = "100vw";
        yesBtn.style.height = "100vh";
        yesBtn.style.fontSize = "48px";
        yesBtn.style.borderRadius = "0";
    }
});

yesBtn.addEventListener("click", () => {
    document.body.innerHTML = `
        <div style="
            height:100vh;
            display:flex;
            justify-content:center;
            align-items:center;
            text-align:center;
            background:linear-gradient(135deg,#ff758c,#ff7eb3);
            color:white;
            font-size:36px;
            font-family:Arial;
        ">
            💘 УРААА 💘<br>
            Ты моя валентинка 😍
        </div>
    `;
});

// сердечки
setInterval(() => {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.textContent = "❤️";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.animationDuration = 4 + Math.random() * 4 + "s";
    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 8000);
}, 300);
</script>

</body>
</html>
