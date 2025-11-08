<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Bitcoin2zero Clicker</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    body { font-family: Arial; text-align: center; padding: 20px; background: #1a1a1a; color: white; }
    h1 { color: #f7931a; }
    .coin { font-size: 60px; cursor: pointer; user-select: none; }
    .stats { margin: 20px; font-size: 18px; }
    button { margin: 10px; padding: 15px 25px; font-size: 18px; background: #f7931a; color: black; border: none; border-radius: 12px; font-weight: bold; }
    .upgrade { background: #28a745; color: white; }
  </style>
</head>
<body>
  <h1>₿ Bitcoin2zero Clicker</h1>
  <p>Labas, <span id="user">Vartotojau</span>!</p>
  
  <div class="coin" id="coin">₿</div>
  <div class="stats">
    <p>Bitcoin: <span id="balance">0</span> BTC</p>
    <p>Per paspaudimą: <span id="perClick">1</span></p>
  </div>

  <button class="upgrade" onclick="buyUpgrade()">Pirk +1 per paspaudimą (10 BTC)</button>
  <button onclick="withdraw()">Išgryninti į TON</button>
  <button onclick="Telegram.WebApp.close()">Uždaryti</button>

  <script>
    let balance = 0;
    let perClick = 1;
    const user = Telegram.WebApp.initDataUnsafe.user;
    document.getElementById("user").innerText = user.first_name || "Vartotojau";

    // Click event
    document.getElementById("coin").onclick = () => {
      balance += perClick;
      updateBalance();
      Telegram.WebApp.HapticFeedback.impactOccurred('light');
    };

    function updateBalance() {
      document.getElementById("balance").innerText = balance.toFixed(8);
      document.getElementById("perClick").innerText = perClick;
    }

    function buyUpgrade() {
      if (balance >= 10) {
        balance -= 10;
        perClick += 1;
        updateBalance();
        alert("Sveikiname! Dabar gauni +" + perClick + " per paspaudimą!");
      } else {
        alert("Trūksta 10 BTC!");
      }
    }

    function withdraw() {
      if (balance >= 100) {
        Telegram.WebApp.openInvoice({
          title: 'Bitcoin2zero Išmokėjimas',
          description: 'Išgrynink savo Bitcoin į TON',
          payload: 'withdraw_' + user.id + '_' + balance,
          provider_token: '', // Čia įrašyk savo TON mokėjimo tokeną (gausi iš @BotFather)
          currency: 'XTR', // TON kriptovaliuta
          prices: [{ label: 'Bitcoin', amount: Math.floor(balance * 100) }]
        });
      } else {
        alert("Reikia bent 100 BTC išgryninimui!");
      }
    }

    Telegram.WebApp.ready();
    updateBalance();
  </script>
</body>
</html>