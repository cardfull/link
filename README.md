<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Downloads Responsivos</title>
    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 16px;
        }

        h2 {
            text-align: center;
            color: #333;
            margin-bottom: 24px;
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        li {
            background: white;
            margin-bottom: 16px;
            padding: 16px;
            border-radius: 8px;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
        }

        .item-header {
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: bold;
            color: #444;
            margin-bottom: 12px;
            flex-wrap: wrap;
        }

        .status-icon {
            width: 12px;
            height: 12px;
            background-color: #4caf50;
            border-radius: 50%;
        }

        .item-actions {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .item-actions a {
            display: block;
            width: 100%;
            text-align: center;
            background-color: #007bff;
            color: white;
            text-decoration: none;
            padding: 10px;
            border-radius: 5px;
            font-weight: bold;
            transition: background-color 0.3s;
        }

        .item-actions a:hover {
            background-color: #0056b3;
        }

        .download-count {
            font-size: 14px;
            color: #666;
            text-align: center;
        }

        .footer {
            text-align: center;
            padding: 20px;
            font-size: 14px;
            color: #777;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Arquivos para Download</h2>
        <ul>
            <li>
                <div class="item-header">
                    <span class="status-icon"></span> 1 - Club Lite
                </div>
                <div class="item-actions">
                    <a href="#" onclick="incrementDownloadCount(1)">Baixar</a>
                    <span id="downloadCount1" class="download-count">Downloads: 0</span>
                </div>
            </li>
            <!-- Adicione os outros itens aqui seguindo o mesmo padrão -->
        </ul>
    </div>

    <footer class="footer">
        <p>&copy; 2025 Meu Site de Downloads</p>
    </footer>

    <script>
        function incrementDownloadCount(id) {
            let count = localStorage.getItem('downloadCount' + id) || 0;
            count++;
            localStorage.setItem('downloadCount' + id, count);
            document.getElementById('downloadCount' + id).textContent = 'Downloads: ' + count;
        }

        window.onload = () => {
            for (let i = 1; i <= 8; i++) {
                let count = localStorage.getItem('downloadCount' + i) || 0;
                let el = document.getElementById('downloadCount' + i);
                if (el) el.textContent = 'Downloads: ' + count;
            }
        };
    </script>
</body>
</html>
