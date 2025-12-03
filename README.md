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
            padding: 20px 15px;
        }

        .right-links h2 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            font-size: 1.8rem;
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        li {
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            padding: 20px;
            transition: transform 0.2s;
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
            font-size: 1.1rem;
        }

        .status-icon {
            width: 14px;
            height: 14px;
            background-color: #4caf50;
            border-radius: 50%;
            flex-shrink: 0;
        }

        .item-actions {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .item-actions a {
            text-decoration: none;
            background-color: #007bff;
            color: white;
            padding: 12px;
            text-align: center;
            border-radius: 5px;
            transition: background-color 0.3s;
            font-weight: 600;
            font-size: 1rem;
            display: inline-block;
            width: 150px;
            user-select: none;
        }

        .item-actions a:hover {
            background-color: #0056b3;
        }

        .download-count {
            font-size: 14px;
            color: #666;
            user-select: none;
        }

        .footer {
            text-align: center;
            padding: 20px;
            color: #888;
            font-size: 14px;
            margin-top: 40px;
        }

        /* Ajustes para telas menores */
        @media (max-width: 600px) {
            .container {
                padding: 15px 10px;
            }

            .right-links h2 {
                font-size: 1.5rem;
            }

            .item-header {
                font-size: 1rem;
            }

            .status-icon {
                width: 12px;
                height: 12px;
            }

            .item-actions {
                gap: 8px;
            }

            .item-actions a {
                width: 100% !important;
                font-size: 1.1rem;
                padding: 14px 0;
            }

            .download-count {
                font-size: 13px;
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
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 3 - Dns Changer
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=138qm-a6WoalvrMLff3GhYV5BlESVHaYn"
                           target="_blank" download onclick="incrementDownloadCount(3)">Baixar</a>
                        <span id="downloadCount3" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 4 - Loja Painel
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1LBvQLUiBBoVljICfVOatjQLmJgrnswTh"
                           target="_blank" download onclick="incrementDownloadCount(4)">Baixar</a>
                        <span id="downloadCount4" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 5 - Loja P2
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1oE6GUvEvAk301OZCwxF3MyPmgdZ4eLji"
                           target="_blank" download onclick="incrementDownloadCount(5)">Baixar</a>
                        <span id="downloadCount5" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 6 - Smarters Pro
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1Midxxpti1y1m4LrKnuV7bSKjqozBPX3Q"
                           target="_blank" download onclick="incrementDownloadCount(6)">Baixar</a>
                        <span id="downloadCount6" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 7 - Cine Magic Plus (Windows)
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1C01bbDO6mgTTgrEa9ABQH3BwiNiq_J2w"
                           target="_blank" download onclick="incrementDownloadCount(7)">Baixar</a>
                        <span id="downloadCount7" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 8 - Cine Magic Plus (MacOS)
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1mnUGmXY69JAaT_TlY1ndgPHqzbXoF5My"
                           target="_blank" download onclick="incrementDownloadCount(8)">Baixar</a>
                        <span id="downloadCount8" class="download-count">Downloads: 0</span>
                    </div>
                </li>

                <!-- 9 - Free VPN -->
                <li>
                    <div class="item-header">
                        <span class="status-icon"></span> 9 - Pre VPN
                    </div>
                    <div class="item-actions">
                        <a href="https://drive.google.com/uc?export=download&id=1t09GsI6GBY-5rXquGzYDACvLBFieco48"
                           target="_blank" download onclick="incrementDownloadCount(9)">Baixar</a>
                        <span id="downloadCount9" class="download-count">Downloads: 0</span>
                    </div>
                </li>
            </ul>
        </div>
    </div>

    <footer class="footer">
        <p>&copy; 2025 Meu Site de Downloads | Todos os direitos reservados.</p>
    </footer>

    <script>
        function updateVisitCount() {
            let visitCount = localStorage.getItem('visitCount') || 0;
            visitCount = parseInt(visitCount) + 1;
            localStorage.setItem('visitCount', visitCount);
            const visitDisplay = document.getElementById('visitCount');
            if (visitDisplay) visitDisplay.textContent = visitCount;
        }

        async function getUserIp() {
            try {
                const response = await fetch('https://api.ipify.org?format=json');
                const data = await response.json();
                const ipDisplay = document.getElementById('userIp');
                if (ipDisplay) ipDisplay.textContent = data.ip;
            } catch {
                const ipDisplay = document.getElementById('userIp');
                if (ipDisplay) ipDisplay.textContent = 'Erro ao obter IP';
            }
        }

        function incrementDownloadCount(fileId) {
            let downloadCount = localStorage.getItem(`downloadCount${fileId}`) || 0;
            downloadCount = parseInt(downloadCount) + 1;
            localStorage.setItem(`downloadCount${fileId}`, downloadCount);
            document.getElementById(`downloadCount${fileId}`).textContent = `Downloads: ${downloadCount}`;
        }

        window.onload = function () {
            updateVisitCount();
            getUserIp();
            // Agora vai até 9
            for (let i = 1; i <= 9; i++) {
                let count = localStorage.getItem(`downloadCount${i}`) || 0;
                const el = document.getElementById(`downloadCount${i}`);
                if (el) {
                    el.textContent = `Downloads: ${count}`;
                }
            }
        };
    </script>
</body>
</html>
