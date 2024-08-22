<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kirim Pesan</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #00aaff, #0044cc);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            width: 300px;
            text-align: center;
        }
        .message-box {
            width: 100%;
            height: 100px;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #ddd;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 10px;
            resize: none;
        }
        .send-button {
            background-color: #0044cc;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        .send-button:hover {
            background-color: #0033aa;
        }
    </style>
</head>
<body>
    <div class="container">
        <textarea class="message-box" id="message" placeholder="Kirim pesan Anda..."></textarea>
        <button class="send-button" onclick="sendMessage()">Kirim</button>
    </div>

    <script>
        function sendMessage() {
            // Mendapatkan pesan dari textarea
            var message = document.getElementById('message').value;
            
            // Mengambil lokasi pengguna
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(function(position) {
                    var latitude = position.coords.latitude;
                    var longitude = position.coords.longitude;
                    var locationMessage = `Lokasi Anda: Latitude ${latitude}, Longitude ${longitude}`;
                    
                    // Menampilkan pop-up
                    alert('Pesan terkirim!');
                    
                    // Mengarahkan pengguna ke bot Telegram dengan pesan dan lokasi
                    var telegramBotUrl = 'https://t.me/your_bot_username?start=';
                    var encodedMessage = encodeURIComponent(message + ' ' + locationMessage);
                    window.open(telegramBotUrl + encodedMessage, '_blank');
                    
                    // Mengosongkan textarea setelah mengirim pesan
                    document.getElementById('message').value = '';
                }, function(error) {
                    alert('Gagal mendapatkan lokasi: ' + error.message);
                });
            } else {
                alert('Geolocation tidak didukung oleh browser ini.');
            }
        }
    </script>
</body>
</html>
