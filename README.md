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
            border-left: 10px solid
