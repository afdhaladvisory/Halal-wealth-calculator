# Halal-wealth-calculator
<!DOCTYPE html>
<html>
<head>
  <title>Retirement Calculator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body { font-family: Arial, sans-serif; padding: 2rem; background: #f9f9f9; }
    .container { max-width: 500px; margin: auto; background: #fff; padding: 2rem; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    input, select { width: 100%; padding: 10px; margin: 10px 0; }
    button { background: green; color: white; padding: 10px; width: 100%; border: none; border-radius: 4px; cursor: pointer; }
    h2 { color: green; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Plan Your Retirement</h2>
    <p>Fill in your details to find out how much you need to save monthly.</p>
    <form id="calcForm">
      Current Age: <input type="number" id="age" placeholder="e.g. 28">
      Current Savings ($): <input type="number" id="current" placeholder="e.g. 16000">
      Annual ROI (%): <input type="number" id="roi" step="0.01" value="5.5">
      Retirement Goal ($): <input type="number" id="goal" value="1000000">
      Investment Term (years):
      <select id="term">
        <option value="10">10</option>
        <option value="13">13</option>
        <option value="15" selected>15</option>
        <option value="20">20</option>
      </select>
      <button type="button" onclick="calculate()">Calculate</button>
    </form>

    <h3>Results</h3>
    <p>Monthly Investment Required: <strong>$<span id="monthly">0.00</span></strong></p>
  </div>

  <script>
    function calculate() {
      const current = parseFloat(document.getElementById("current").value || 0);
      const roi = parseFloat(document.getElementById("roi").value) / 100 / 12;
      const goal = parseFloat(document.getElementById("goal").value);
      const months = parseInt(document.getElementById("term").value) * 12;

      const futureValueCurrent = current * Math.pow(1 + roi, months);
      const PMT = (goal - futureValueCurrent) * roi / (Math.pow(1 + roi, months) - 1);

      document.getElementById("monthly").innerText = PMT > 0 ? PMT.toFixed(2) : "0.00";
    }
  </script>
</body>
</html>
