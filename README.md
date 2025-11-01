<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Typing Test</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: "Poppins", sans-serif;
      background: #0f172a;
      color: #f8fafc;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      margin: 0;
    }
    h1 {
      margin-bottom: 10px;
      font-size: 2em;
    }
    #test-box {
      background: #1e293b;
      padding: 20px;
      border-radius: 12px;
      width: 90%;
      max-width: 600px;
      text-align: center;
      box-shadow: 0 0 15px rgba(0,0,0,0.3);
    }
    #quote {
      font-size: 1.2em;
      margin-bottom: 20px;
      color: #cbd5e1;
    }
    textarea {
      width: 100%;
      height: 120px;
      padding: 10px;
      font-size: 1em;
      border-radius: 8px;
      border: none;
      resize: none;
      outline: none;
    }
    button {
      margin-top: 15px;
      padding: 10px 20px;
      border: none;
      background: #3b82f6;
      color: white;
      font-size: 1em;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover { background: #2563eb; }
    #result {
      margin-top: 20px;
      font-size: 1.2em;
      color: #38bdf8;
    }
  </style>
</head>
<body>
  <h1>Typing Speed Test</h1>
  <div id="test-box">
    <p id="quote">Klik "Mulai Tes" untuk memulai mengetik!</p>
    <textarea id="input" placeholder="Ketik teks di sini..." disabled></textarea><br>
    <button id="startBtn">Mulai Tes</button>
    <button id="restartBtn" style="display:none;">Ulangi</button>
    <div id="result"></div>
  </div>

  <script>
    const quotes = [
      "Belajar tanpa berpikir tidak ada gunanya.",
      "Setiap langkah kecil membawa kamu lebih dekat ke tujuan.",
      "Jangan takut gagal, takutlah tidak mencoba.",
      "Kesuksesan datang pada mereka yang bekerja keras."
    ];
    const quote = document.getElementById("quote");
    const input = document.getElementById("input");
    const startBtn = document.getElementById("startBtn");
    const restartBtn = document.getElementById("restartBtn");
    const result = document.getElementById("result");

    let startTime, currentQuote;

    function startTest() {
      currentQuote = quotes[Math.floor(Math.random() * quotes.length)];
      quote.textContent = currentQuote;
      input.value = "";
      input.disabled = false;
      input.focus();
      result.textContent = "";
      startTime = new Date();
      startBtn.style.display = "none";
      restartBtn.style.display = "inline-block";
    }

    function endTest() {
      const endTime = new Date();
      const timeTaken = (endTime - startTime) / 1000 / 60; // in minutes
      const typedWords = input.value.trim().split(/\s+/).length;
      const wpm = Math.round(typedWords / timeTaken);
      result.textContent = `Kecepatan mengetikmu: ${wpm} kata per menit!`;
      input.disabled = true;
    }

    input.addEventListener("input", () => {
      if (input.value.trim() === currentQuote) {
        endTest();
      }
    });

    startBtn.addEventListener("click", startTest);
    restartBtn.addEventListener("click", () => {
      quote.textContent = "Klik 'Mulai Tes' untuk memulai mengetik!";
      input.value = "";
      result.textContent = "";
      input.disabled = true;
      startBtn.style.display = "inline-block";
      restartBtn.style.display = "none";
    });
  </script>
</body>
</html>
