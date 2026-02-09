<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de Keys</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 500px; margin: 2rem auto; padding: 0 1rem; }
        .container { background: #f0f0f0; padding: 2rem; border-radius: 8px; text-align: center; }
        h1 { color: #333; }
        #generatedKey { margin: 1.5rem 0; padding: 1rem; background: #fff; border-radius: 4px; font-weight: bold; font-size: 1.1rem; min-height: 2rem; }
        #stockInfo { color: #666; margin: 1rem 0; }
        button { padding: 0.8rem 2rem; border-radius: 4px; border: none; background: #007bff; color: white; cursor: pointer; font-weight: bold; font-size: 1rem; }
        button:disabled { background: #6c757d; cursor: not-allowed; }
        button:hover:not(:disabled) { background: #0056b3; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Generador de Keys</h1>
        <div id="stockInfo"></div>
        <div>Key generada:</div>
        <div id="generatedKey">-- Ninguna --</div>
        <button id="generateBtn" onclick="generateKey()">Generar Key</button>
    </div>

    <script>
        // Cargar stock desde localStorage
        function loadStock() {
            const stock = localStorage.getItem('keyStock');
            return stock ? JSON.parse(stock) : [];
        }

        // Guardar stock actualizado
        function saveStock(stock) {
            localStorage.setItem('keyStock', JSON.stringify(stock));
            updateUI();
        }

        // Actualizar interfaz (info de stock y estado del botón)
        function updateUI() {
            const stock = loadStock();
            document.getElementById('stockInfo').textContent = `Stock disponible: ${stock.length} keys`;
            document.getElementById('generateBtn').disabled = stock.length === 0;
        }

        // Generar key aleatoria y eliminar del stock
        function generateKey() {
            const stock = loadStock();
            if (stock.length === 0) { alert('No hay keys disponibles en el stock'); return; }
            
            // Seleccionar índice aleatorio
            const randomIndex = Math.floor(Math.random() * stock.length);
            const selectedKey = stock[randomIndex];
            
            // Eliminar la key del stock
            const updatedStock = stock.filter((_, index) => index !== randomIndex);
            saveStock(updatedStock);
            
            // Mostrar la key generada
            document.getElementById('generatedKey').textContent = selectedKey;
            alert(`Key generada exitosamente: ${selectedKey}`);
        }

        // Inicializar interfaz
        window.onload = updateUI;
    </script>
</body>
</html>
