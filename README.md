<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Arquivos para Download</title>
    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            width: 100%; /* Importante para responsividade */
        }

        .right-links h2 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            word-break: break-word;
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
            max-width: 100%;
        }

        li {
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            padding: 20px;
            transition: transform 0.2s;
            max-width: 100%;
            word-break: break-word; /* evita overflow de texto */
        }

        li:hover {
            transform: scale(1.01);
        }

        .item-header {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: bold;
            margin-bottom: 10px;
            color: #444;
            flex-wrap: wrap; /* permite quebrar linha em telas pequenas */
            word-break: break-word;
        }

        .status-icon {
            width: 12px;
            height: 12px;
            background-color: #4caf50;
            border-radius: 50%;
            flex-shrink: 0;
        }

        .item-actions {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .item-actions a {
            text-decoration: none;
            background-color: #007bff;
            color: white;
            padding: 10px;
            text-align: center;
            border-radius: 5px;
            transition: background-color 0.3s;
            width: 100%; /* botões sempre 100% largura */
            box-sizing: border-box;
            word-break: break-word;
        }

        .item-actions a:hover {
            background-color: #0056b3;
        }

        .download-count {
            font-size: 14px;
            color: #666;
            word-break: break-word;
        }

        .footer {
            text-align: center;
            padding: 20px;
            color: #888;
            font-size: 14px;
            margin-top: 40px;
            word-break: break-word;
        }

        @media (max-width: 600px) {
            .container {
                padding: 10px;
            }

            .item-header {
                font-size: 16px;
            }

            /* Se quiser, pode reduzir o padding do botão no mobile */
            .item-actions a {
                padding: 12px;
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="right-links links">
            <h2>Arquivos para Download</h2>
            <ul>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 1 - Club Lite
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1_sfzo16QtVbkG6uwBkGO8h1XvawvN2LP"
                           target="_blank" download onclick="incrementDownloadCount(1)">Baixar</a>
                        <span id="downloadCount1" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 2 - Club Smart
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1YbnfRTIoKQo3qJxW1aaG1G7DYYOsh2jk"
                           target="_blank" download onclick="incrementDownloadCount(2)">Baixar</a>
                        <span id="downloadCount2" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <!-- demais itens seguem o mesmo padrão -->
            </ul>
        </div>
    </div>

    <footer class="footer">
        <p>&copy; 2025 Meu Site de Downloads | Todos os direitos reservados.</p>
    </footer>

    <script>
        function incrementDownloadCount(fileId) {
            let downloadCount = localStorage.getItem(`downloadCount${fileId}`) || 0;
            downloadCount = parseInt(downloadCount) + 1;
            localStorage.setItem(`downloadCount${fileId}`, downloadCount);
            document.getElementById(`downloadCount${fileId}`).textContent = `Downloads: ${downloadCount}`;
        }

        window.onload = function () {
            for (let i = 1; i <= 8; i++) {
                let count = localStorage.getItem(`downloadCount${i}`) || 0;
                document.getElementById(`downloadCount${i}`).textContent = `Downloads: ${count}`;
            }
        };
    </script>
</body>
</html>
