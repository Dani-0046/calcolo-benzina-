<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calcolatore Consumo Benzina</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f4f8;
      padding: 20px;
      max-width: 600px;
      margin: auto;
    }
    h1 {
      text-align: center;
      color: #333;
    }
    label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
    }
    input[type="number"] {
      width: 100%;
      padding: 8px;
      margin-top: 5px;
    }
    .checkbox-container {
      display: flex;
      align-items: center;
      margin-top: 15px;
    }
    .checkbox-container input {
      margin-right: 10px;
    }
    button {
      margin-top: 20px;
      width: 100%;
      padding: 10px;
      background-color: #4caf50;
      color: white;
      font-size: 16px;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
    #result {
      margin-top: 20px;
      padding: 10px;
      background-color: #fff;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <h1>Calcolatore Consumo Benzina</h1>

  <label for="distance">Distanza percorsa (km):</label>
  <input type="number" id="distance" />

  <label for="price">Prezzo benzina (€/litro):</label>
  <input type="number" step="0.01" id="price" />

  <label for="efficiency">Efficienza del veicolo (litri/100km):</label>
  <input type="number" step="0.1" id="efficiency" />

  <div class="checkbox-container">
    <input type="checkbox" id="roundtrip" />
    <label for="roundtrip">Aggiungi ritorno</label>
  </div>

  <label for="passengers">Numero di passeggeri (incluso il conducente):</label>
  <input type="number" id="passengers" />

  <label for="extra">Altri costi (es. pedaggi, parcheggi):</label>
  <input type="number" step="0.01" id="extra" />

  <button onclick="calculate()">Calcola</button>

  <div id="result"></div>

  <script>
    function calculate() {
      const distance = parseFloat(document.getElementById('distance').value) || 0;
      const price = parseFloat(document.getElementById('price').value) || 0;
      const efficiency = parseFloat(document.getElementById('efficiency').value) || 0;
      const roundtrip = document.getElementById('roundtrip').checked;
      const passengers = parseInt(document.getElementById('passengers').value) || 1;
      const extra = parseFloat(document.getElementById('extra').value) || 0;

      const totalKm = roundtrip ? distance * 2 : distance;
      const litersUsed = (totalKm * efficiency) / 100;
      const fuelCost = litersUsed * price;
      const totalCost = fuelCost + extra;
      const perPerson = totalCost / passengers;

      document.getElementById('result').innerHTML = `
        <strong>Risultati:</strong><br />
        Distanza totale: ${totalKm.toFixed(2)} km<br />
        Carburante utilizzato: ${litersUsed.toFixed(2)} litri<br />
        Costo carburante: €${fuelCost.toFixed(2)}<br />
        Costo totale (inclusi extra): €${totalCost.toFixed(2)}<br />
        Costo per persona: €${perPerson.toFixed(2)}
      `;
    }
  </script>
</body>
</html>
