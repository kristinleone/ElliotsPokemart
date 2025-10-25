<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Pokémon Card POS</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: white;
    color: black;
    text-align: center;
    margin: 20px;
  }

  table {
    margin: 0 auto 20px;
    border-collapse: collapse;
  }

  th, td {
    padding: 8px 12px;
    border: 1px solid #ccc;
    font-size: 1.2em;
  }

  td.price {
    color: white;
    font-weight: bold;
  }

  td.price.white { background: white; color: black; }
  td.price.red { background: red; }
  td.price.black { background: black; }
  td.price.green { background: green; }
  td.price.blue { background: blue; }

  input[type="number"] {
    width: 60px;
    font-size: 1.1em;
    text-align: center;
  }

  button {
    font-size: 1.2em;
    padding: 8px 16px;
    margin-top: 10px;
  }

  #totalDisplay {
    font-size: 1.5em;
    margin-top: 10px;
  }

  #moneyOwed {
    font-size: 1.5em;
    margin: 10px;
    font-weight: bold;
  }

  #changeSection {
    display: none;
    margin-top: 20px;
  }

  .svg-money {
    width: 60px;
    vertical-align: middle;
  }

  .coin {
    display: inline-block;
    border-radius: 50%;
    background: silver;
    text-align: center;
    color: black;
    font-weight: bold;
  }

  .coin.quarter { width: 40px; height: 40px; line-height: 40px; font-size: 0.9em; }
  .coin.dime { width: 28px; height: 28px; line-height: 28px; font-size: 0.8em; }
  .coin.nickel { width: 32px; height: 32px; line-height: 32px; font-size: 0.85em; }
  .coin.penny { width: 36px; height: 36px; line-height: 36px; font-size: 0.9em; background: #b87333; color: white; }

  #changeBreakdown div {
    margin: 4px 0;
    font-size: 1.2em;
  }
</style>
</head>
<body>

<h1>Pokémon Card POS</h1>

<table>
  <tr><th>Qty</th><th>Price</th></tr>
  <tr><td><input type="number" min="0"></td><td class="price white">$0.25</td></tr>
  <tr><td><input type="number" min="0"></td><td class="price red">$0.50</td></tr>
  <tr><td><input type="number" min="0"></td><td class="price black">$1.00</td></tr>
  <tr><td><input type="number" min="0"></td><td class="price green">$2.00</td></tr>
  <tr><td><input type="number" min="0"></td><td class="price blue">$5.00</td></tr>
</table>

<div id="totalDisplay">Total: $0.00</div>
<div id="moneyOwed" style="color:red;">Money Owed: $0.00</div>
<button id="clearAll">Clear</button>

<hr style="margin:20px 0;">

<h2>Money Received</h2>
<div id="moneyInputs">
  <div>
    <svg class="svg-money" viewBox="0 0 100 50">
      <rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/>
      <text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$20</text>
    </svg>
    × <input type="number" min="0" data-value="20">
  </div>
  <div>
    <svg class="svg-money" viewBox="0 0 100 50">
      <rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/>
      <text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$10</text>
    </svg>
    × <input type="number" min="0" data-value="10">
  </div>
  <div>
    <svg class="svg-money" viewBox="0 0 100 50">
      <rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/>
      <text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$5</text>
    </svg>
    × <input type="number" min="0" data-value="5">
  </div>
  <div>
    <svg class="svg-money" viewBox="0 0 100 50">
      <rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/>
      <text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$1</text>
    </svg>
    × <input type="number" min="0" data-value="1">
  </div>
  <div><span class="coin quarter">25¢</span> × <input type="number" min="0" data-value="0.25"></div>
  <div><span class="coin dime">10¢</span> × <input type="number" min="0" data-value="0.10"></div>
  <div><span class="coin nickel">5¢</span> × <input type="number" min="0" data-value="0.05"></div>
  <div><span class="coin penny">1¢</span> × <input type="number" min="0" data-value="0.01"></div>
