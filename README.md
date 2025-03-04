<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Descargador de Videos</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(315deg, rgba(101,0,94,1) 3%, rgba(60,132,206,1) 38%, rgba(48,238,226,1) 68%, rgba(255,25,25,1) 98%);
            animation: gradient 15s ease infinite;
            background-size: 400% 400%;
            background-attachment: fixed;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            color: white;
            text-align: center;
        }

        @keyframes gradient {
            0% { background-position: 0% 0%; }
            50% { background-position: 100% 100%; }
            100% { background-position: 0% 0%; }
        }

        input, button {
            padding: 10px;
            margin: 10px;
            border: none;
            border-radius: 5px;
        }

        button {
            background-color: #ff1925;
            color: white;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Descargador de Videos</h1>
    <p>Ingresa la URL del video para descargar:</p>
    <input type="text" id="videoUrl" placeholder="Pega la URL aquí">
    <button onclick="descargarVideo()">Descargar</button>
    
    <script>
        async function descargarVideo() {
            const url = document.getElementById('videoUrl').value;
            if (!url) {
                alert('Por favor, ingresa una URL válida.');
                return;
            }

            try {
                const response = await fetch(`https://api.savetube.me/api/download?url=${encodeURIComponent(url)}`);
                const data = await response.json();
                
                if (data.success && data.download_url) {
                    window.location.href = data.download_url;
                } else {
                    alert('Error al descargar el video. Intenta con otra URL.');
                }
            } catch (error) {
                alert('Ocurrió un error al conectarse con la API.');
            }
        }
    </script>
</body>
</html>
