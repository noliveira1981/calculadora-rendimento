<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Rendimento</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
            padding: 20px;
        }
        .container {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            margin: auto;
        }
        h1 {
            color: #333;
            font-size: 20px;
            margin-bottom: 15px;
        }
        .radio-group {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }
        .radio-group label {
            font-size: 14px;
            cursor: pointer;
            padding: 8px 12px;
            background: #ddd;
            border-radius: 5px;
            transition: 0.3s;
        }
        .radio-group input {
            display: none;
        }
        .radio-group input:checked + label {
            background: #28a745;
            color: white;
        }
        label {
            font-weight: bold;
            display: block;
            text-align: left;
            font-size: 14px;
            margin-top: 10px;
        }
        input, button {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 14px;
        }
        button {
            background: #28a745;
            color: white;
            border: none;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background: #218838;
        }
        .btn-limpar {
            background: #dc3545;
        }
        .btn-limpar:hover {
            background: #c82333;
        }
        .resultado {
            font-size: 16px;
            margin-top: 10px;
            padding: 10px;
            background: #e9ecef;
            border-radius: 5px;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Calculadora de Rendimento</h1>

        <div class="radio-group">
            <input type="radio" id="bolo" name="tipo" value="bolo" checked onclick="mostrarCampos()">
            <label for="bolo">Bolo</label>

            <input type="radio" id="creme" name="tipo" value="creme" onclick="mostrarCampos()">
            <label for="creme">Creme</label>
        </div>

        <!-- Campos para cálculo de bolo -->
        <div id="campoBolo">
            <label for="massaCura">Massa crua (g):</label>
            <input type="number" id="massaCura" placeholder="Ex: 550" step="1" min="1">
            <label for="massaAssada">Massa assada (g):</label>
            <input type="number" id="massaAssada" placeholder="Ex: 500" step="1" min="1">
        </div>

        <!-- Campos para cálculo do creme -->
        <div id="campoCreme" class="hidden">
            <label for="quantidade">Rendimento desejado (kg):</label>
            <input type="number" id="quantidade" placeholder="Ex: 3.4" step="0.1" min="0">
        </div>

        <button onclick="calcular()">Calcular</button>
        <button class="btn-limpar" onclick="limparCampos()">Limpar</button>

        <div class="resultado">
            <p id="resultado1">---</p>
            <p id="resultado2">---</p>
        </div>
    </div>

    <script>
        function mostrarCampos() {
            let tipoProduto = document.querySelector('input[name="tipo"]:checked').value;

            document.getElementById("campoBolo").classList.add("hidden");
            document.getElementById("campoCreme").classList.add("hidden");

            if (tipoProduto === "bolo") {
                document.getElementById("campoBolo").classList.remove("hidden");
            } else {
                document.getElementById("campoCreme").classList.remove("hidden");
            }
        }

        function calcular() {
            let tipoProduto = document.querySelector('input[name="tipo"]:checked').value;

            if (tipoProduto === "bolo") {
                calcularBolo();
            } else {
                calcularCreme();
            }
        }

        function calcularBolo() {
            let massaCura = parseFloat(document.getElementById("massaCura").value);
            let massaAssada = parseFloat(document.getElementById("massaAssada").value);

            if (isNaN(massaCura) || massaCura <= 0 || isNaN(massaAssada) || massaAssada <= 0) {
                alert("Por favor, insira valores válidos para a massa crua e assada.");
                return;
            }

            let perda = massaCura - massaAssada;
            let percentualPerda = (perda / massaCura) * 100;

            document.getElementById("resultado1").innerText = `Perda de massa: ${perda.toFixed(2)}g`;
            document.getElementById("resultado2").innerText = `Percentual de perda: ${percentualPerda.toFixed(2)}%`;
        }

        function calcularCreme() {
            let rendimentoBase = 1.7;
            let leitePara500g = 1.25;
            let basePara500g = 500;

            let quantidadeDesejada = parseFloat(document.getElementById("quantidade").value);

            if (isNaN(quantidadeDesejada) || quantidadeDesejada <= 0) {
                alert("Por favor, insira um valor válido para o rendimento.");
                return;
            }

            let baseNecessaria = (quantidadeDesejada * basePara500g) / rendimentoBase;
            let leiteNecessario = (baseNecessaria * leitePara500g) / basePara500g;

            document.getElementById("resultado1").innerText = `Leite necessário: ${leiteNecessario.toFixed(2)}L`;
            document.getElementById("resultado2").innerText = `Creme necessário: ${baseNecessaria.toFixed(2)}g`;
        }

        function limparCampos() {
            document.getElementById("massaCura").value = "";
            document.getElementById("massaAssada").value = "";
            document.getElementById("quantidade").value = "";
            document.getElementById("resultado1").innerText = "---";
            document.getElementById("resultado2").innerText = "---";
        }
    </script>

</body>
</html>
