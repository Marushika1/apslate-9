<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Asphalt Racer - Pro Racing Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            color: #fff;
        }

        #mainMenu {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .menu-content {
            text-align: center;
        }

        .game-title {
            font-size: 64px;
            font-weight: bold;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #ff6b00, #ffa500, #ff6b00);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 30px rgba(255, 107, 0, 0.5);
            letter-spacing: 3px;
        }

        .subtitle {
            font-size: 18px;
            color: #aaa;
            margin-bottom: 40px;
            letter-spacing: 2px;
        }

        .car-selector {
            margin-bottom: 40px;
        }

        .car-selector h3 {
            color: #ff6b00;
            margin-bottom: 20px;
            font-size: 18px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .car-grid {
            display: grid;
            grid-template-columns: repeat(3, 120px);
            gap: 15px;
            margin-bottom: 30px;
            justify-content: center;
        }

        .car-option {
            padding: 15px;
            border: 2px solid #333;
            background: rgba(255, 107, 0, 0.1);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            text-align: center;
        }

        .car-option:hover {
            border-color: #ff6b00;
            background: rgba(255, 107, 0, 0.2);
            transform: translateY(-5px);
        }

        .car-option.active {
            border-color: #ff6b00;
            background: rgba(255, 107, 0, 0.3);
            box-shadow: 0 0 20px rgba(255, 107, 0, 0.5);
        }

        .car-emoji {
            font-size: 40px;
            margin-bottom: 8px;
        }

        .car-name {
            font-size: 12px;
            color: #aaa;
        }

        .color-selector {
            margin-bottom: 40px;
        }

        .color-selector h3 {
            color: #ff6b00;
            margin-bottom: 15px;
            font-size: 18px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .color-grid {
            display: grid;
            grid-template-columns: repeat(8, 50px);
            gap: 10px;
            justify-content: center;
        }

        .color-box {
            width: 50px;
            height: 50px;
            border: 2px solid #333;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .color-box:hover {
            transform: scale(1.1);
        }

        .color-box.active {
            border: 3px solid #fff;
            box-shadow: 0 0 15px currentColor;
        }

        .difficulty-selector {
            margin-bottom: 40px;
        }

        .difficulty-selector h3 {
            color: #ff6b00;
            margin-bottom: 15px;
            font-size: 18px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .difficulty-buttons {
            display: flex;
            gap: 15px;
            justify-content: center;
        }

        .difficulty-btn {
            padding: 12px 25px;
            border: 2px solid #333;
            background: rgba(255, 107, 0, 0.1);
            color: #fff;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
            text-transform: uppercase;
            font-size: 12px;
            letter-spacing: 1px;
        }

        .difficulty-btn:hover {
            border-color: #ff6b00;
            background: rgba(255, 107, 0, 0.2);
        }

        .difficulty-btn.active {
            border-color: #ff6b00;
            background: #ff6b00;
            color: #000;
        }

        .start-btn {
            padding: 15px 50px;
            font-size: 16px;
            background: linear-gradient(45deg, #ff6b00, #ffa500);
            color: #000;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
            transition: all 0.3s;
            box-shadow: 0 0 30px rgba(255, 107, 0, 0.5);
        }

        .start-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 40px rgba(255, 107, 0, 0.8);
        }

        .start-btn:active {
            transform: scale(0.98);
        }

        #gameContainer {
            display: none;
            width: 100vw;
            height: 100vh;
            position: relative;
            overflow: hidden;
        }

        canvas {
            display: block;
            width: 100%;
            height: 100%;
        }

        .hud {
            position: fixed;
            top: 20px;
            left: 20px;
            right: 20px;
            z-index: 100;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #fff;
        }

        .hud-left {
            font-size: 24px;
            font-weight: bold;
            letter-spacing: 2px;
        }

        .hud-stats {
            display: flex;
            gap: 30px;
            font-size: 18px;
            font-weight: bold;
        }

        .stat {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: rgba(0, 0, 0, 0.5);
            padding: 10px 20px;
            border-radius: 5px;
            border-left: 3px solid #ff6b00;
        }

        .stat-label {
            font-size: 12px;
            color: #aaa;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .stat-value {
            font-size: 24px;
            color: #ff6b00;
        }

        .speedometer {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 150px;
            height: 150px;
            border: 3px solid #ff6b00;
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: rgba(0, 0, 0, 0.7);
            z-index: 100;
        }

        .speed-value {
            font-size: 32px;
            font-weight: bold;
            color: #ff6b00;
        }

        .speed-unit {
            font-size: 12px;
            color: #aaa;
            text-transform: uppercase;
        }

        .game-over-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }

        .game-over-content {
            text-align: center;
        }

        .game-over-title {
            font-size: 56px;
            font-weight: bold;
            margin-bottom: 20px;
            color: #ff6b00;
            text-transform: uppercase;
            letter-spacing: 3px;
        }

        .game-over-stats {
            font-size: 20px;
            margin-bottom: 30px;
            color: #fff;
        }

        .game-over-stats p {
            margin: 10px 0;
        }

        .game-over-buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
        }

        .btn-menu, .btn-restart {
            padding: 12px 30px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s;
        }

        .btn-restart {
            background: linear-gradient(45deg, #ff6b00, #ffa500);
            color: #000;
        }

        .btn-restart:hover {
            transform: scale(1.05);
        }

        .btn-menu {
            background: transparent;
            border: 2px solid #ff6b00;
            color: #ff6b00;
        }

        .btn-menu:hover {
            background: rgba(255, 107, 0, 0.2);
        }

        .controls-info {
            position: fixed;
            bottom: 30px;
            left: 30px;
            background: rgba(0, 0, 0, 0.7);
            padding: 15px 20px;
            border-left: 3px solid #ff6b00;
            font-size: 12px;
            z-index: 100;
            max-width: 200px;
        }

        .controls-info p {
            margin: 5px 0;
            color: #aaa;
        }

        .controls-info strong {
            color: #ff6b00;
        }
    </style>
</head>
<body>
    <!-- MAIN MENU -->
    <div id="mainMenu">
        <div class="menu-content">
            <div class="game-title">🏎️ ASPHALT RACER</div>
            <div class="subtitle">Pro Racing Championship</div>

            <!-- Car Selector -->
            <div class="car-selector">
                <h3>SELECT YOUR CAR</h3>
                <div class="car-grid">
                    <div class="car-option active" data-car="sports">
                        <div class="car-emoji">🏎️</div>
                        <div class="car-name">Sports</div>
                    </div>
                    <div class="car-option" data-car="supercar">
                        <div class="car-emoji">🔴</div>
                        <div class="car-name">Supercar</div>
                    </div>
                    <div class="car-option" data-car="hypercar">
                        <div class="car-emoji">⭐</div>
                        <div class="car-name">Hypercar</div>
                    </div>
                    <div class="car-option" data-car="truck">
                        <div class="car-emoji">🚙</div>
                        <div class="car-name">Truck</div>
                    </div>
                    <div class="car-option" data-car="police">
                        <div class="car-emoji">🚓</div>
                        <div class="car-name">Police</div>
                    </div>
                    <div class="car-option" data-car="taxi">
                        <div class="car-emoji">🚕</div>
                        <div class="car-name">Taxi</div>
                    </div>
                </div>
            </div>

            <!-- Color Selector -->
            <div class="color-selector">
                <h3>SELECT COLOR</h3>
                <div class="color-grid">
                    <div class="color-box active" data-color="#FF0000" style="background: #FF0000;"></div>
                    <div class="color-box" data-color="#FF6B00" style="background: #FF6B00;"></div>
                    <div class="color-box" data-color="#FFD700" style="background: #FFD700;"></div>
                    <div class="color-box" data-color="#00FF00" style="background: #00FF00;"></div>
                    <div class="color-box" data-color="#00CCFF" style="background: #00CCFF;"></div>
                    <div class="color-box" data-color="#0066FF" style="background: #0066FF;"></div>
                    <div class="color-box" data-color="#FF00FF" style="background: #FF00FF;"></div>
                    <div class="color-box" data-color="#FFFFFF" style="background: #FFFFFF;"></div>
                </div>
            </div>

            <!-- Difficulty Selector -->
            <div class="difficulty-selector">
                <h3>SELECT DIFFICULTY</h3>
                <div class="difficulty-buttons">
                    <button class="difficulty-btn active" data-difficulty="easy">Easy</button>
                    <button class="difficulty-btn" data-difficulty="normal">Normal</button>
                    <button class="difficulty-btn" data-difficulty="hard">Hard</button>
                    <button class="difficulty-btn" data-difficulty="insane">Insane</button>
                </div>
            </div>

            <button class="start-btn" onclick="startGame()">▶ START RACE</button>
        </div>
    </div>

    <!-- GAME CONTAINER -->
    <div id="gameContainer">
        <canvas id="gameCanvas"></canvas>

        <!-- HUD -->
        <div class="hud">
            <div class="hud-left">ASPHALT RACER</div>
            <div class="hud-stats">
                <div class="stat">
                    <span class="stat-label">Score</span>
                    <span class="stat-value" id="scoreDisplay">0</span>
                </div>
                <div class="stat">
                    <span class="stat-label">Combo</span>
                    <span class="stat-value" id="comboDisplay">0x</span>
                </div>
                <div class="stat">
                    <span class="stat-label">Level</span>
                    <span class="stat-value" id="levelDisplay">1</span>
                </div>
            </div>
        </div>

        <!-- Speedometer -->
        <div class="speedometer">
            <div class="speed-value" id="speedValue">0</div>
            <div class="speed-unit">km/h</div>
        </div>

        <!-- Controls Info -->
        <div class="controls-info">
            <p><strong>←→</strong> Steer</p>
            <p><strong>↑</strong> Accelerate</p>
            <p><strong>↓</strong> Brake</p>
            <p><strong>SPACE</strong> Nitro</p>
        </div>
    </div>

    <!-- GAME OVER OVERLAY -->
    <div class="game-over-overlay" id="gameOverOverlay">
        <div class="game-over-content">
            <div class="game-over-title">🏁 RACE FINISHED</div>
            <div class="game-over-stats">
                <p>Final Score: <span id="finalScore">0</span></p>
                <p>Best Combo: <span id="bestCombo">0x</span></p>
                <p>Max Speed: <span id="maxSpeed">0</span> km/h</p>
                <p>Level Reached: <span id="finalLevel">1</span></p>
            </div>
            <div class="game-over-buttons">
                <button class="btn-restart" onclick="restartGame()">🔄 RESTART</button>
                <button class="btn-menu" onclick="goToMenu()">🏠 MENU</button>
            </div>
        </div>
    </div>

    <script>
        // ============================================
        // GAME VARIABLES
        // ============================================
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let selectedCar = 'sports';
        let selectedColor = '#FF0000';
        let selectedDifficulty = 'easy';

        let gameRunning = false;
        let score = 0;
        let combo = 0;
        let bestCombo = 0;
        let level = 1;
        let currentSpeed = 0;
        let maxSpeed = 0;
        let frameCount = 0;

        // ============================================
        // MENU LISTENERS
        // ============================================
        document.querySelectorAll('.car-option').forEach(option => {
            option.addEventListener('click', () => {
                document.querySelectorAll('.car-option').forEach(o => o.classList.remove('active'));
                option.classList.add('active');
                selectedCar = option.dataset.car;
            });
        });

        document.querySelectorAll('.color-box').forEach(option => {
            option.addEventListener('click', () => {
                document.querySelectorAll('.color-box').forEach(o => o.classList.remove('active'));
                option.classList.add('active');
                selectedColor = option.dataset.color;
            });
        });

        document.querySelectorAll('.difficulty-btn').forEach(option => {
            option.addEventListener('click', () => {
                document.querySelectorAll('.difficulty-btn').forEach(o => o.classList.remove('active'));
                option.classList.add('active');
                selectedDifficulty = option.dataset.difficulty;
            });
        });

        // ============================================
        // GAME OBJECTS
        // ============================================
        const player = {
            x: canvas.width / 2,
            y: canvas.height - 150,
            width: 50,
            height: 80,
            vx: 0,
            vy: 0,
            speed: 0,
            maxSpeed: 20,
            acceleration: 0.5,
            friction: 0.95,
            steering: 0,
            steeringSpeed: 0.1,
            maxSteering: 0.3,
            nitro: 100,
            maxNitro: 100,
            nitroActive: false
        };

        let obstacles = [];
        let particles = [];
        let roadOffset = 0;

        // ============================================
        // KEYBOARD INPUT
        // ============================================
        const keys = {};
        window.addEventListener('keydown', (e) => {
            keys[e.key] = true;
            if (e.key === ' ') {
                e.preventDefault();
                activateNitro();
            }
        });
        window.addEventListener('keyup', (e) => {
            keys[e.key] = false;
        });

        // ============================================
        // GAME FUNCTIONS
        // ============================================
        function startGame() {
            document.getElementById('mainMenu').style.display = 'none';
            document.getElementById('gameContainer').style.display = 'block';
            gameRunning = true;
            score = 0;
            combo = 0;
            bestCombo = 0;
            level = 1;
            maxSpeed = 0;
            frameCount = 0;
            player.speed = 0;
            player.x = canvas.width / 2;
            player.y = canvas.height - 150;
            obstacles = [];
            gameLoop();
        }

        function goToMenu() {
            gameRunning = false;
            document.getElementById('mainMenu').style.display = 'flex';
            document.getElementById('gameContainer').style.display = 'none';
            document.getElementById('gameOverOverlay').style.display = 'none';
        }

        function restartGame() {
            document.getElementById('gameOverOverlay').style.display = 'none';
            startGame();
        }

        function activateNitro() {
            if (gameRunning && player.nitro > 50) {
                player.nitroActive = true;
                player.nitro -= 20;
                player.maxSpeed = 35;
                setTimeout(() => {
                    player.nitroActive = false;
                    player.maxSpeed = 20;
                }, 3000);
            }
        }

        // ============================================
        // DRAWING FUNCTIONS
        // ============================================
        function drawRoad() {
            // Road background
            ctx.fillStyle = '#1a1a1a';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Road
            ctx.fillStyle = '#2d2d2d';
            ctx.fillRect(canvas.width / 2 - 150, 0, 300, canvas.height);

            // Center line (dashed)
            ctx.strokeStyle = '#FFD700';
            ctx.lineWidth = 3;
            ctx.setLineDash([40, 20]);
            ctx.beginPath();
            ctx.moveTo(canvas.width / 2, roadOffset);
            ctx.lineTo(canvas.width / 2, canvas.height + roadOffset);
            ctx.stroke();
            ctx.setLineDash([]);

            // Side lines
            ctx.strokeStyle = '#fff';
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.moveTo(canvas.width / 2 - 150, 0);
            ctx.lineTo(canvas.width / 2 - 150, canvas.height);
            ctx.stroke();

            ctx.beginPath();
            ctx.moveTo(canvas.width / 2 + 150, 0);
            ctx.lineTo(canvas.width / 2 + 150, canvas.height);
            ctx.stroke();
        }

        function drawPlayer() {
            ctx.save();
            ctx.translate(player.x, player.y);
            ctx.rotate(player.steering * 0.5);

            // Car body
            ctx.fillStyle = selectedColor;
            ctx.fillRect(-player.width / 2, -player.height / 2, player.width, player.height);

            // Car outline
            ctx.strokeStyle = '#000';
            ctx.lineWidth = 2;
            ctx.strokeRect(-player.width / 2, -player.height / 2, player.width, player.height);

            // Windshield
            ctx.fillStyle = 'rgba(100, 200, 255, 0.6)';
            ctx.fillRect(-player.width / 2 + 5, -player.height / 2 + 10, player.width - 10, 15);

            // Wheels
            ctx.fillStyle = '#000';
            ctx.fillRect(-player.width / 2 + 5, -player.height / 2, 8, 8);
            ctx.fillRect(player.width / 2 - 13, -player.height / 2, 8, 8);
            ctx.fillRect(-player.width / 2 + 5, player.height / 2 - 8, 8, 8);
            ctx.fillRect(player.width / 2 - 13, player.height / 2 - 8, 8, 8);

            // Nitro effect
            if (player.nitroActive) {
                ctx.fillStyle = 'rgba(255, 150, 0, 0.7)';
                ctx.fillRect(-player.width / 2, player.height / 2, player.width, 30);
            }

            ctx.restore();
        }

        function drawObstacle(obstacle) {
            ctx.fillStyle = '#FF3333';
            ctx.fillRect(obstacle.x - obstacle.width / 2, obstacle.y - obstacle.height / 2, obstacle.width, obstacle.height);
            ctx.strokeStyle = '#990000';
            ctx.lineWidth = 2;
            ctx.strokeRect(obstacle.x - obstacle.width / 2, obstacle.y - obstacle.height / 2, obstacle.width, obstacle.height);

            // Warning stripes
            ctx.strokeStyle = '#FFD700';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(obstacle.x - obstacle.width / 2, obstacle.y - obstacle.height / 2);
            ctx.lineTo(obstacle.x + obstacle.width / 2, obstacle.y + obstacle.height / 2);
            ctx.stroke();
        }

        function createParticles(x, y, color) {
            for (let i = 0; i < 8; i++) {
                particles.push({
                    x: x,
                    y: y,
                    vx: (Math.random() - 0.5) * 8,
                    vy: Math.random() * 5,
                    life: 30,
                    color: color
                });
            }
        }

        // ============================================
        // GAME LOGIC
        // ============================================
        function updatePlayer() {
            // Steering
            if (keys['ArrowLeft'] || keys['a'] || keys['A']) {
                player.steering = Math.max(player.steering - player.steeringSpeed, -player.maxSteering);
            } else if (keys['ArrowRight'] || keys['d'] || keys['D']) {
                player.steering = Math.min(player.steering + player.steeringSpeed, player.maxSteering);
            } else {
                player.steering *= 0.9;
            }

            // Acceleration
            if (keys['ArrowUp'] || keys['w'] || keys['W']) {
                player.speed = Math.min(player.speed + player.acceleration, player.maxSpeed);
            } else if (keys['ArrowDown'] || keys['s'] || keys['S']) {
                player.speed = Math.max(player.speed - player.acceleration * 2, 0);
            } else {
                player.speed *= player.friction;
            }

            // Movement
            player.x += player.steering * player.speed * 2;
            currentSpeed = Math.round(player.speed * 5);
            maxSpeed = Math.max(maxSpeed, currentSpeed);

            // Boundary
            const minX = canvas.width / 2 - 120;
            const maxX = canvas.width / 2 + 120;
            if (player.x < minX) player.x = minX;
            if (player.x > maxX) player.x = maxX;

            // Nitro regen
            if (player.nitro < player.maxNitro) {
                player.nitro += 0.5;
            }
        }

        function createObstacle() {
            const lanes = [canvas.width / 2 - 80, canvas.width / 2, canvas.width / 2 + 80];
            const randomLane = lanes[Math.floor(Math.random() * lanes.length)];
            obstacles.push({
                x: randomLane,
                y: -50,
                width: 50,
                height: 80,
                speed: 5 + (level * 1.5)
            });
        }

        function updateObstacles() {
            for (let i = obstacles.length - 1; i >= 0; i--) {
                obstacles[i].y += obstacles[i].speed;

                // Collision
                const dx = player.x - obstacles[i].x;
                const dy = player.y - obstacles[i].y;
                const distance = Math.sqrt(dx * dx + dy * dy);

                if (distance < 50) {
                    createParticles(obstacles[i].x, obstacles[i].y, '#FF3333');
                    obstacles.splice(i, 1);
                    endGame();
                } else if (obstacles[i].y > canvas.height) {
                    obstacles.splice(i, 1);
                    score += 10 * (combo || 1);
                    combo++;
                    bestCombo = Math.max(bestCombo, combo);
                    if (score % 200 === 0) level++;
                }
            }
        }

        function updateParticles() {
            for (let i = particles.length - 1; i >= 0; i--) {
                particles[i].x += particles[i].vx;
                particles[i].y += particles[i].vy;
                particles[i].life--;
                if (particles[i].life <= 0) particles.splice(i, 1);
            }
        }

        function drawParticles() {
            particles.forEach(p => {
                ctx.fillStyle = p.color;
                ctx.globalAlpha = p.life / 30;
                ctx.fillRect(p.x, p.y, 5, 5);
                ctx.globalAlpha = 1;
            });
        }

        function endGame() {
            gameRunning = false;
            document.getElementById('finalScore').textContent = score;
            document.getElementById('bestCombo').textContent = bestCombo + 'x';
            document.getElementById('maxSpeed').textContent = maxSpeed;
            document.getElementById('finalLevel').textContent = level;
            document.getElementById('gameOverOverlay').style.display = 'flex';
        }

        // ============================================
        // GAME LOOP
        // ============================================
        function gameLoop() {
            if (!gameRunning) return;

            // Clear and draw
            drawRoad();
            roadOffset += currentSpeed * 0.5;

            updatePlayer();
            updateObstacles();
            updateParticles();

            frameCount++;
            if (frameCount % Math.max(50 - level * 5, 20) === 0) {
                createObstacle();
            }

            // Draw
            drawParticles();
            obstacles.forEach(drawObstacle);
            drawPlayer();

            // Update HUD
            document.getElementById('scoreDisplay').textContent = score;
            document.getElementById('comboDisplay').textContent = combo + 'x';
            document.getElementById('levelDisplay').textContent = level;
            document.getElementById('speedValue').textContent = currentSpeed;

            requestAnimationFrame(gameLoop);
        }

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
