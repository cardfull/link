<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Link para Downloads</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7fc;
            margin: 0;
            padding: 0;
            color: #333;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 15px;
            text-align: center;
            position: relative;
        }
        .info-topo {
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 12px;
            color: white;
        }
        .container {
            display: flex;
            flex-direction: column;
            padding: 20px;
        }
        @media (min-width: 768px) {
            .container {
                flex-direction: row;
                justify-content: center;
                gap: 40px;
            }
        }
        .right-links {
            width: 100%;
            max-width: 800px;
        }
        .links ul {
            list-style-type: none;
            padding: 0;
        }
        .links li {
            margin: 10px 0;
            background: #fff;
            padding: 10px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            box-shadow: 0 0 5px rgba(0,0,0,0.1);
        }
        .status-icon {
            width: 0;
            height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-bottom: 20px solid green;
            margin-right: 10px;
        }
        .footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 10px;
            position: fixed;
            width: 100%;
            bottom: 0;
        }
        .download-count {
            font-size: 12px;
            color: #666;
            margin-left: 10px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Bem-vindo ao site de Downloads</h1>
        <div class="info-topo">
            <span>Visitas: <span id="visitCount">0</span></span> |
            <span>IP: <span id="userIp">Carregando...</span></span>
        </div>
    </header>

    <div class="container">
        <div class="right-links links">
            <h2>Arquivos para Download</h2>
            <ul>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        1 - Club Lite
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1_sfzo16QtVbkG6uwBkGO8h1XvawvN2LP" target="_blank" download onclick="incrementDownloadCount(1)">Baixar</a>
                        <span id="downloadCount1" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        2 - Club Smart
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1YbnfRTIoKQo3qJxW1aaG1G7DYYOsh2jk" target="_blank" download onclick="incrementDownloadCount(2)">Baixar</a>
                        <span id="downloadCount2" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        3 - Dns Changer
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=138qm-a6WoalvrMLff3GhYV5BlESVHaYn" target="_blank" download onclick="incrementDownloadCount(3)">Baixar</a>
                        <span id="downloadCount3" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        4 - Loja Painel
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1LBvQLUiBBoVljICfVOatjQLmJgrnswTh" target="_blank" download onclick="incrementDownloadCount(4)">Baixar</a>
                        <span id="downloadCount4" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        5 - Loja P2
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1oE6GUvEvAk301OZCwxF3MyPmgdZ4eLji" target="_blank" download onclick="incrementDownloadCount(5)">Baixar</a>
                        <span id="downloadCount5" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        6 - Smarters Pro
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1Midxxpti1y1m4LrKnuV7bSKjqozBPX3Q" target="_blank" download onclick="incrementDownloadCount(6)">Baixar</a>
                        <span id="downloadCount6" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        7 - Cine Magic Plus (Windows)
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1C01bbDO6mgTTgrEa9ABQH3BwiNiq_J2w" target="_blank" download onclick="incrementDownloadCount(7)">Baixar</a>
                        <span id="downloadCount7" class="download-count">Downloads: 0</span>
                    </div>
                </li>
                <li>
                    <div style="display: flex; align-items: center;">
                        <span class="status-icon"></span>
                        8 - Cine Magic Plus (MacOS)
                    </div>
                    <div>
                        <a href="https://drive.google.com/uc?export=download&id=1mnUGmXY69JAaT_TlY1ndgPHqzbXoF5My" target="_blank" download onclick="incrementDownloadCount(8)">Baixar</a>
                        <span id="downloadCount8" class="download-count">Downloads: 0</span>
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
            document.getElementById('visitCount').textContent = visitCount;
        }

        async function getUserIp() {
            try {
                const response = await fetch('https://api.ipify.org?format=json');
                const data = await response.json();
                document.getElementById('userIp').textContent = data.ip;
            } catch (error) {
                document.getElementById('userIp').textContent = 'Erro ao obter IP';
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
            [1, 2, 3, 4, 5, 6, 7, 8].forEach(id => {
                let count = localStorage.getItem(`downloadCount${id}`) || 0;
                document.getElementById(`downloadCount${id}`).textContent = `Downloads: ${count}`;
            });
        };
    </script>
</body>
</html>
