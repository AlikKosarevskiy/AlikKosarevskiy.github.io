<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hill Car</title>
  <style>
    canvas {
      background: #cceeff;
      display: block;
      margin: auto;
    }
    #controls {
      text-align: center;
      margin-top: 10px;
    }
    button {
      font-size: 1.5em;
      padding: 10px 20px;
      margin: 5px;
    }
  </style>
</head>
<body>

<canvas id="gameCanvas" width="800" height="400"></canvas>
<div id="controls">
  <button id="gasBtn">Газ</button>
  <button id="brakeBtn">Тормоз</button>
</div>

<script>
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

let car = {
  x: 100,
  y: 0,
  vx: 0,
  vy: 0,
  width: 50,
  height: 20,
  rotation: 0,
  onGround: false
};

let gravity = 0.3;
let gas = false;
let brake = false;
let terrain = [];
let speed = 0.1;

// Генерация холмистой местности
for (let i = 0; i < 1000; i++) {
  terrain.push(300 + 50 * Math.sin(i * 0.1));
}

function drawCar() {
  ctx.save();
  ctx.translate(car.x, car.y);
  ctx.rotate(car.rotation);
  ctx.fillStyle = "red";
  ctx.fillRect(-car.width / 2, -car.height / 2, car.width, car.height);
  ctx.restore();
}

function drawTerrain() {
  ctx.beginPath();
  ctx.moveTo(0, terrain[0]);
  for (let i = 1; i < canvas.width; i++) {
    ctx.lineTo(i, terrain[Math.floor(car.x - canvas.width/2 + i)] || 400);
  }
  ctx.strokeStyle = "green";
  ctx.lineWidth = 2;
  ctx.stroke();
}

function gameLoop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  let index = Math.floor(car.x);
  let terrainY = terrain[index] || 400;

  car.vy += gravity;

  if (gas) car.vx += speed;
  if (brake) car.vx -= speed * 1.2;

  car.x += car.vx;
  car.y += car.vy;

  // Поворот машины при наклоне дороги
  let y1 = terrain[index - 1] || terrainY;
  let y2 = terrain[index + 1] || terrainY;
  let angle = Math.atan2(y2 - y1, 2);
  car.rotation = angle;

  // Столкновение с землёй
  if (car.y > terrainY - car.height / 2) {
    car.y = terrainY - car.height / 2;
    car.vy = 0;
    car.onGround = true;
  } else {
    car.onGround = false;
  }

  // Простая логика "переворота"
  if (Math.abs(car.rotation) > 1.5) {
    alert("Ты перевернулся!");
    resetGame();
    return;
  }

  // Центрируем экран на машине
  ctx.save();
  ctx.translate(-car.x + canvas.width / 2, 0);
  drawTerrain();
  drawCar();
  ctx.restore();

  requestAnimationFrame(gameLoop);
}

function resetGame() {
  car.x = 100;
  car.y = 200;
  car.vx = 0;
  car.vy = 0;
  car.rotation = 0;
}

document.getElementById("gasBtn").addEventListener("mousedown", () => gas = true);
document.getElementById("gasBtn").addEventListener("mouseup", () => gas = false);
document.getElementById("brakeBtn").addEventListener("mousedown", () => brake = true);
document.getElementById("brakeBtn").addEventListener("mouseup", () => brake = false);

resetGame();
gameLoop();
</script>

</body>
</html>
