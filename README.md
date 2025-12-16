index.html:

<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <title>Kerstkaart</title>
</head>
<body>

<canvas id="canvasId" width="800" height="600" style="border:1px solid black;"></canvas>
<script src="main.js" defer></script>
</body>
</html>



Main.js:


  const canvas = document.getElementById("canvasId");
const g = canvas.getContext("2d");


g.fillStyle = "#b3e5fc";
g.fillRect(0, 0, canvas.width, canvas.height);

const now = new Date();
const hour = now.getHours();
const lightsOn = hour >= 18;

function drawBall(x, y) {
    const colors = ["red", "blue", "yellow", "pink", "orange", "purple"];
    const color = colors[Math.floor(Math.random() * colors.length)];

   g.beginPath();
    g.arc(x, y, 8, 0, Math.PI * 2);
    g.fillStyle = color;
    g.fill();
}

function drawTree(x, y) {
    g.fillStyle = "brown";
    g.fillRect(x + 40, y + 120, 20, 50);

   const gradient = g.createLinearGradient(0, y, 0, y + 120);
    gradient.addColorStop(0, "green");
    gradient.addColorStop(1, "green");

   g.beginPath();
    g.moveTo(x, y + 120);
    g.lineTo(x + 50, y);
    g.lineTo(x + 100, y + 120);
    g.closePath();
    g.fillStyle = gradient;
    g.fill();
    g.beginPath();
    g.arc(x + 50, y - 10, 7, 0, Math.PI * 2);
    g.fillStyle = "gold";
    g.fill();
    for (let i = 0; i < 8; i++) {
        const ballX = x + 20 + Math.random() * 60;
        const ballY = y + 30 + Math.random() * 70;
        drawBall(ballX, ballY);
    }
}

function drawHouse(x, y) {
    g.fillStyle = "#ffcc80";
    g.fillRect(x, y, 80, 60);
    g.beginPath();
    g.moveTo(x, y);
    g.lineTo(x + 40, y - 40);
    g.lineTo(x + 80, y);
    g.closePath();
    g.fillStyle = "#d84315";
    g.fill();
    g.fillStyle = lightsOn ? "yellow" : "#90caf9";
    g.fillRect(x + 10, y + 20, 15, 15);
    g.fillRect(x + 55, y + 20, 15, 15);
}
drawTree(350, 250);

for (let i = 0; i < 4; i++) {
    const houseX = Math.random() * 650;
    const houseY = 420 + Math.random() * 50;
    drawHouse(houseX, houseY);
}
g.fillStyle = "darkred";
g.font = "36px Arial";
g.fillText("Merry Christmas", 250, 560);

