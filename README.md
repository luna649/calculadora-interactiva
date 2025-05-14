# calculadora-interactiva
data:text/html,<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculadora de Movilidad</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label { display: block; margin-top: 10px; }
    input, select, button { margin-top: 5px; padding: 5px; width: 100%; max-width: 300px; }
    #results { margin-top: 20px; padding: 10px; border: 1px solid #ccc; max-width: 400px; }
  </style>
</head>
<body>
  <h1>Calculadora Interactiva de Movilidad</h1>

  <form id="mobility-form">
    <label for="distance">Distancia (km):</label>
    <input type="number" id="distance" required>

    <label for="transport">Medio de transporte:</label>
    <select id="transport">
      <option value="car">Coche</option>
      <option value="public">Transporte público</option>
      <option value="bike">Bicicleta</option>
      <option value="walk">A pie</option>
    </select>

    <label for="departure">Hora de salida:</label>
    <input type="time" id="departure" required>

    <button type="submit">Calcular</button>
  </form>

  <div id="results"></div>

  <script>
    document.getElementById('mobility-form').addEventListener('submit', function (e) {
      e.preventDefault();

      const distance = parseFloat(document.getElementById('distance').value);
      const transport = document.getElementById('transport').value;
      const departure = document.getElementById('departure').value;

      let speed, costPerKm, carbonPerKm;

      switch (transport) {
        case 'car':
          speed = 50; // km/h
          costPerKm = 0.10; // USD/km
          carbonPerKm = 0.21; // kg CO2/km
          break;
        case 'public':
          speed = 30;
          costPerKm = 0.05;
          carbonPerKm = 0.10;
          break;
        case 'bike':
          speed = 15;
          costPerKm = 0.00;
          carbonPerKm = 0.00;
          break;
        case 'walk':
          speed = 5;
          costPerKm = 0.00;
          carbonPerKm = 0.00;
          break;
      }

      const timeHours = distance / speed;
      const timeMinutes = Math.round(timeHours * 60);
      const cost = (distance * costPerKm).toFixed(2);
      const carbon = (distance * carbonPerKm).toFixed(2);

      document.getElementById('results').innerHTML = `
        <p><strong>Hora de salida:</strong> ${departure}</p>
        <p><strong>Tiempo estimado de viaje:</strong> ${timeMinutes} minutos</p>
        <p><strong>Costo aproximado:</strong> $${cost}</p>
        <p><strong>Huella de carbono:</strong> ${carbon} kg CO₂</p>
      `;
    });
  </script>
</body>
</html>

