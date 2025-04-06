# Dk
Welcome to dk game

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Dm Win Trading</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #101820;
      color: #ffffff;
      text-align: center;
      padding: 20px;
    }
    .container {
      max-width: 600px;
      margin: auto;
      padding: 20px;
      background-color: #1a1f2b;
      border-radius: 10px;
    }
    .timer {
      font-size: 2rem;
      margin: 20px 0;
    }
    .buttons button {
      padding: 10px 20px;
      margin: 10px;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      cursor: pointer;
    }
    .green { background-color: #28a745; color: #fff; }
    .red { background-color: #dc3545; color: #fff; }
    .violet { background-color: #6f42c1; color: #fff; }
    #result {
      margin-top: 20px;
      font-size: 1.5rem;
    }
    canvas {
      margin-top: 30px;
      background-color: #fff;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Dm Win Trading</h1>
    <p>Fake Balance: ₹10,000</p>
    <div class="timer">Next round in: <span id="countdown">30</span> sec</div>
    <div class="buttons">
      <button class="green" onclick="choose('Green')">Green</button>
      <button class="red" onclick="choose('Red')">Red</button>
      <button class="violet" onclick="choose('Violet')">Violet</button>
    </div>
    <div id="result"></div>
    <canvas id="chart" width="500" height="200"></canvas>
  </div>

  <script>
    let countdown = 30;
    let selectedColor = null;
    let ctx = document.getElementById("chart").getContext("2d");
    let history = [];

    function drawChart() {
      ctx.clearRect(0, 0, 500, 200);
      ctx.beginPath();
      ctx.moveTo(0, 100);
      history.forEach((color, index) => {
        let y = color === "Green" ? 50 : color === "Red" ? 150 : 100;
        ctx.lineTo(index * 50 + 50, y);
      });
      ctx.strokeStyle = "#000";
      ctx.stroke();
    }

    function updateCountdown() {
      countdown--;
      document.getElementById("countdown").innerText = countdown;
      if (countdown <= 0) {
        const colors = ["Green", "Red", "Violet"];
        const resultColor = colors[Math.floor(Math.random() * colors.length)];
        history.push(resultColor);
        drawChart();

        let message = "You Lose";
        if (selectedColor === resultColor) {
          message = "You Win!";
        }
        document.getElementById("result").innerText = "Result: " + resultColor + " - " + message;

        countdown = 30;
        selectedColor = null;
      }
    }

    function choose(color) {
      selectedColor = color;
      alert("You selected: " + color);
    }

    setInterval(updateCountdown, 1000);
    drawChart();
  </script>
</body>
</html>

