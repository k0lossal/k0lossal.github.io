<!-- index.html -->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bot WebApp</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: var(--tg-theme-bg-color, #ffffff);
            color: var(--tg-theme-text-color, #000000);
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
        }
        .btn {
            padding: 10px 20px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            background-color: var(--tg-theme-button-color, #2481cc);
            color: var(--tg-theme-button-text-color, #ffffff);
            cursor: pointer;
        }
        .input-field {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: 1px solid var(--tg-theme-hint-color, #999999);
            border-radius: 5px;
            background-color: var(--tg-theme-secondary-bg-color, #f0f0f0);
            color: var(--tg-theme-text-color, #000000);
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Gerador de Documentos</h2>
        <div id="params"></div>
        
        <input type="text" id="nome" class="input-field" placeholder="Nome completo">
        <input type="text" id="data" class="input-field" placeholder="Data de nascimento">
        
        <button class="btn" onclick="enviarDados()">Gerar Documento</button>
        <button class="btn" onclick="fecharWebApp()">Cancelar</button>
    </div>

    <script>
        let tg = window.Telegram.WebApp;
        tg.expand();

        // Recebe parâmetros do bot
        window.onload = function() {
            const initData = tg.initData || '';
            const initDataUnsafe = tg.initDataUnsafe || {};
            
            // Mostra os parâmetros recebidos
            document.getElementById('params').innerHTML = `
                <p>Tipo de Documento: ${initDataUnsafe.start_param || 'Não especificado'}</p>
            `;
        }

        function enviarDados() {
            const dados = {
                nome: document.getElementById('nome').value,
                data: document.getElementById('data').value,
                tipo: tg.initDataUnsafe.start_param
            };

            // Envia dados de volta para o bot
            tg.sendData(JSON.stringify(dados));
            tg.close();
        }

        function fecharWebApp() {
            tg.close();
        }
    </script>
</body>
</html>