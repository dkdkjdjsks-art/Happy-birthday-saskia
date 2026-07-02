<!index html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday! 🤍</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            /* Update Latar Belakang: Pink Soft Lucu */
            background: linear-gradient(135deg, #fff0f3 0%, #f7d9e3 100%);
            color: #4a4a4a;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
            perspective: 1000px;
        }

        /* Overlay Pembuka (Bypass Autoplay Browser) */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            /* Update Latar Belakang Overlay: Pink Soft */
            background-color: #fff0f3;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 999;
            transition: opacity 0.8s ease, visibility 0.8s;
            text-align: center;
            padding: 20px;
        }

        .overlay h2 {
            font-weight: 300;
            margin-bottom: 20px;
            color: #6b5b52;
            letter-spacing: 2px;
        }

        .open-btn {
            padding: 12px 30px;
            background-color: #6b5b52;
            color: #ffffff;
            border: none;
            border-radius: 25px;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s, background-color 0.3s;
        }

        .open-btn:hover {
            transform: scale(1.05);
            background-color: #554841;
        }

        /* Amplop & Kartu */
        .card-container {
            width: 90%;
            max-width: 420px;
            height: 550px;
            position: relative;
            transition: transform 0.8s ease;
            display: none; /* Muncul setelah overlay diklik */
            opacity: 0;
        }

        .card-container.show {
            display: block;
            animation: fadeIn 1s forwards;
        }

        .card {
            width: 100%;
            height: 100%;
            background: #ffffff;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.08);
            padding: 35px 25px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255,255,255,0.8);
        }

        /* Hiasan Estetik - Update Warna Gradasi Bulatan */
        .card::before {
            content: '';
            position: absolute;
            top: -50px;
            right: -50px;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle, rgba(247,217,227,0.4) 0%, transparent 70%);
            border-radius: 50%;
        }

        .header {
            text-align: center;
        }

        .header .emoji {
            font-size: 2.5rem;
            margin-bottom: 10px;
            display: inline-block;
            animation: float 3s ease-in-out infinite;
        }

        .header h1 {
            font-size: 1.6rem;
            font-weight: 400;
            color: #554841;
            letter-spacing: 1px;
        }

        /* Teks Berjalan / Scrollable */
        .letter-body {
            flex-grow: 1;
            margin: 25px 0;
            overflow-y: auto;
            padding-right: 5px;
            font-size: 0.95rem;
            line-height: 1.7;
            color: #625750;
            text-align: justify;
            font-weight: 300;
        }

        /* Custom Scrollbar */
        .letter-body::-webkit-scrollbar {
            width: 4px;
        }
        .letter-body::-webkit-scrollbar-thumb {
            /* Update Warna Scrollbar: Pink Soft */
            background: #f7d9e3;
            border-radius: 10px;
        }

        .letter-body p {
            margin-bottom: 15px;
        }

        .footer {
            text-align: center;
            font-size: 0.9rem;
            color: #8c7b70;
            font-style: italic;
            /* Update Warna Border Atas Footer: Pink Soft */
            border-top: 1px solid #f7d9e3;
            padding-top: 15px;
        }

        /* Elemen Musik Kontrol */
        .music-control {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.85);
            padding: 8px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            cursor: pointer;
            backdrop-filter: blur(5px);
            z-index: 10;
            /* Update Warna Border Musik: Pink Soft */
            border: 1px solid #f7d9e3;
        }

        .music-control .icon {
            display: inline-block;
            animation: rotate 4s linear infinite;
            animation-play-state: paused;
        }

        .music-control.playing .icon {
            animation-play-state: running;
        }

        /* Animasi-animasi */
        @keyframes fadeIn {
            to { opacity: 1; }
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        /* Floating Hearts Background - Update Warna Hati (Slightly Pink) */
        .heart {
            position: absolute;
            color: rgba(247, 187, 207, 0.15);
            font-size: 1.5rem;
            pointer-events: none;
            z-index: 1;
            animation: fly linear infinite;
        }

        @keyframes fly {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            10% { opacity: 0.5; }
            90% { opacity: 0.5; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>

    <!-- Overlay Pembuka -->
    <div class="overlay" id="overlay">
        <h2>Ada surat buat kamu 🤍</h2>
        <button class="open-btn" onclick="bukaSurat()">Buka Surat</button>
    </div>

    <!-- Konten Kartu Utama -->
    <div class="card-container" id="cardContainer">
        <div class="card">
            <div class="header">
                <span class="emoji">🎂</span>
                <h1>Happy Birthday!! 🤍</h1>
            </div>

            <div class="letter-body">
                <p>Ga kerasa ya udah nambah umur lagi. Semoga di umur yang baru ini semua yang kamu harapin pelan-pelan bisa tercapai. Semoga kamu selalu sehat, bahagia, dan banyak banget hal baik yang dateng ke hidup kamu.</p>
                
                <p>Aku cuma mau bilang makasih ya, karena aku bener-bener seneng bisa kenal sama kamu. Makasih udah selalu ada pas aku lagi butuh, makasih udah selalu jadi tempat yang bikin aku ngerasa ga sendirian.</p>
                
                <p>Jujur aku juga sering banget cerita tentang kamu ke temen-temen aku, karena aku bersyukur banget punya sahabat kayak kamu. Kamu tuh salah satu orang yang ngasih banyak core memory di hidup aku, dan itu bakal selalu aku inget.</p>
                
                <p>Semoga kita bisa terus jadi sahabat, bikin cerita-cerita baru, ketawa bareng, dan saling ada satu sama lain. Sekali lagi, happy birthday yaa. Semoga tahun ini jadi salah satu tahun terbaik buat kamu.</p>
            </div>

            <div class="footer">
                love u always. 🤍
            </div>
        </div>
    </div>

    <!-- Musik Kontrol & Audio -->
    <div class="music-control" id="musicControl" onclick="toggleMusic()">
        <span class="icon">🎵</span>
        <span id="musicStatus">Memutar musik...</span>
    </div>

    <!-- Audio Tag (Fallback: Mixkit beautiful dream, silakan sesuaikan link jika memiliki file Hazel English) -->
    <audio id="bgMusic" loop>
        <source src="https://assets.mixkit.co/music/preview/mixkit-beautiful-dream-493.mp3" type="audio/mpeg">
    </audio>

    <script>
        const audio = document.getElementById('bgMusic');
        const overlay = document.getElementById('overlay');
        const cardContainer = document.getElementById('cardContainer');
        const musicControl = document.getElementById('musicControl');
        const musicStatus = document.getElementById('musicStatus');

        // Atur volume agar tidak terlalu mengejutkan
        audio.volume = 0.6;

        function bukaSurat() {
            // Sembunyikan overlay
            overlay.style.opacity = '0';
            overlay.style.visibility = 'hidden';

            // Tampilkan kartu ucapan
            cardContainer.classList.add('show');

            // Putar Musik (Bypass aturan muting browser lewat interaksi user)
            audio.play().then(() => {
                musicControl.classList.add('playing');
            }).catch(error => {
                console.log("Autoplay gagal, perlu klik manual pada musik:", error);
                musicStatus.innerText = "Musik dijeda";
            });

            // Mulai efek hati berterbangan
            buatHati();
        }

        function toggleMusic() {
            if (audio.paused) {
                audio.play();
                musicControl.classList.add('playing');
                musicStatus.innerText = "Memutar musik...";
            } else {
                audio.pause();
                musicControl.classList.remove('playing');
                musicStatus.innerText = "Musik dijeda";
            }
        }

        // Efek Dekorasi Hati Terbang
        function buatHati() {
            setInterval(() => {
                const heart = document.createElement('div');
                heart.classList.add('heart');
                heart.innerText = '🤍';
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.animationDuration = Math.random() * 3 + 3 + 's'; // Antara 3-6 detik
                heart.style.fontSize = Math.random() * 10 + 15 + 'px';
                document.body.appendChild(heart);

                // Hapus elemen setelah animasi selesai agar tidak membebani browser
                setTimeout(() => {
                    heart.remove();
                }, 6000);
            }, 600);
        }
    </script>
</body>
</html>

