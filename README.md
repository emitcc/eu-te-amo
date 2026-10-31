<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Luiz</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
        }

        body {
            background-color: #0d0914;
            color: #ffffff;
            font-family: 'Press Start 2P', monospace;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            overflow-x: hidden;
            position: relative;
            padding: 20px;
        }

        /* Pixel grid background effect */
        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background-image: 
                linear-gradient(rgba(147, 51, 234, 0.07) 1px, transparent 1px),
                linear-gradient(90deg, rgba(147, 51, 234, 0.07) 1px, transparent 1px);
            background-size: 20px 20px;
            pointer-events: none;
            z-index: 0;
        }

        .container {
            z-index: 10;
            max-width: 650px;
            width: 100%;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 25px;
        }

        .title-box {
            background-color: #1a102f;
            border: 4px solid #a855f7;
            box-shadow: 6px 6px 0px #000000, 0 0 15px rgba(168, 85, 247, 0.4);
            padding: 20px;
            width: 100%;
        }

        h1 {
            color: #e9d5ff;
            font-size: 1.1rem;
            line-height: 1.8;
            text-shadow: 2px 2px #000000, 0 0 8px #a855f7;
            word-break: break-word;
        }

        /* Pixel Envelope */
        .envelope-wrapper {
            position: relative;
            cursor: pointer;
            margin: 20px 0;
            transition: transform 0.2s;
        }

        .envelope-wrapper:hover {
            transform: scale(1.05);
        }

        .pixel-envelope {
            width: 140px;
            height: 100px;
            background-color: #ffffff;
            border: 4px solid #000000;
            position: relative;
            box-shadow: 6px 6px 0px #7e22ce;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .envelope-flap {
            position: absolute;
            top: 0;
            left: 0;
            width: 0;
            height: 0;
            border-left: 66px solid transparent;
            border-right: 66px solid transparent;
            border-top: 45px solid #c084fc;
            transform-origin: top;
            transition: transform 0.4s ease;
            z-index: 3;
        }

        .pixel-heart-icon {
            width: 24px;
            height: 24px;
            background-color: #a855f7;
            position: relative;
            z-index: 2;
            transform: rotate(-45deg);
            margin-top: 10px;
            box-shadow: 0 0 8px #c084fc;
        }

        .pixel-heart-icon::before,
        .pixel-heart-icon::after {
            content: "";
            width: 24px;
            height: 24px;
            background-color: #a855f7;
            border-radius: 50%;
            position: absolute;
        }

        .pixel-heart-icon::before {
            top: -12px;
            left: 0;
        }

        .pixel-heart-icon::after {
            left: 12px;
            top: 0;
        }

        .click-hint {
            font-size: 0.6rem;
            color: #c084fc;
            margin-top: 12px;
            animation: blink 1.2s infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }

        /* Pixel Letter Modal */
        .letter-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(13, 9, 20, 0.85);
            backdrop-filter: blur(4px);
            z-index: 100;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .letter-content {
            background-color: #ffffff;
            color: #0d0914;
            border: 6px solid #a855f7;
            box-shadow: 10px 10px 0px #000000;
            padding: 30px 20px;
            max-width: 500px;
            width: 100%;
            text-align: left;
            position: relative;
            max-height: 85vh;
            overflow-y: auto;
        }

        .letter-content p {
            font-size: 0.65rem;
            line-height: 1.8;
            margin-bottom: 15px;
            color: #1a102f;
        }

        .letter-signature {
            text-align: right;
            font-weight: bold;
            color: #7e22ce;
            margin-top: 25px;
            font-size: 0.75rem;
        }

        .close-btn {
            background-color: #a855f7;
            color: #ffffff;
            border: 3px solid #000000;
            padding: 10px 15px;
            font-family: 'Press Start 2P', monospace;
            font-size: 0.6rem;
            cursor: pointer;
            margin-top: 15px;
            display: block;
            width: 100%;
            text-align: center;
            box-shadow: 4px 4px 0px #000000;
        }

        .close-btn:active {
            transform: translate(2px, 2px);
            box-shadow: 2px 2px 0px #000000;
        }

        /* Controls / Buttons */
        .btn-pixel {
            background-color: #7e22ce;
            color: #ffffff;
            border: 4px solid #ffffff;
            padding: 14px 20px;
            font-family: 'Press Start 2P', monospace;
            font-size: 0.65rem;
            cursor: pointer;
            box-shadow: 5px 5px 0px #000000;
            transition: background-color 0.2s;
        }

        .btn-pixel:hover {
            background-color: #9333ea;
        }

        .btn-pixel:active {
            transform: translate(3px, 3px);
            box-shadow: 2px 2px 0px #000000;
        }

        /* Pixel Hearts Floating */
        .floating-heart {
            position: fixed;
            pointer-events: none;
            z-index: 1;
            font-size: 16px;
            animation: floatUp linear forwards;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(100vh) scale(0.8);
                opacity: 1;
            }
            100% {
                transform: translateY(-10vh) scale(1.2);
                opacity: 0;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Main Message Box -->
        <div class="title-box">
            <h1>Luiz, amo você com todo meu coração</h1>
        </div>

        <!-- Envelope -->
        <div class="envelope-wrapper" onclick="openLetter()">
            <div class="pixel-envelope">
                <div class="envelope-flap" id="flap"></div>
                <div class="pixel-heart-icon"></div>
            </div>
            <div class="click-hint">[ CLIQUE PARA ABRIR ]</div>
        </div>

        <!-- Extra Action Button -->
        <button class="btn-pixel" onclick="spawnHeartBurst()">+ MAIS AMOR 💜</button>
    </div>

    <!-- Letter Popup Modal -->
    <div class="letter-modal" id="letterModal">
        <div class="letter-content">
            <p>Meu amor, Luiz,</p>
            <p>Mesmo com toda essa distância entre nós e sem termos nos visto pessoalmente ainda, o que eu sinto por você é mais real do que cualquier outra coisa.</p>
            <p>Você se tornou a minha pessoa favorita, o meu porto seguro e a minha maior certeza diária. Nosso amor prova todos os dias que a conexão de duas almas é infinitamente mais forte do que qualquer espaço físico.</p>
            <p>Mal posso esperar pelo dia em que a distância vai virar só uma lembrança e finalmente poderemos estar no mesmo lugar.</p>
            <p class="letter-signature">De: Emilia</p>
            <button class="close-btn" onclick="closeLetter()">FECHAR CARTA</button>
        </div>
    </div>

    <script>
        // Open & Close Letter
        function openLetter() {
            document.getElementById('flap').style.transform = 'rotateX(180deg)';
            setTimeout(() => {
                document.getElementById('letterModal').style.display = 'flex';
                spawnHeartBurst();
            }, 300);
        }

        function closeLetter() {
            document.getElementById('letterModal').style.display = 'none';
            document.getElementById('flap').style.transform = 'rotateX(0deg)';
        }

        // Floating Hearts Generator
        const heartTypes = ['💜', '🤍', '🖤', '💜', '✨'];

        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('floating-heart');
            heart.innerText = heartTypes[Math.floor(Math.random() * heartTypes.length)];
            heart.style.left = Math.random() * 100 + 'vw';
            
            const duration = Math.random() * 3 + 4; // 4s to 7s
            heart.style.animationDuration = duration + 's';
            
            const size = Math.random() * 12 + 12; // 12px to 24px
            heart.style.fontSize = size + 'px';

            document.body.appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, duration * 1000);
        }

        // Continuous heart spawning
        setInterval(createHeart, 400);

        // Burst of hearts on interaction
        function spawnHeartBurst() {
            for (let i = 0; i < 15; i++) {
                setTimeout(createHeart, i * 60);
            }
        }
    </script>
</body>
</html>
