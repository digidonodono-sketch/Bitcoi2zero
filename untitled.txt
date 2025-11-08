<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Bitcoin2zero</title>
  <style>
    body { font-family: Arial; text-align: center; padding: 20px; background: #f0f0f0; }
    h1 { color: #333; }
    button { margin: 10px; padding: 15px; font-size: 18px; background: #007bff; color: white; border: none; border-radius: 10px; }
  </style>
</head>
<body>
  <h1>Bitcoin2zero</h1>
  <p>Labas, <span id="user">...</span>!</p>
  <button onclick="sendData()">Siųsti duomenis botui</button>
  <button onclick="Telegram.WebApp.close()">Uždaryti</button>

  <script>
    // Gauk vartotojo vardą
    let user = Telegram.WebApp.initDataUnsafe.user;
    document.getElementById("user").innerText = user.first_name || "Vartotojau";

    // Siųsk duomenis botui
    function sendData() {
      Telegram.WebApp.sendData("vartotojas_spaude_mygtuka");
      alert("Duomenys išsiųsti botui!");
    }

    // Pasiruošimas
    Telegram.WebApp.ready();
  </script>
</body>
</html>