</div>

<div id="changeSection">
  <h2>Change to Give</h2>
  <div id="changeBreakdown"></div>
</div>

<script>
const itemRows = document.querySelectorAll("table tr");
const totalDisplay = document.getElementById("totalDisplay");
const moneyOwed = document.getElementById("moneyOwed");
const changeSection = document.getElementById("changeSection");
const changeBreakdown = document.getElementById("changeBreakdown");
const clearAll = document.getElementById("clearAll");
const moneyInputs = document.querySelectorAll("#moneyInputs input");

function calculateTotal() {
  let total = 0;
  itemRows.forEach(row => {
    const input = row.querySelector("input");
    const priceCell = row.querySelector(".price");
    if (input && priceCell) {
      const qty = parseFloat(input.value) || 0;
      const price = parseFloat(priceCell.textContent.replace("$", ""));
      total += qty * price;
    }
  });
  totalDisplay.textContent = `Total: $${total.toFixed(2)}`;
  return total;
}

function calculateReceived() {
  let received = 0;
  moneyInputs.forEach(input => {
    const count = parseFloat(input.value) || 0;
    const val = parseFloat(input.dataset.value);
    received += count * val;
  });
  return received;
}

function calculateChangeDue() {
  const total = calculateTotal();
  const received = calculateReceived();
  const diff = received - total;

  if (diff < 0) {
    moneyOwed.style.color = "red";
    moneyOwed.textContent = `Money Owed: $${Math.abs(diff).toFixed(2)}`;
    changeSection.style.display = "none";
  } else {
    moneyOwed.style.color = "green";
    moneyOwed.textContent = `Change Due: $${diff.toFixed(2)}`;
    if (diff > 0) showChangeBreakdown(diff);
    else changeSection.style.display = "none";
  }
}

function showChangeBreakdown(amount) {
  const denominations = [
    { value: 20.0, label: "$20", svg: '<svg class="svg-money" viewBox="0 0 100 50"><rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/><text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$20</text></svg>' },
    { value: 10.0, label: "$10", svg: '<svg class="svg-money" viewBox="0 0 100 50"><rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/><text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$10</text></svg>' },
    { value: 5.0, label: "$5", svg: '<svg class="svg-money" viewBox="0 0 100 50"><rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/><text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$5</text></svg>' },
    { value: 1.0, label: "$1", svg: '<svg class="svg-money" viewBox="0 0 100 50"><rect width="100" height="50" fill="green" stroke="black" stroke-width="2"/><text x="50" y="30" text-anchor="middle" fill="white" font-size="20">$1</text></svg>' },
    { value: 0.25, label: "25¢", svg: '<span class="coin quarter">25¢</span>' },
    { value: 0.10, label: "10¢", svg: '<span class="coin dime">10¢</span>' },
    { value: 0.05, label: "5¢", svg: '<span class="coin nickel">5¢</span>' },
    { value: 0.01, label: "1¢", svg: '<span class="coin penny">1¢</span>' },
  ];

  let remaining = Math.round(amount * 100);
  changeBreakdown.innerHTML = "";
  denominations.forEach(d => {
    const count = Math.floor(remaining / Math.round(d.value * 100));
    if (count > 0) {
      remaining -= count * Math.round(d.value * 100);
      const div = document.createElement("div");
      div.innerHTML = `${d.svg} × ${count}`;
      changeBreakdown.appendChild(div);
    }
  });

  changeSection.style.display = "block";
}

document.querySelectorAll("input").forEach(i => i.addEventListener("input", calculateChangeDue));
clearAll.addEventListener("click", () => {
  document.querySelectorAll("table input").forEach(i => i.value = "");
  totalDisplay.textContent = "Total: $0.00";
  moneyOwed.style.color = "red";
  moneyOwed.textContent = "Money Owed: $0.00";
  changeSection.style.display = "none";
});
</script>

</body>
</html>
