<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pokémon Card Market</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: white;
    padding: 20px;
    text-align: center;
  }
  table {
    margin: 0 auto;
    border-collapse: collapse;
    width: 300px;
  }
  th, td {
    border: 1px solid #ccc;
    padding: 10px;
  }
  input[type="number"] {
    width: 60px;
    text-align: center;
  }
  .total {
    font-weight: bold;
    margin-top: 20px;
    font-size: 1.2em;
  }
  .change-section {
    margin-top: 30px;
  }
  .change-section table {
    width: 350px;
  }
  .money-positive {
    color: green;
  }
  .money-negative {
    color: red;
  }
  .price-white { background-color: white; }
  .price-red { background-color: #ffcccc; }
  .price-black { background-color: #ddd; color: black; }
  .price-green { background-color: #ccffcc; }
  .price-blue { background-color: #cce5ff; }
  img {
    height: 30px;
    vertical-align: middle;
    margin-right: 8px;
  }
  button {
    margin-top: 15px;
    padding: 8px 16px;
    font-size: 1em;
  }
</style>
</head>
<body>

<h2>Pokémon Card Market</h2>

<table>
  <tr><th>Price</th><th>Quantity</th></tr>
  <tr><td class="price-white">$0.25</td><td><input type="number" id="q25" min="0"></td></tr>
  <tr><td class="price-red">$0.50</td><td><input type="number" id="q50" min="0"></td></tr>
  <tr><td class="price-black">$1.00</td><td><input type="number" id="q100" min="0"></td></tr>
  <tr><td class="price-green">$2.00</td><td><input type="number" id="q200" min="0"></td></tr>
  <tr><td class="price-blue">$5.00</td><td><input type="number" id="q500" min="0"></td></tr>
</table>

<div class="total" id="total">Total: $0.00</div>

<div class="change-section">
  <h3>Change Maker</h3>
  <table>
    <tr><th>Denomination</th><th>Quantity</th></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/9/99/US_$20_bill_cartoon_icon.svg" alt="$20">$20</td><td><input type="number" id="b20" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/2/2a/US_$10_bill_cartoon_icon.svg" alt="$10">$10</td><td><input type="number" id="b10" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/8/8a/US_$5_bill_cartoon_icon.svg" alt="$5">$5</td><td><input type="number" id="b5" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/5/55/US_$1_bill_cartoon_icon.svg" alt="$1">$1</td><td><input type="number" id="b1" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/4/47/Quarter_coin_cartoon_icon.svg" alt="25¢">25¢</td><td><input type="number" id="c25" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/8/88/Dime_coin_cartoon_icon.svg" alt="10¢">10¢</td><td><input type="number" id="c10" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/d/d3/Nickel_coin_cartoon_icon.svg" alt="5¢">5¢</td><td><input type="number" id="c5" min="0"></td></tr>
    <tr><td><img src="https://upload.wikimedia.org/wikipedia/commons/7/7b/Penny_coin_cartoon_icon.svg" alt="1¢">1¢</td><td><input type="number" id="c1" min="0"></td></tr>
  </table>

  <div class="total" id="change"></div>
</div>

<button onclick="clearAll()">Clear</button>

<script>
function calculateTotal() {
  const q25 = parseFloat(document.getElementById('q25').value) || 0;
  const q50 = parseFloat(document.getElementById('q50').value) || 0;
  const q100 = parseFloat(document.getElementById('q100').value) || 0;
  const q200 = parseFloat(document.getElementById('q200').value) || 0;
  const q500 = parseFloat(document.getElementById('q500').value) || 0;

  const total = q25 * 0.25 + q50 * 0.50 + q100 * 1 + q200 * 2 + q500 * 5;
  document.getElementById('total').textContent = "Total: $" + total.toFixed(2);
  return total;
}

function calculateChange() {
  const total = calculateTotal();
  const b20 = parseFloat(document.getElementById('b20').value) || 0;
  const b10 = parseFloat(document.getElementById('b10').value) || 0;
  const b5 = parseFloat(document.getElementById('b5').value) || 0;
  const b1 = parseFloat(document.getElementById('b1').value) || 0;
  const c25 = parseFloat(document.getElementById('c25').value) || 0;
  const c10 = parseFloat(document.getElementById('c10').value) || 0;
  const c5 = parseFloat(document.getElementById('c5').value) || 0;
  const c1 = parseFloat(document.getElementById('c1').value) || 0;

  const received = (b20 * 20) + (b10 * 10) + (b5 * 5) + (b1 * 1) + (c25 * 0.25) + (c10 * 0.10) + (c5 * 0.05) + (c1 * 0.01);
  const difference = received - total;
  const changeDiv = document.getElementById('change');

  if (difference < 0) {
    changeDiv.textContent = "Money owed: $" + Math.abs(difference).toFixed(2);
    changeDiv.className = "total money-negative";
  } else {
    changeDiv.textContent = "Change: $" + difference.toFixed(2);
    changeDiv.className = "total money-positive";
  }
}

function clearAll() {
  document.querySelectorAll('input[type="number"]').forEach(input => input.value = '');
  document.getElementById('total').textContent = "Total: $0.00";
  document.getElementById('change').textContent = '';
}

document.querySelectorAll('input[type="number"]').forEach(input => {
  input.addEventListener('input', calculateChange);
});
</script>

</body>
</html>
