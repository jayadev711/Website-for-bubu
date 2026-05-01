<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be Mine?</title>
    <style>
        :root {
            --primary-pink: #ff4d6d;
            --secondary-pink: #ff85a1;
            --bg-color: #fff0f3;
        }

        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: var(--bg-color);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }

        .container {
            text-align: center;
            background: white;
            padding: 3rem;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(255, 77, 109, 0.2);
            max-width: 400px;
            width: 90%;
            z-index: 10;
        }

        .gif-container img {
            width: 200px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        h1 {
            color: var(--primary-pink);
            font-size: 1.8rem;
            margin-bottom: 1.5rem;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            position: relative;
            height: 50px;
        }

        button {
            padding: 12px 25px;
            font-size: 1.1rem;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s;
        }

        #yesBtn {
            background-color: var(--primary-pink);
            color: white;
        }

        #yesBtn:hover {
            transform: scale(1.1);
            background-color: #ff758f;
        }

        #noBtn {
            background-color: #dee2e6;
            color: #495057;
            position: absolute; /* Needed for the dodging effect */
            right: 50px;
        }

        /* Success screen styles */
        .hidden {
            display: none;
        }

        .celebration {
            animation: pop 0.5s ease-out;
        }

        @keyframes pop {
            0% { transform: scale(0.5); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>

    <div class="container" id="mainContainer">
        <div class="gif-container">
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHIycXNueG1mN3BvNmJmZ3NueG1mN3BvNmJmZ3NueG1mN3BvJmVwPXYxX2ludGVybmFsX2dpZl9ieV9pZCZjdD1n/c76IJLufpNwSULPk2m/giphy.gif" alt="Cute bear">
        </div>
        <h1 id="question">Will you be my Valentine? ❤️</h1>
        
        <div class="buttons">
            <button id="yesBtn">Yes! 💖</button>
            <button id="noBtn">No 🙈</button>
        </div>
    </div>

    <div class="container hidden" id="successContainer">
        <div class="gif-container">
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNXA4eWp6N3BvNmJmZ3NueG1mN3BvNmJmZ3NueG1mN3BvJmVwPXYxX2ludGVybmFsX2dpZl9ieV9pZCZjdD1n/T866tiFv2p0W7mQ0N0/giphy.gif" alt="Happy bear">
        </div>
        <h1 class="celebration">Yay! See you soon! 😘</h1>
    </div>

    <script>
        const noBtn = document.getElementById('noBtn');
        const yesBtn = document.getElementById('yesBtn');
        const mainContainer = document.getElementById('mainContainer');
        const successContainer = document.getElementById('successContainer');

        // Function to move the "No" button
        const moveButton = () => {
            // Calculate random positions within the viewport, but keep the button clickable
            const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
            const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
            
            noBtn.style.position = 'fixed';
            noBtn.style.left = `${x}px`;
            noBtn.style.top = `${y}px`;
        };

        // Move button on hover (Desktop)
        noBtn.addEventListener('mouseover', moveButton);

        // Move button on click/tap (Mobile)
        noBtn.addEventListener('click', (e) => {
            e.preventDefault();
            moveButton();
        });

        // Show success screen
        yesBtn.addEventListener('click', () => {
            mainContainer.classList.add('hidden');
            successContainer.classList.remove('hidden');
            
            // Optional: Launch confetti (using basic browser alert or extra library)
            createConfetti();
        });

        // Simple confetti effect
        function createConfetti() {
            for(let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.innerText = '❤️';
                confetti.style.position = 'fixed';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.top = '-20px';
                confetti.style.fontSize = Math.random() * 20 + 10 + 'px';
                confetti.style.zIndex = '999';
                confetti.style.pointerEvents = 'none';
                document.body.appendChild(confetti);

                const animation = confetti.animate([
                    { transform: 'translateY(0) rotate(0deg)', opacity: 1 },
                    { transform: `translateY(100vh) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                ], {
                    duration: Math.random() * 3000 + 2000,
                    easing: 'linear'
                });

                animation.onfinish = () => confetti.remove();
            }
        }
    </script>
</body>
</html>
