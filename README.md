
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Pokémon Card Market</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: white;
    padding: 20px;
    text-align: center;
    color: #222;
  }

  h2 { margin-bottom: 10px; }

  table.main, table.change {
    margin: 0 auto 12px auto;
    border-collapse: collapse;
    width: 320px;
    max-width: 92vw;
  }
  table.main th, table.main td,
  table.change th, table.change td {
    border: 1px solid #ddd;
    padding: 8px;
    vertical-align: middle;
    text-align: left;
  }
  table.main th, table.change th {
    text-align: center;
    background: #f8f8f8;
  }

  input[type="number"] { width: 72px; padding: 6px; font-size: 1rem; text-align: center; }

  .total {
    font-weight: bold;
    margin-top: 10px;
    font-size: 1.15em;
  }

  .price-white { background-color: #ffffff; }
  .price-red   { background-color: #ffebeb; }
  .price-black { background-color: #eeeeee; color: #000; }
  .price-green { background-color: #eefbee; }
  .price-blue  { background-color: #eef6ff; }

  .change-section { margin-top: 20px; }
  .denom-cell { display: flex; align-items: center; gap: 8px; }

  .icon { flex: 0 0 auto; }

  /* Bills: consistent green */
  .bill { width: 40px; height: 26px; }

  /* Coins: scale relatively */
  .quarter { width: 36px; height: 36px; }
  .nickel  { width: 30px; height: 30px; }
  .penny   { width: 28px; height: 28px; }
  .dime    { width: 24px; height: 24px; }

  button { margin-top: 12px; padding: 8px 14px; font-size: 1rem; cursor: pointer; }

  #changeBox { display: inline-block; margin-top: 8px; padding: 8px 12px; border-radius: 6px; }
  .change-green { background: #4CAF50; color: #fff; }
  .change-red { background: #E74C3C; color: #fff; }
</style>
</head>
<body>

<h2>Pokémon Card Market</h2>

<!-- Prices -->
<table class="main">
  <tr><th>Price</th><th>Quantity</th></tr>
  <tr><td class="price-white">$0.25</td><td><input type="number" id="q25" min="0" placeholder=""></td></tr>
  <tr><td class="price-red">$0.50</td><td><input type="number" id="q50" min="0" placeholder=""></td></tr>
  <tr><td class="price-black">$1.00</td><td><input type="number" id="q100" min="0" placeholder=""></td></tr>
  <tr><td class="price-green">$2.00</td><td><input type="number" id="q200" min="0" placeholder=""></td></tr>
  <tr><td class="price-blue">$5.00</td><td><input type="number" id="q500" min="0" placeholder=""></td></tr>
</table>

<div id="total" class="total">Total: $0.00</div>

<!-- Change Maker -->
<div class="change-section">
  <h3>Change Maker</h3>

  <table class="change">
    <tr><th>Denomination</th><th>Quantity</th></tr>

    <!-- $20 -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon bill" viewBox="0 0 160 96">
            <rect x="6" y="12" width="148" height="72" rx="10" ry="10"
              fill="#79c48c" stroke="#5ea972" stroke-width="6"/>
            <text x="80" y="58" font-size="36" font-family="Verdana" font-weight="700"
              text-anchor="middle" fill="#0b3b17">$20</text>
          </svg>
          <span>$20</span>
        </div>
      </td>
      <td><input type="number" id="b20" min="0" placeholder=""></td>
    </tr>

    <!-- $10 -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon bill" viewBox="0 0 160 96">
            <rect x="6" y="12" width="148" height="72" rx="10" ry="10"
              fill="#79c48c" stroke="#5ea972" stroke-width="6"/>
            <text x="80" y="58" font-size="34" font-family="Verdana" font-weight="700"
              text-anchor="middle" fill="#0b3b17">$10</text>
          </svg>
          <span>$10</span>
        </div>
      </td>
      <td><input type="number" id="b10" min="0" placeholder=""></td>
    </tr>

    <!-- $5 -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon bill" viewBox="0 0 160 96">
            <rect x="6" y="12" width="148" height="72" rx="10" ry="10"
              fill="#79c48c" stroke="#5ea972" stroke-width="6"/>
            <text x="80" y="58" font-size="34" font-family="Verdana" font-weight="700"
              text-anchor="middle" fill="#0b3b17">$5</text>
          </svg>
          <span>$5</span>
        </div>
      </td>
      <td><input type="number" id="b5" min="0" placeholder=""></td>
    </tr>

    <!-- $1 -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon bill" viewBox="0 0 160 96">
            <rect x="6" y="12" width="148" height="72" rx="10" ry="10"
              fill="#79c48c" stroke="#5ea972" stroke-width="6"/>
            <text x="80" y="58" font-size="34" font-family="Verdana" font-weight="700"
              text-anchor="middle" fill="#0b3b17">$1</text>
          </svg>
          <span>$1</span>
        </div>
      </td>
      <td><input type="number" id="b1" min="0" placeholder=""></td>
    </tr>

    <!-- 25¢ quarter -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon quarter" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="45" fill="#d1d3d4" stroke="#9fa2a3" stroke-width="5"/>
            <text x="50" y="58" text-anchor="middle" font-size="20" font-family="Verdana"
              font-weight="700" fill="#2b2b2b">25¢</text>
          </svg>
          <span>25¢</span>
        </div>
      </td>
      <td><input type="number" id="c25" min="0" placeholder=""></td>
    </tr>

    <!-- 10¢ dime -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon dime" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="32" fill="#f0f4f6" stroke="#bfc6cc" stroke-width="5"/>
            <text x="50" y="58" text-anchor="middle" font-size="16" font-family="Verdana"
              font-weight="700" fill="#2b2b2b">10¢</text>
          </svg>
          <span>10¢</span>
        </div>
      </td>
      <td><input type="number" id="c10" min="0" placeholder=""></td>
    </tr>

    <!-- 5¢ nickel -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon nickel" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="38" fill="#d4d7d9" stroke="#9aa0a5" stroke-width="5"/>
            <text x="50" y="58" text-anchor="middle" font-size="16" font-family="Verdana"
              font-weight="700" fill="#1f1f1f">5¢</text>
          </svg>
          <span>5¢</span>
        </div>
      </td>
      <td><input type="number" id="c5" min="0" placeholder=""></td>
    </tr>

    <!-- 1¢ penny -->
    <tr>
      <td>
        <div class="denom-cell">
          <svg class="icon penny" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="36" fill="#d46a28" stroke="#9a3e10" stroke-width="5"/>
            <text x="50" y="58" text-anchor="middle" font-size="16" font-family="Verdana"
              font-weight="700" fill="#fff">1¢</text>
          </svg>
          <span>1¢</span>
        </div>
      </td>
      <td><input type="number" id="c1" min="0" placeholder=""></td>
    </tr>
  </table>

  <div id="changeBox" aria-live="polite"></div>
</div>

<button onclick="clearAll()">Clear</button>

<script>
function calculateTotal() {
  const q25 = parseFloat(document.getElementById('q25').value) || 0;
  const q50 = parseFloat(document.getElementById('q50').value) || 0;
  const q100 = parseFloat(document.getElementById('q100').value) || 0;
  const q200 = parseFloat(document.getElementById('q200').value) || 0;
  const q500 = parseFloat(document.getElementById('q500').value) || 0;
  const total = q25*0.25 + q50*0.5 + q100*1 + q200*2 + q500*5;
  document.getElementById('total').textContent = "Total: $" + total.toFixed(2);
  return total;
}

function calculateChange() {
  const total = calculateTotal();
  const b20 = parseFloat(document.getElementById('b20').value) || 0;
  const b10 = parseFloat(document.getElementById('b10').value) || 0;
  const b5  = parseFloat(document.getElementById('b5').value)  || 0;
  const b1  = parseFloat(document.getElementById('b1').value)  || 0;
  const c25 = parseFloat(document.getElementById('c25').value) || 0;
  const c10 = parseFloat(document.getElementById('c10').value) || 0;
  const c5  = parseFloat(document.getElementById('c5').value)  || 0;
  const c1  = parseFloat(document.getElementById('c1').value)  || 0;

  const received = b20*20 + b10*10 + b5*5 + b1*1 + c25*0.25 + c10*0.1 + c5*0.05 + c1*0.01;
  const diff = received - total;
  const box = document.getElementById('changeBox');

  if (total === 0 && received === 0) { box.className=''; box.textContent=''; return; }

  if (diff < 0) {
    box.className='change-red';
    box.innerHTML='<strong>Money owed:</strong> $'+Math.abs(diff).toFixed(2);
  } else {
    box.className='change-green';
    box.innerHTML='<strong>Change:</strong> $'+diff.toFixed(2);
  }
}

function clearAll() {
  document.querySelectorAll('input[type="number"]').forEach(i => i.value='');
  document.getElementById('total').textContent='Total: $0.00';
  const box=document.getElementById('changeBox');
  box.className=''; box.textContent='';
}

document.querySelectorAll('input[type="number"]').forEach(el=>{
  el.addEventListener('input', calculateChange);
});
clearAll();
</script>
</body>
</html>
