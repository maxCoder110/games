# games
games
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>NEON ARCADE: ULTIMATE COLLECTION</title>
    <style>
        /* --- RETRO ARCADE CSS --- */
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Rajdhani:wght@500;700&display=swap');

        body {
            margin: 0;
            overflow: hidden;
            background-color: #050510;
            font-family: 'Rajdhani', sans-serif;
            color: white;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        /* Moving Grid Background */
        .retro-bg {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(180deg, #000 0%, #110022 100%);
            z-index: -2;
        }
        .grid-floor {
            position: absolute;
            bottom: -50%;
            left: -50%;
            width: 200%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(255, 0, 255, 0.3) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 0, 255, 0.3) 1px, transparent 1px);
            background-size: 50px 50px;
            transform: perspective(500px) rotateX(60deg);
            animation: moveGrid 3s linear infinite;
            z-index: -1;
            opacity: 0.5;
        }
        @keyframes moveGrid {
            0% { transform: perspective(500px) rotateX(60deg) translateY(0); }
            100% { transform: perspective(500px) rotateX(60deg) translateY(50px); }
        }

        /* CRT Scanline Overlay */
        .crt-overlay {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            background-size: 100% 2px, 3px 100%;
            pointer-events: none;
            z-index: 100;
        }

        /* UI Elements */
        #menu-container {
            text-align: center;
            z-index: 10;
            transition: opacity 0.5s;
        }

        h1 {
            font-family: 'Press Start 2P', cursive;
            font-size: 60px;
            color: #fff;
            text-transform: uppercase;
            text-shadow: 
                3px 3px 0px #ff00de, 
                -3px -3px 0px #00ffff;
            margin-bottom: 10px;
            animation: pulseTitle 2s infinite;
        }

        .subtitle {
            font-size: 24px;
            letter-spacing: 5px;
            color: #00ffff;
            text-shadow: 0 0 10px #00ffff;
            margin-bottom: 60px;
        }

        .card-container {
            display: flex;
            gap: 30px;
            justify-content: center;
            align-items: center;
        }

        .game-card {
            width: 250px;
            height: 350px;
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: 15px;
            background: rgba(0,0,0,0.6);
            backdrop-filter: blur(5px);
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 20px;
            box-sizing: border-box;
        }

        /* Card Themes */
        .card-1 { border-color: #00ffcc; box-shadow: 0 0 15px rgba(0, 255, 204, 0.2); }
        .card-1:hover { transform: translateY(-20px) scale(1.05); box-shadow: 0 0 40px #00ffcc; background: rgba(0, 255, 204, 0.1); }
        
        .card-2 { border-color: #ffaa00; box-shadow: 0 0 15px rgba(255, 170, 0, 0.2); }
        .card-2:hover { transform: translateY(-20px) scale(1.05); box-shadow: 0 0 40px #ffaa00; background: rgba(255, 170, 0, 0.1); }

        .card-3 { border-color: #ff00de; box-shadow: 0 0 15px rgba(255, 0, 222, 0.2); }
        .card-3:hover { transform: translateY(-20px) scale(1.05); box-shadow: 0 0 40px #ff00de; background: rgba(255, 0, 222, 0.1); }

        .game-title {
            font-family: 'Press Start 2P', cursive;
            font-size: 16px;
            line-height: 1.5;
            margin-bottom: 10px;
            text-shadow: 2px 2px 0px #000;
        }
        .card-1 .game-title { color: #00ffcc; }
        .card-2 .game-title { color: #ffaa00; }
        .card-3 .game-title { color: #ff00de; }

        .game-desc {
            font-size: 14px;
            color: #ccc;
        }

        /* Game Iframe Container */
        #game-wrapper {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #000;
            z-index: 50;
            display: none;
        }

        iframe {
            width: 100%;
            height: 100%;
            border: none;
        }

        #back-button {
            position: absolute;
            top: 20px;
            left: 20px;
            background: rgba(0,0,0,0.8);
            border: 2px solid #fff;
            color: #fff;
            padding: 10px 20px;
            font-family: 'Press Start 2P';
            cursor: pointer;
            z-index: 60;
            text-transform: uppercase;
        }
        #back-button:hover {
            background: #fff;
            color: #000;
        }

        @keyframes pulseTitle {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.02); opacity: 0.9; }
            100% { transform: scale(1); opacity: 1; }
        }
    </style>
</head>
<body>

    <div class="retro-bg"></div>
    <div class="grid-floor"></div>
    <div class="crt-overlay"></div>

    <div id="menu-container">
        <h1>NEON ARCADE</h1>
        <div class="subtitle">SELECT YOUR REALITY</div>

        <div class="card-container">
            <div class="game-card card-1" onclick="loadGame('game1')">
                <div class="game-title">NEON CYCLE<br>GRID WARS</div>
                <div class="game-desc">Strategic Trail Battles. Trap your enemies.</div>
            </div>

            <div class="game-card card-2" onclick="loadGame('game2')">
                <div class="game-title">WARFARE SAGA<br>POWER UP</div>
                <div class="game-desc">Tank & Tron Hybrid. Defeat the bosses.</div>
            </div>

            <div class="game-card card-3" onclick="loadGame('game3')">
                <div class="game-title">NEON VOID<br>OVERDRIVE</div>
                <div class="game-desc">Infinite Runner. Dodge & Collect.</div>
            </div>
        </div>
    </div>

    <div id="game-wrapper">
        <button id="back-button" onclick="closeGame()">EXIT TO MENU</button>
        <iframe id="game-frame"></iframe>
    </div>

    <textarea id="code-game1" style="display:none;">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Neon Cycle: Grid Wars</title>
    <style>
        body { margin: 0; overflow: hidden; background-color: #050505; font-family: 'Courier New', Courier, monospace; }
        #ui {
            position: absolute; top: 20px; left: 20px; color: #00ffcc;
            text-shadow: 0 0 10px #00ffcc; pointer-events: none; z-index: 10;
        }
        #game-over {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
            color: white; font-size: 40px; text-align: center; display: none;
            text-shadow: 0 0 20px #ff0055; background: rgba(0,0,0,0.9); padding: 60px; 
            border: 4px solid #ff0055; box-shadow: 0 0 50px #ff0055;
            z-index: 20;
        }
        h1 { margin: 0; font-size: 24px; text-transform: uppercase; letter-spacing: 4px; }
        p { margin: 5px 0; font-size: 18px; }
        .controls { font-size: 14px; color: #888; margin-top: 10px; }
        .blink { animation: blinker 1s linear infinite; color: #ff0055; }
        @keyframes blinker { 50% { opacity: 0; } }
    </style>
</head>
<body>

<div id="ui">
    <h1>NEON CYCLE</h1>
    <p>Level: <span id="level">1</span></p>
    <p>Score: <span id="score">0</span></p>
    <p>Enemies: <span id="enemies">0</span></p>
    <div class="controls">ARROWS to Turn | SPACE to Boost</div>
</div>

<div id="game-over">
    <div style="font-size: 60px; margin-bottom: 10px;">SYSTEM FAILURE</div>
    <div class="blink">CRITICAL ERROR DETECTED</div>
    <div style="font-size: 20px; margin-top: 30px; color: #fff;">Press ENTER to Reboot</div>
</div>

<script type="importmap">
  {
    "imports": {
      "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
      "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
    }
  }
</script>

<script type="module">
import * as THREE from 'three';
import { UnrealBloomPass } from 'three/addons/postprocessing/UnrealBloomPass.js';
import { EffectComposer } from 'three/addons/postprocessing/EffectComposer.js';
import { RenderPass } from 'three/addons/postprocessing/RenderPass.js';

// --- CONFIGURATION ---
const GRID_SIZE = 240; 
const CELL_SIZE = 2; 
const SPEED_NORMAL = 1.0;
const SPEED_BOOST = 1.8;
const COLORS = {
    player: 0x00ffff,
    enemy: 0xff3300,
    wall: 0xaa00aa,
    grid: 0x111111
};

// --- GLOBALS ---
let scene, camera, renderer, composer;
let cycles = [];
let walls = [];
let particles = [];
let gridMap = new Set();
let isGameOver = false;
let level = 1;
let score = 0;
let trailLengthCap = 50; 
let screenShake = 0; // Visual impact variable

// DOM Elements
const uiLevel = document.getElementById('level');
const uiScore = document.getElementById('score');
const uiEnemies = document.getElementById('enemies');
const uiGameOver = document.getElementById('game-over');

// --- SETUP ---
function init() {
    scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x050505, 0.0025);

    camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 140, 120); // Higher camera for better view
    camera.lookAt(0, 0, 0);

    renderer = new THREE.WebGLRenderer({ antialias: false }); // False for retro feel
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // POST PROCESSING (The Glow)
    const renderScene = new RenderPass(scene, camera);
    const bloomPass = new UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 1.5, 0.4, 0.85);
    bloomPass.threshold = 0;
    bloomPass.strength = 1.5; 
    bloomPass.radius = 0.5;
    
    composer = new EffectComposer(renderer);
    composer.addPass(renderScene);
    composer.addPass(bloomPass);

    // Floor Grid
    const gridHelper = new THREE.GridHelper(GRID_SIZE * 2, GRID_SIZE / 2, 0x444444, 0x111111);
    scene.add(gridHelper);

    // Boundary
    createBoundary();

    // Lights
    const ambient = new THREE.AmbientLight(0x404040);
    scene.add(ambient);
    const dirLight = new THREE.DirectionalLight(0xffffff, 1);
    dirLight.position.set(50, 100, 50);
    scene.add(dirLight);

    window.addEventListener('resize', onWindowResize);
    window.addEventListener('keydown', handleInput);
    window.addEventListener('keyup', (e) => {
        if (e.code === 'Space' && cycles[0]) cycles[0].speed = SPEED_NORMAL;
    });

    startLevel();
    animate();
}

// --- GAME LOGIC ---

function startLevel() {
    // 1. Wipe everything existing
    killAllVisuals();
    
    isGameOver = false;
    trailLengthCap = 40 + (level * 20);
    
    // Spawn Player
    const player = new Cycle(0, 0, COLORS.player, true);
    cycles.push(player);

    // Spawn Enemies
    const enemyCount = Math.min(level + 1, 15);
    for(let i=0; i<enemyCount; i++) {
        let ex, ez;
        // Ensure enemies don't spawn on top of player
        do {
            ex = (Math.random() > 0.5 ? 1 : -1) * (20 + Math.random() * 80);
            ez = (Math.random() > 0.5 ? 1 : -1) * (20 + Math.random() * 80);
        } while (Math.abs(ex) < 30 && Math.abs(ez) < 30);
        
        cycles.push(new Cycle(ex, ez, COLORS.enemy, false));
    }

    // Spawn Random Obstacles
    if (level > 0) {
        let wallCount = level * 8;
        for(let i=0; i<wallCount; i++) {
            let wx = Math.floor((Math.random() * GRID_SIZE - GRID_SIZE/2) / CELL_SIZE) * CELL_SIZE;
            let wz = Math.floor((Math.random() * GRID_SIZE - GRID_SIZE/2) / CELL_SIZE) * CELL_SIZE;
            if(Math.abs(wx) < 30 && Math.abs(wz) < 30) continue; 
            createWall(wx, wz);
        }
    }

    updateUI();
}

// Cleans up meshes without explosion logic (used for restart)
function killAllVisuals() {
    cycles.forEach(c => {
        scene.remove(c.mesh);
        c.trailPoints.forEach(t => scene.remove(t.mesh));
    });
    walls.forEach(w => scene.remove(w));
    
    cycles = [];
    walls = [];
    gridMap.clear();
}

class Cycle {
    constructor(x, z, color, isPlayer) {
        this.isPlayer = isPlayer;
        this.color = color;
        this.speed = SPEED_NORMAL;
        this.alive = true;
        this.direction = isPlayer ? 0 : Math.floor(Math.random() * 4);
        this.nextDirection = this.direction;

        // Visuals
        const geometry = new THREE.BoxGeometry(2, 2, 4); 
        const material = new THREE.MeshStandardMaterial({ 
            color: color, 
            emissive: color,
            emissiveIntensity: 3.0
        });
        this.mesh = new THREE.Mesh(geometry, material);
        this.mesh.position.set(x, 1, z);
        scene.add(this.mesh);

        this.trailPoints = [];
        this.lastGridPos = { x: Math.round(x), z: Math.round(z) };
    }

    update() {
        if (!this.alive) return;

        // AI Logic
        if (!this.isPlayer) this.aiThink();

        // Rotation
        const targetRot = (this.direction === 0 ? Math.PI : this.direction === 1 ? Math.PI/2 : this.direction === 2 ? 0 : -Math.PI/2);
        this.mesh.rotation.y = targetRot;

        // Movement
        let dist = this.speed;
        let dx = 0, dz = 0;
        if (this.direction === 0) dz = -dist;
        else if (this.direction === 1) dx = dist;
        else if (this.direction === 2) dz = dist;
        else if (this.direction === 3) dx = -dist;

        this.mesh.position.x += dx;
        this.mesh.position.z += dz;

        // Grid Logic
        let currentGridX = Math.round(this.mesh.position.x / CELL_SIZE) * CELL_SIZE;
        let currentGridZ = Math.round(this.mesh.position.z / CELL_SIZE) * CELL_SIZE;

        if (currentGridX !== this.lastGridPos.x || currentGridZ !== this.lastGridPos.z) {
            
            // 1. Check for Walls/Trails
            let key = `${currentGridX},${currentGridZ}`;
            if (gridMap.has(key) || Math.abs(currentGridX) > GRID_SIZE || Math.abs(currentGridZ) > GRID_SIZE) {
                this.die();
                return;
            }

            // 2. Check Head-to-Head
            for(let other of cycles) {
                if(other !== this && other.alive) {
                    if (Math.abs(other.mesh.position.x - this.mesh.position.x) < 2 &&
                        Math.abs(other.mesh.position.z - this.mesh.position.z) < 2) {
                        this.die();
                        other.die();
                        return;
                    }
                }
            }

            // 3. Drop Trail
            this.addTrailSegment(this.lastGridPos.x, this.lastGridPos.z);
            this.lastGridPos = { x: currentGridX, z: currentGridZ };
            gridMap.add(key); 
            this.direction = this.nextDirection;
        }
    }

    addTrailSegment(x, z) {
        const geo = new THREE.BoxGeometry(CELL_SIZE, 2, CELL_SIZE);
        const mat = new THREE.MeshBasicMaterial({ color: this.color, transparent: true, opacity: 0.8 });
        const trailMesh = new THREE.Mesh(geo, mat);
        trailMesh.position.set(x, 1, z);
        scene.add(trailMesh);
        this.trailPoints.push({ x: x, z: z, mesh: trailMesh });

        if (this.trailPoints.length > trailLengthCap) {
            let old = this.trailPoints.shift();
            scene.remove(old.mesh);
            gridMap.delete(`${old.x},${old.z}`);
        }
    }

    aiThink() {
        // Look ahead
        let lookX = this.lastGridPos.x;
        let lookZ = this.lastGridPos.z;
        let step = CELL_SIZE;

        if (this.direction === 0) lookZ -= step;
        else if (this.direction === 1) lookX += step;
        else if (this.direction === 2) lookZ += step;
        else if (this.direction === 3) lookX -= step;

        let blocked = gridMap.has(`${lookX},${lookZ}`) || Math.abs(lookX) > GRID_SIZE || Math.abs(lookZ) > GRID_SIZE;

        if (blocked || Math.random() < 0.05) {
            let possible = [];
            // Check all 4 directions
            const dirs = [
                { id: 0, x: 0, z: -step }, // N
                { id: 1, x: step, z: 0 },  // E
                { id: 2, x: 0, z: step },  // S
                { id: 3, x: -step, z: 0 }  // W
            ];

            dirs.forEach(d => {
                // Don't turn 180
                if (Math.abs(this.direction - d.id) === 2) return;
                
                let k = `${this.lastGridPos.x + d.x},${this.lastGridPos.z + d.z}`;
                if (!gridMap.has(k) && Math.abs(this.lastGridPos.x + d.x) < GRID_SIZE && Math.abs(this.lastGridPos.z + d.z) < GRID_SIZE) {
                    possible.push(d.id);
                }
            });

            if (possible.length > 0) {
                this.nextDirection = possible[Math.floor(Math.random() * possible.length)];
                this.direction = this.nextDirection;
            }
        }
    }

    die() {
        if (!this.alive) return;
        this.alive = false;
        
        createExplosion(this.mesh.position, this.color);
        
        // Remove visuals immediately
        scene.remove(this.mesh);
        this.trailPoints.forEach(p => {
            scene.remove(p.mesh);
            gridMap.delete(`${p.x},${p.z}`); // Clean grid immediately
        });
        this.trailPoints = [];

        // Screen Shake
        screenShake = 1.0; 

        if (this.isPlayer) {
            // TRIGGER MASS EXTINCTION
            endGame();
        } else {
            // If enemy dies, just give score
            if (!isGameOver) {
                score += 100;
                checkLevelComplete();
            }
        }
        updateUI();
    }
}

// --- WORLD GENERATION ---
function createBoundary() {
    const geo = new THREE.BoxGeometry(GRID_SIZE * 2 + 2, 8, 2);
    const mat = new THREE.MeshBasicMaterial({ color: 0xff0055 });
    
    const w1 = new THREE.Mesh(geo, mat); w1.position.z = -GRID_SIZE - 1;
    const w2 = new THREE.Mesh(geo, mat); w2.position.z = GRID_SIZE + 1;
    const w3 = new THREE.Mesh(geo, mat); w3.rotation.y = Math.PI/2; w3.position.x = -GRID_SIZE - 1;
    const w4 = new THREE.Mesh(geo, mat); w4.rotation.y = Math.PI/2; w4.position.x = GRID_SIZE + 1;
    scene.add(w1, w2, w3, w4);
}

function createWall(x, z) {
    const geo = new THREE.BoxGeometry(CELL_SIZE * 3, 6, CELL_SIZE * 3);
    const mat = new THREE.MeshLambertMaterial({ color: COLORS.wall });
    const wall = new THREE.Mesh(geo, mat);
    wall.position.set(x, 3, z);
    scene.add(wall);
    walls.push(wall);
    
    // Mark grid
    for(let i=-1; i<=1; i++) {
        for(let j=-1; j<=1; j++) {
            gridMap.add(`${x + i*CELL_SIZE},${z + j*CELL_SIZE}`);
        }
    }
}

function createExplosion(pos, color) {
    const particleCount = 40;
    const geometry = new THREE.BufferGeometry();
    const positions = [];
    const velocities = [];

    for (let i = 0; i < particleCount; i++) {
        positions.push(pos.x, pos.y, pos.z);
        // Explosive velocity
        velocities.push(
            (Math.random() - 0.5) * 4,
            (Math.random() - 0.5) * 4,
            (Math.random() - 0.5) * 4
        );
    }
    
    geometry.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
    const material = new THREE.PointsMaterial({ color: color, size: 2.5, transparent: true });
    const pts = new THREE.Points(geometry, material);
    scene.add(pts);
    particles.push({ mesh: pts, vels: velocities, age: 0 });
}

// --- SYSTEM LOGIC ---

function handleInput(e) {
    if (isGameOver) {
        if (e.code === 'Enter') {
            isGameOver = false;
            level = 1;
            score = 0;
            uiGameOver.style.display = 'none';
            startLevel();
        }
        return;
    }

    const p = cycles[0];
    if (!p || !p.alive) return;

    if (e.code === 'ArrowUp' && p.direction !== 2) p.nextDirection = 0;
    if (e.code === 'ArrowRight' && p.direction !== 3) p.nextDirection = 1;
    if (e.code === 'ArrowDown' && p.direction !== 0) p.nextDirection = 2;
    if (e.code === 'ArrowLeft' && p.direction !== 1) p.nextDirection = 3;
    if (e.code === 'Space') p.speed = SPEED_BOOST;
}

function checkLevelComplete() {
    let enemiesAlive = cycles.filter(c => !c.isPlayer && c.alive).length;
    if (enemiesAlive === 0) {
        level++;
        score += 500;
        // Subtle shake for success
        screenShake = 0.5;
        setTimeout(startLevel, 2000); 
    }
}

function endGame() {
    isGameOver = true;
    uiGameOver.style.display = 'block';
    
    // KILL EVERYONE
    cycles.forEach(c => {
        if(c.alive && !c.isPlayer) {
            c.die(); // Chain reaction explosions
        }
    });
}

function updateUI() {
    uiLevel.innerText = level;
    uiScore.innerText = score;
    uiEnemies.innerText = cycles.filter(c => !c.isPlayer && c.alive).length;
}

function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
    composer.setSize(window.innerWidth, window.innerHeight);
}

function animate() {
    requestAnimationFrame(animate);

    // Camera Shake Decay
    if (screenShake > 0) {
        camera.position.x += (Math.random() - 0.5) * screenShake;
        camera.position.z += (Math.random() - 0.5) * screenShake;
        screenShake *= 0.9; // Fade out shake
    }

    // Particle Updates
    for(let i = particles.length - 1; i >= 0; i--) {
        let p = particles[i];
        p.age++;
        const pos = p.mesh.geometry.attributes.position.array;
        for(let j=0; j<pos.length; j+=3) {
            pos[j] += p.vels[j];
            pos[j+1] += p.vels[j+1];
            pos[j+2] += p.vels[j+2];
        }
        p.mesh.geometry.attributes.position.needsUpdate = true;
        p.mesh.material.opacity = 1 - (p.age / 50); // Fade out

        if(p.age > 50) {
            scene.remove(p.mesh);
            particles.splice(i, 1);
        }
    }

    if(!isGameOver) {
        cycles.forEach(c => c.update());
        
        // Smooth follow camera (Only if player exists)
        if (cycles[0] && cycles[0].alive) {
            const pPos = cycles[0].mesh.position;
            // Target Camera Position
            const targetX = pPos.x;
            const targetZ = pPos.z + 80;
            
            // Lerp
            camera.position.x += (targetX - camera.position.x) * 0.1;
            camera.position.z += (targetZ - camera.position.z) * 0.1;
            camera.lookAt(pPos.x, 0, pPos.z);
        }
    }

    composer.render();
}

init();

</script>
</body>
</html>
</textarea>

<textarea id="code-game2" style="display:none;">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>NEON WARFARE SAGA: POWER UP UPDATE</title>
    <style>
        body { margin: 0; overflow: hidden; background: #000; font-family: 'Segoe UI', sans-serif; user-select: none; }
        
        /* --- UI LAYERS --- */
        .full-screen { position: absolute; top: 0; left: 0; width: 100%; height: 100%; display: none; flex-direction: column; justify-content: center; align-items: center; }
        
        /* MENU SCREEN */
        #menu-screen { display: flex; background: linear-gradient(135deg, #050011 0%, #110022 100%); z-index: 50; }
        .logo { font-size: 80px; color: transparent; -webkit-text-stroke: 2px #00ffff; text-shadow: 0 0 40px #00ffff; font-style: italic; font-weight: 900; margin-bottom: 20px; text-align: center; }
        .subtitle { color: #ff00ff; font-size: 24px; letter-spacing: 10px; margin-bottom: 50px; text-shadow: 0 0 10px #ff00ff; }
        
        /* TANK HUD */
        #tank-hud { display: none; pointer-events: none; position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 10; }
        #score-box { position: absolute; top: 20px; left: 20px; font-size: 24px; color: #fff; text-shadow: 0 0 10px #fff; }
        #health-bar-container { position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%) skew(-20deg); width: 300px; height: 20px; border: 2px solid #ff0000; background: #220000; }
        #health-fill { width: 100%; height: 100%; background: #ff0000; transition: width 0.2s; }
        
        #powerup-text { 
            position: absolute; bottom: 80px; left: 50%; transform: translateX(-50%); 
            font-size: 24px; font-weight: bold; text-shadow: 0 0 10px currentColor; display: none;
        }

        #boss-hud { display: none; position: absolute; top: 20px; right: 20px; width: 300px; text-align: right; }
        #boss-name { color: #ffaa00; font-size: 20px; font-weight: 900; text-shadow: 0 0 10px #ffaa00; }
        #boss-bar-bg { width: 100%; height: 15px; background: #330000; border: 1px solid #ffaa00; margin-top: 5px; }
        #boss-bar-fill { width: 100%; height: 100%; background: #ffaa00; transition: width 0.1s; }

        /* TRON HUD */
        #tron-hud { display: none; pointer-events: none; position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 10; }
        .tron-title { position: absolute; top: 20px; width: 100%; text-align: center; color: #00ffff; font-size: 30px; letter-spacing: 5px; text-shadow: 0 0 20px #00ffff; }
        .tron-controls { position: absolute; bottom: 20px; width: 100%; text-align: center; color: #aaa; font-size: 18px; }

        /* END SCREENS */
        #game-over-screen { background: rgba(20, 0, 0, 0.95); z-index: 60; }
        #victory-screen { background: rgba(0, 20, 20, 0.95); z-index: 60; }
        
        /* BUTTONS */
        button {
            background: transparent; border: 3px solid #00ffff; color: #00ffff;
            padding: 20px 60px; font-size: 24px; font-weight: bold; cursor: pointer;
            text-transform: uppercase; transition: 0.2s; box-shadow: 0 0 15px #00ffff;
            font-family: inherit; margin-top: 20px;
        }
        button:hover { background: #00ffff; color: #000; box-shadow: 0 0 50px #00ffff; }
        button.restart { border-color: #ff0055; color: #ff0055; box-shadow: 0 0 15px #ff0055; }
        button.restart:hover { background: #ff0055; color: #fff; box-shadow: 0 0 50px #ff0055; }

        .dmg-flash { position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: radial-gradient(circle, transparent, red); opacity: 0; transition: opacity 0.1s; pointer-events: none; z-index: 5; }
    </style>
</head>
<body>

    <div id="menu-screen" class="full-screen">
        <div class="logo">NEON WARFARE</div>
        <div class="subtitle">SAGA EDITION</div>
        <button id="btn-start">INITIATE SYSTEM</button>
    </div>

    <div id="game-over-screen" class="full-screen">
        <h1 style="color: #ff0055; font-size: 60px; text-shadow: 0 0 30px red;">SYSTEM FAILURE</h1>
        <h2 id="death-reason" style="color: #fff;">KIA</h2>
        <button class="restart" onclick="location.reload()">REBOOT</button>
    </div>

    <div id="victory-screen" class="full-screen">
        <h1 style="color: #00ff00; font-size: 80px; text-shadow: 0 0 50px #00ff00;">VICTORY</h1>
        <h2 style="color: #fff;">SYSTEM CORE SECURED</h2>
        <button onclick="location.reload()">PLAY AGAIN</button>
    </div>

    <div id="tank-hud">
        <div id="score-box">KILLS: <span id="score">0</span></div>
        <div id="health-bar-container"><div id="health-fill"></div></div>
        <div id="powerup-text">TRIPLE SHOT ACTIVE</div>
        <div id="boss-hud">
            <div id="boss-name">TARGET DETECTED</div>
            <div id="boss-bar-bg"><div id="boss-bar-fill"></div></div>
        </div>
        <div class="dmg-flash" id="dmg-flash"></div>
    </div>

    <div id="tron-hud">
        <div class="tron-title">/// HYPER-CYCLE MODE ///</div>
        <div class="tron-controls">USE ARROW KEYS TO TURN</div>
    </div>

    <script type="module">
        import * as THREE from 'https://esm.sh/three@0.160.0';
        import { EffectComposer } from 'https://esm.sh/three@0.160.0/examples/jsm/postprocessing/EffectComposer.js?deps=three@0.160.0';
        import { RenderPass } from 'https://esm.sh/three@0.160.0/examples/jsm/postprocessing/RenderPass.js?deps=three@0.160.0';
        import { UnrealBloomPass } from 'https://esm.sh/three@0.160.0/examples/jsm/postprocessing/UnrealBloomPass.js?deps=three@0.160.0';

        // --- GLOBAL MANAGERS ---
        const Audio = {
            ctx: null,
            init: function() {
                const AC = window.AudioContext || window.webkitAudioContext;
                if(!this.ctx) this.ctx = new AC();
                if(this.ctx.state === 'suspended') this.ctx.resume();
            },
            play: function(freq, type, dur, vol=0.1) {
                if(!this.ctx) return;
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                osc.type = type;
                osc.frequency.setValueAtTime(freq, this.ctx.currentTime);
                gain.gain.setValueAtTime(vol, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + dur);
                osc.connect(gain); gain.connect(this.ctx.destination);
                osc.start(); osc.stop(this.ctx.currentTime + dur);
            }
        };

        const App = {
            mode: 'MENU',
            renderer: null,
            composer: null,
            
            init: function() {
                this.renderer = new THREE.WebGLRenderer({ antialias: false });
                this.renderer.setSize(window.innerWidth, window.innerHeight);
                document.body.appendChild(this.renderer.domElement);
                
                document.getElementById('menu-screen').style.display = 'flex';
                document.getElementById('btn-start').addEventListener('click', () => {
                    Audio.init();
                    this.startTankGame();
                });

                window.addEventListener('resize', () => this.onResize());
                this.loop();
            },

            startTankGame: function() {
                this.mode = 'TANK';
                document.getElementById('menu-screen').style.display = 'none';
                document.getElementById('tank-hud').style.display = 'block';
                TankGame.init();
            },

            startTronGame: function() {
                this.mode = 'TRON';
                document.getElementById('tank-hud').style.display = 'none';
                document.getElementById('tron-hud').style.display = 'block';
                TronGame.init();
            },

            gameOver: function(reason) {
                this.mode = 'OVER';
                document.getElementById('death-reason').innerText = reason;
                document.getElementById('game-over-screen').style.display = 'flex';
            },

            victory: function() {
                this.mode = 'WIN';
                document.getElementById('victory-screen').style.display = 'flex';
            },

            loop: function() {
                requestAnimationFrame(() => this.loop());
                if (this.mode === 'TANK') TankGame.update(this.renderer, this.composer);
                if (this.mode === 'TRON') TronGame.update(this.renderer);
            },

            onResize: function() {
                this.renderer.setSize(window.innerWidth, window.innerHeight);
                if(this.mode === 'TANK') TankGame.resize();
                if(this.mode === 'TRON') TronGame.resize();
            }
        };

        // ==========================================
        // === GAME 1: NEON WARFARE (TANK SHOOTER) ===
        // ==========================================
        const TankGame = {
            scene: null, camera: null, composer: null,
            state: { 
                active: false, level: 1, score: 0, health: 100, speed: 0.4, mouseX: 0, 
                bossActive: false, bossHP: 0, bossMaxHP: 0,
                tripleShot: false, shield: false
            },
            assets: { player: null, boss: null, enemies: [], pBullets: [], eBullets: [], particles: [], powerups: [] },
            
            init: function() {
                this.scene = new THREE.Scene();
                this.scene.fog = new THREE.FogExp2(0x110505, 0.02);
                this.camera = new THREE.PerspectiveCamera(70, window.innerWidth/window.innerHeight, 0.1, 1000);
                this.camera.position.set(0, 6, 12);
                this.camera.lookAt(0,0,-10);

                this.composer = new EffectComposer(App.renderer);
                this.composer.addPass(new RenderPass(this.scene, this.camera));
                const bloom = new UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 1.5, 0.4, 0.85);
                bloom.strength = 1.5; bloom.radius = 0.5;
                this.composer.addPass(bloom);

                const amb = new THREE.AmbientLight(0xffffff, 0.4);
                const dir = new THREE.DirectionalLight(0xffaa00, 1);
                dir.position.set(10, 20, 10);
                this.scene.add(amb, dir);

                const grid = new THREE.GridHelper(300, 60, 0xff0000, 0x330000);
                grid.position.y = -1; grid.scale.z = 5;
                this.scene.add(grid);
                this.grid = grid;

                const pGroup = new THREE.Group();
                const chassis = new THREE.Mesh(new THREE.BoxGeometry(1.5, 0.5, 2), new THREE.MeshPhongMaterial({color:0x00ff00}));
                const turret = new THREE.Mesh(new THREE.BoxGeometry(1, 0.6, 1), new THREE.MeshPhongMaterial({color:0x00aa00}));
                turret.position.y = 0.5;
                const barrel = new THREE.Mesh(new THREE.CylinderGeometry(0.1, 0.1, 1.5), new THREE.MeshPhongMaterial({color:0x222222}));
                barrel.rotation.x = Math.PI/2; barrel.position.set(0, 0.6, -1);
                pGroup.add(chassis, turret, barrel);
                this.scene.add(pGroup);
                this.assets.player = pGroup;

                document.addEventListener('mousemove', e => this.state.mouseX = (e.clientX/window.innerWidth)*2-1);
                const fire = () => { if(App.mode === 'TANK') this.shoot(); };
                window.addEventListener('mousedown', fire);
                window.addEventListener('keydown', e => { if(e.code==='Space') fire(); });

                this.state.active = true;
            },

            shoot: function() {
                Audio.play(400, 'square', 0.1);
                const spawnBullet = (offset) => {
                    const b = new THREE.Mesh(new THREE.BoxGeometry(0.2, 0.2, 2), new THREE.MeshBasicMaterial({color:0x00ff00}));
                    b.position.copy(this.assets.player.position);
                    b.position.x += offset;
                    b.position.y = 0.5;
                    this.scene.add(b);
                    this.assets.pBullets.push(b);
                };

                spawnBullet(0);
                if (this.state.tripleShot) {
                    spawnBullet(-1);
                    spawnBullet(1);
                }
            },

            spawnPowerup: function() {
                const rand = Math.random();
                let type, color, geo;
                
                if (rand < 0.4) {
                    type = 'health'; color = 0x00ff00; // Green Box
                    geo = new THREE.BoxGeometry(1, 1, 1);
                } else if (rand < 0.8) {
                    type = 'triple'; color = 0x00ffff; // Cyan Octahedron
                    geo = new THREE.OctahedronGeometry(0.8);
                } else {
                    type = 'shield'; color = 0xffff00; // Yellow Sphere
                    geo = new THREE.IcosahedronGeometry(0.8);
                }

                const mesh = new THREE.Mesh(geo, new THREE.MeshBasicMaterial({color: color, wireframe: true}));
                // Core
                const core = new THREE.Mesh(new THREE.BoxGeometry(0.4, 0.4, 0.4), new THREE.MeshBasicMaterial({color: 0xffffff}));
                mesh.add(core);

                mesh.position.set((Math.random()-0.5)*25, 1, -120);
                mesh.userData = { type: type, color: color };
                
                this.scene.add(mesh);
                this.assets.powerups.push(mesh);
            },

            activatePowerup: function(type, color) {
                const txt = document.getElementById('powerup-text');
                txt.style.display = 'block';
                txt.style.color = '#' + new THREE.Color(color).getHexString();
                Audio.play(600, 'sine', 0.2);

                if (type === 'health') {
                    this.state.health = Math.min(100, this.state.health + 30);
                    document.getElementById('health-fill').style.width = this.state.health + '%';
                    txt.innerText = "REPAIRED";
                    setTimeout(() => txt.style.display = 'none', 1000);
                } 
                else if (type === 'triple') {
                    this.state.tripleShot = true;
                    txt.innerText = "TRIPLE SHOT ACTIVE";
                    setTimeout(() => {
                        this.state.tripleShot = false;
                        if(txt.innerText.includes("TRIPLE")) txt.style.display = 'none';
                    }, 10000);
                }
                else if (type === 'shield') {
                    this.state.shield = true;
                    txt.innerText = "SHIELD ACTIVE";
                    this.assets.player.children.forEach(c => c.material.emissive = new THREE.Color(0xffff00));
                    setTimeout(() => {
                        this.state.shield = false;
                        this.assets.player.children.forEach(c => c.material.emissive = new THREE.Color(0x000000));
                        if(txt.innerText.includes("SHIELD")) txt.style.display = 'none';
                    }, 5000);
                }
            },

            spawnBoss: function() {
                this.state.bossActive = true;
                let hp, color, type;
                if (this.state.level === 1) { hp = 300; color = 0xff0000; type='HK-PHANTOM'; }
                else if (this.state.level === 2) { hp = 600; color = 0x00ff00; type='IRON-STRIDER'; }
                else { hp = 1000; color = 0x0000ff; type='OMEGA-CORE'; }

                this.state.bossMaxHP = hp;
                this.state.bossHP = hp;
                const boss = new THREE.Group();
                const body = new THREE.Mesh(new THREE.BoxGeometry(3, 2, 3), new THREE.MeshPhongMaterial({color:color}));
                boss.add(body);
                boss.position.set(0, 15, -150); 
                boss.userData = { type: type };
                this.scene.add(boss);
                this.assets.boss = boss;
                document.getElementById('boss-hud').style.display = 'block';
                document.getElementById('boss-name').innerText = type;
                document.getElementById('boss-bar-fill').style.width = '100%';
            },

            spawnEnemy: function() {
                const grp = new THREE.Group();
                const isTank = Math.random() > 0.5;
                const mat = new THREE.MeshPhongMaterial({color: 0xaa0000});

                if (isTank) {
                    // Tank Model
                    const chassis = new THREE.Mesh(new THREE.BoxGeometry(2.5, 1, 3), mat);
                    chassis.position.y = 0.5;
                    const turret = new THREE.Mesh(new THREE.BoxGeometry(1.5, 0.8, 2), mat);
                    turret.position.y = 1.4;
                    const barrel = new THREE.Mesh(new THREE.CylinderGeometry(0.2, 0.2, 2.5), mat);
                    barrel.rotation.x = Math.PI / 2;
                    barrel.position.set(0, 1.4, 1.5);
                    const treadL = new THREE.Mesh(new THREE.BoxGeometry(0.5, 1, 3), new THREE.MeshPhongMaterial({color: 0x550000}));
                    treadL.position.set(-1.5, 0.5, 0);
                    const treadR = new THREE.Mesh(new THREE.BoxGeometry(0.5, 1, 3), new THREE.MeshPhongMaterial({color: 0x550000}));
                    treadR.position.set(1.5, 0.5, 0);
                    grp.add(chassis, turret, barrel, treadL, treadR);
                    grp.userData = { hp: 3 + this.state.level, type: 'tank', shootTimer: Math.random() * 100 + 50 };
                } else {
                    // Soldier Model
                    const body = new THREE.Mesh(new THREE.BoxGeometry(0.6, 1, 0.4), mat);
                    body.position.y = 1;
                    const head = new THREE.Mesh(new THREE.SphereGeometry(0.3), mat);
                    head.position.y = 1.65;
                    const legL = new THREE.Mesh(new THREE.BoxGeometry(0.25, 1, 0.25), mat);
                    legL.position.set(-0.2, 0.5, 0);
                    const legR = new THREE.Mesh(new THREE.BoxGeometry(0.25, 1, 0.25), mat);
                    legR.position.set(0.2, 0.5, 0);
                    const armL = new THREE.Mesh(new THREE.BoxGeometry(0.2, 0.8, 0.2), mat);
                    armL.position.set(-0.4, 1.2, 0);
                    const armR = new THREE.Mesh(new THREE.BoxGeometry(0.2, 0.8, 0.2), mat);
                    armR.position.set(0.4, 1.2, 0);
                    const gun = new THREE.Mesh(new THREE.BoxGeometry(0.2, 0.2, 0.8), new THREE.MeshPhongMaterial({color: 0x555555}));
                    gun.position.set(0.4, 1.1, 0.4);
                    grp.add(body, head, legL, legR, armL, armR, gun);
                    grp.userData = { hp: 1 + this.state.level, type: 'soldier', shootTimer: Math.random() * 100 };
                }
                grp.position.set((Math.random()-0.5)*30, 0, -120);
                this.scene.add(grp);
                this.assets.enemies.push(grp);
            },

            shootEnemyBullet: function(enemy) {
                Audio.play(150, 'square', 0.1);
                const b = new THREE.Mesh(new THREE.SphereGeometry(0.3), new THREE.MeshBasicMaterial({color:0xff0000}));
                b.position.copy(enemy.position);
                b.position.y += 0.8; 
                b.position.z += 1;
                const dx = (this.assets.player.position.x - enemy.position.x) * 0.03;
                b.userData = { vel: new THREE.Vector3(dx, 0, 0.6) };
                this.scene.add(b);
                this.assets.eBullets.push(b);
            },

            update: function() {
                if(!this.state.active) return;

                // Player Move
                const targetX = this.state.mouseX * 15;
                this.assets.player.position.x += (targetX - this.assets.player.position.x) * 0.1;
                this.assets.player.rotation.y = -(this.assets.player.position.x - targetX) * 0.03;
                
                // Grid Move
                this.state.speed += 0.0001;
                this.grid.position.z += this.state.speed;
                if(this.grid.position.z > 0) this.grid.position.z = -50;

                // Spawning
                if(this.assets.boss) {
                    const b = this.assets.boss;
                    if(b.position.z < -40) { b.position.z += 0.5; b.position.y -= 0.1; }
                    else {
                        b.position.y = 4 + Math.sin(Date.now()*0.002)*2;
                        b.position.x += (this.assets.player.position.x - b.position.x) * 0.05;
                        if(Math.random() < 0.05) {
                            const bullet = new THREE.Mesh(new THREE.SphereGeometry(0.5), new THREE.MeshBasicMaterial({color:0xffaa00}));
                            bullet.position.copy(b.position);
                            const dir = new THREE.Vector3().subVectors(this.assets.player.position, b.position).normalize().multiplyScalar(0.8);
                            bullet.userData = { vel: dir };
                            this.scene.add(bullet);
                            this.assets.eBullets.push(bullet);
                            Audio.play(100, 'sawtooth', 0.2);
                        }
                    }
                } else {
                    if (this.state.score >= this.state.level * 10 && !this.state.bossActive) this.spawnBoss();
                    else if (!this.state.bossActive) {
                        if (Math.random() < 0.02) this.spawnEnemy();
                        if (Math.random() < 0.005) this.spawnPowerup();
                    }
                }

                // Player Bullets
                for(let i=this.assets.pBullets.length-1; i>=0; i--) {
                    const b = this.assets.pBullets[i];
                    b.position.z -= 2;
                    const bBox = new THREE.Box3().setFromObject(b);
                    const vBox = bBox.clone(); vBox.min.y = -100; vBox.max.y = 100;
                    let hit = false;

                    if(this.assets.boss) {
                        const bossBox = new THREE.Box3().setFromObject(this.assets.boss);
                        if(vBox.intersectsBox(bossBox)) {
                            this.createExplosion(b.position);
                            this.state.bossHP -= 10;
                            document.getElementById('boss-bar-fill').style.width = (this.state.bossHP/this.state.bossMaxHP*100)+'%';
                            hit = true;
                            if(this.state.bossHP <= 0) {
                                this.scene.remove(this.assets.boss);
                                this.assets.boss = null;
                                this.state.bossActive = false;
                                document.getElementById('boss-hud').style.display = 'none';
                                if(this.state.level === 3) { this.state.active = false; App.startTronGame(); return; }
                                else { this.state.level++; this.scene.fog.color.setHex(this.state.level===2?0x051105:0x050511); }
                            }
                        }
                    }

                    if(!hit) {
                        for(let j=this.assets.enemies.length-1; j>=0; j--) {
                            const e = this.assets.enemies[j];
                            if(bBox.intersectsBox(new THREE.Box3().setFromObject(e))) {
                                e.userData.hp--;
                                if(e.userData.hp <= 0) {
                                    this.createExplosion(e.position);
                                    this.scene.remove(e); this.assets.enemies.splice(j,1);
                                    this.state.score++;
                                    document.getElementById('score').innerText = this.state.score;
                                }
                                hit = true; break;
                            }
                        }
                    }
                    if(hit || b.position.z < -150) { this.scene.remove(b); this.assets.pBullets.splice(i,1); }
                }

                const pBox = new THREE.Box3().setFromObject(this.assets.player);
                pBox.min.y = -50; pBox.max.y = 50;

                // Enemies
                for(let i=this.assets.enemies.length-1; i>=0; i--) {
                    const e = this.assets.enemies[i];
                    e.position.z += this.state.speed;
                    if (e.position.z > -100 && e.position.z < 0) {
                        e.userData.shootTimer--;
                        if (e.userData.shootTimer <= 0) {
                            this.shootEnemyBullet(e);
                            e.userData.shootTimer = e.userData.type === 'tank' ? 120 : 80; 
                        }
                    }
                    if(pBox.intersectsBox(new THREE.Box3().setFromObject(e))) {
                        this.takeDamage(20);
                        this.scene.remove(e); this.assets.enemies.splice(i,1);
                    } else if(e.position.z > 10) {
                        this.scene.remove(e); this.assets.enemies.splice(i,1);
                    }
                }

                // Enemy Bullets
                for(let i=this.assets.eBullets.length-1; i>=0; i--) {
                    const b = this.assets.eBullets[i];
                    b.position.add(b.userData.vel);
                    if(pBox.containsPoint(b.position)) {
                        this.takeDamage(10);
                        this.scene.remove(b); this.assets.eBullets.splice(i,1);
                    } else if (b.position.z > 20 || b.position.y < -5) {
                        this.scene.remove(b); this.assets.eBullets.splice(i,1);
                    }
                }

                // Powerups
                for(let i=this.assets.powerups.length-1; i>=0; i--) {
                    const p = this.assets.powerups[i];
                    p.position.z += this.state.speed;
                    p.rotation.y += 0.05; p.rotation.z += 0.05;
                    if(pBox.intersectsBox(new THREE.Box3().setFromObject(p))) {
                        this.activatePowerup(p.userData.type, p.userData.color);
                        this.scene.remove(p); this.assets.powerups.splice(i,1);
                    } else if(p.position.z > 10) {
                        this.scene.remove(p); this.assets.powerups.splice(i,1);
                    }
                }

                // Particles
                for(let i=this.assets.particles.length-1; i>=0; i--) {
                    const p = this.assets.particles[i];
                    p.position.add(p.userData.vel);
                    p.scale.multiplyScalar(0.9);
                    if(p.scale.x < 0.05) { this.scene.remove(p); this.assets.particles.splice(i,1); }
                }

                this.composer.render();
            },

            createExplosion: function(pos) {
                Audio.play(200, 'square', 0.1);
                for(let i=0; i<8; i++) {
                    const p = new THREE.Mesh(new THREE.BoxGeometry(0.3,0.3,0.3), new THREE.MeshBasicMaterial({color:0xffaa00}));
                    p.position.copy(pos);
                    p.userData = { vel: new THREE.Vector3(Math.random()-0.5, Math.random(), Math.random()-0.5) };
                    this.scene.add(p);
                    this.assets.particles.push(p);
                }
            },

            takeDamage: function(amt) {
                if (this.state.shield) return; // Invincible
                this.state.health -= amt;
                document.getElementById('health-fill').style.width = this.state.health + '%';
                const flash = document.getElementById('dmg-flash');
                flash.style.opacity = 1;
                setTimeout(() => flash.style.opacity = 0, 100);
                if(this.state.health <= 0) App.gameOver("TANK DESTROYED");
            },

            resize: function() {
                this.camera.aspect = window.innerWidth/window.innerHeight;
                this.camera.updateProjectionMatrix();
                this.composer.setSize(window.innerWidth, window.innerHeight);
            }
        };

        // ==========================================
        // === GAME 2: NEON TRON (LIGHT CYCLE) ===
        // ==========================================
        const TronGame = {
            scene: null, camera: null, composer: null,
            gridSize: 40, cellSize: 2,
            cycles: [], lastTime: 0, tickRate: 80,
            walls: new Set(),

            init: function() {
                this.scene = new THREE.Scene();
                this.scene.background = new THREE.Color(0x001111);
                this.camera = new THREE.PerspectiveCamera(60, window.innerWidth/window.innerHeight, 0.1, 1000);
                this.camera.position.set(0, 50, 60);
                this.camera.lookAt(0, 0, 0);

                this.composer = new EffectComposer(App.renderer);
                this.composer.addPass(new RenderPass(this.scene, this.camera));
                const bloom = new UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 1.5, 0.4, 0.85);
                bloom.strength = 2.0; bloom.radius = 0.8;
                this.composer.addPass(bloom);

                const gridHelper = new THREE.GridHelper(this.gridSize * this.cellSize, this.gridSize, 0x00ffff, 0x003333);
                this.scene.add(gridHelper);
                const plane = new THREE.Mesh(new THREE.PlaneGeometry(200, 200), new THREE.MeshBasicMaterial({color:0x000000}));
                plane.rotation.x = -Math.PI/2; plane.position.y = -0.1;
                this.scene.add(plane);

                this.walls.clear();
                this.cycles = [
                    this.createCycle(0x00ffff, 0, 10, 0, 1, true),
                    this.createCycle(0xff0055, 0, -10, 0, -1, false)
                ];

                window.addEventListener('keydown', e => {
                    if(App.mode !== 'TRON') return;
                    const p = this.cycles[0];
                    if(e.key === 'ArrowUp' && p.dz !== 1) { p.nextDx = 0; p.nextDz = -1; }
                    if(e.key === 'ArrowDown' && p.dz !== -1) { p.nextDx = 0; p.nextDz = 1; }
                    if(e.key === 'ArrowLeft' && p.dx !== 1) { p.nextDx = -1; p.nextDz = 0; }
                    if(e.key === 'ArrowRight' && p.dx !== -1) { p.nextDx = 1; p.nextDz = 0; }
                });
            },

            createCycle: function(color, x, z, dx, dz, isPlayer) {
                const mesh = new THREE.Mesh(new THREE.BoxGeometry(1.8, 1, 1.8), new THREE.MeshBasicMaterial({color: color}));
                mesh.position.set(x * this.cellSize, 0.5, z * this.cellSize);
                this.scene.add(mesh);
                return {
                    mesh: mesh, color: color, x: x, z: z, dx: dx, dz: dz, nextDx: dx, nextDz: dz,
                    isPlayer: isPlayer, alive: true
                };
            },

            update: function(renderer) {
                const now = Date.now();
                if (now - this.lastTime > this.tickRate) {
                    this.lastTime = now;
                    this.tick();
                }
                this.composer.render();
            },

            tick: function() {
                this.cycles.forEach(c => {
                    if(!c.alive) return;
                    if(!c.isPlayer) this.aiMove(c);
                    c.dx = c.nextDx; c.dz = c.nextDz;
                    this.addWall(c.x, c.z, c.color);
                    c.x += c.dx; c.z += c.dz;
                    c.mesh.position.x = c.x * this.cellSize;
                    c.mesh.position.z = c.z * this.cellSize;

                    if (this.checkCollision(c.x, c.z)) {
                        c.alive = false;
                        this.scene.remove(c.mesh);
                        this.createExplosion(c.mesh.position, c.color);
                        Audio.play(100, 'sawtooth', 0.5);
                        if (c.isPlayer) App.gameOver("DERESOLED");
                        else App.victory();
                    }
                });
            },

            addWall: function(x, z, color) {
                const key = `${x},${z}`;
                this.walls.add(key);
                const wall = new THREE.Mesh(new THREE.BoxGeometry(1.8, 1, 1.8), new THREE.MeshBasicMaterial({color: color}));
                wall.position.set(x * this.cellSize, 0.5, z * this.cellSize);
                this.scene.add(wall);
            },

            checkCollision: function(x, z) {
                const limit = this.gridSize / 2;
                if (x < -limit || x > limit || z < -limit || z > limit) return true;
                if (this.walls.has(`${x},${z}`)) return true;
                return false;
            },

            aiMove: function(c) {
                const nextX = c.x + c.dx;
                const nextZ = c.z + c.dz;
                if (this.checkCollision(nextX, nextZ) || Math.random() < 0.05) {
                    const dirs = [{dx: 0, dz: 1}, {dx: 0, dz: -1}, {dx: 1, dz: 0}, {dx: -1, dz: 0}];
                    const valid = dirs.filter(d => !(d.dx === -c.dx && d.dz === -c.dz));
                    const safe = valid.filter(d => !this.checkCollision(c.x + d.dx, c.z + d.dz));
                    if(safe.length > 0) {
                        const move = safe[Math.floor(Math.random() * safe.length)];
                        c.nextDx = move.dx; c.nextDz = move.dz;
                    }
                }
            },

            createExplosion: function(pos, color) {
                for(let i=0; i<20; i++) {
                    const p = new THREE.Mesh(new THREE.BoxGeometry(0.5,0.5,0.5), new THREE.MeshBasicMaterial({color:color}));
                    p.position.copy(pos);
                    p.position.x += (Math.random()-0.5)*2;
                    p.position.z += (Math.random()-0.5)*2;
                    this.scene.add(p);
                }
            },

            resize: function() {
                this.camera.aspect = window.innerWidth/window.innerHeight;
                this.camera.updateProjectionMatrix();
                this.composer.setSize(window.innerWidth, window.innerHeight);
            }
        };

        App.init();
    </script>
</body>
</html>
</textarea>

<textarea id="code-game3" style="display:none;">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>NEON VOID: OVERDRIVE</title>
    <style>
        body { margin: 0; overflow: hidden; background: #000; font-family: 'Courier New', monospace; user-select: none; }
        
        /* HUD Styles */
        #ui-layer { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 10; }
        
        .hud-text {
            position: absolute; color: #fff; text-shadow: 0 0 10px #fff, 0 0 20px #ff00de;
            font-weight: bold; letter-spacing: 2px;
        }
        
        #score-display { top: 20px; left: 20px; font-size: 24px; }
        #highscore-display { top: 20px; right: 20px; font-size: 18px; color: #ffd700; text-shadow: 0 0 10px #ffd700; }
        
        #overlay {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85); display: flex; flex-direction: column;
            justify-content: center; align-items: center; z-index: 20; pointer-events: auto;
        }
        
        h1 {
            font-size: 80px; color: transparent; -webkit-text-stroke: 2px #00ffff;
            text-shadow: 0 0 30px #00ffff; margin: 0; font-style: italic; text-transform: uppercase;
        }
        
        h2 { color: #ff00de; text-shadow: 0 0 15px #ff00de; margin-bottom: 40px; font-size: 24px; }
        
        button {
            background: transparent; border: 2px solid #00ffff; color: #00ffff;
            padding: 15px 50px; font-size: 24px; font-family: inherit; cursor: pointer;
            text-transform: uppercase; transition: 0.2s;
            box-shadow: 0 0 15px #00ffff;
        }
        button:hover { background: #00ffff; color: #000; box-shadow: 0 0 40px #00ffff; }
        
        #controls-hint { position: absolute; bottom: 20px; color: #666; font-size: 14px; }
    </style>

    <script type="importmap">
        {
            "imports": {
                "three": "https://unpkg.com/three@0.160.0/build/three.module.js",
                "three/addons/": "https://unpkg.com/three@0.160.0/examples/jsm/"
            }
        }
    </script>
</head>
<body>

    <div id="ui-layer">
        <div id="score-display">SCORE: <span id="score">0</span></div>
        <div id="highscore-display">BEST: <span id="highscore">0</span></div>
    </div>

    <div id="overlay">
        <h1>Neon Void</h1>
        <h2>OVERDRIVE</h2>
        <button id="start-btn">INITIALIZE</button>
        <div id="controls-hint">MOUSE / TOUCH TO STEER</div>
    </div>

    <script type="module">
        import * as THREE from 'three';
        import { EffectComposer } from 'three/addons/postprocessing/EffectComposer.js';
        import { RenderPass } from 'three/addons/postprocessing/RenderPass.js';
        import { UnrealBloomPass } from 'three/addons/postprocessing/UnrealBloomPass.js';

        // --- AUDIO ENGINE (Procedural Sound) ---
        // We create sound using math (Oscillators) so no external files are needed.
        const Audio = {
            ctx: null,
            masterGain: null,
            
            init: function() {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                this.ctx = new AudioContext();
                this.masterGain = this.ctx.createGain();
                this.masterGain.gain.value = 0.3; // Master volume
                this.masterGain.connect(this.ctx.destination);
            },

            playTone: function(freq, type, duration) {
                if (!this.ctx) return;
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                osc.type = type;
                osc.frequency.setValueAtTime(freq, this.ctx.currentTime);
                
                gain.gain.setValueAtTime(0.1, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, this.ctx.currentTime + duration);
                
                osc.connect(gain);
                gain.connect(this.masterGain);
                osc.start();
                osc.stop(this.ctx.currentTime + duration);
            },

            playCollect: function() {
                this.playTone(880, 'sine', 0.1);
                setTimeout(() => this.playTone(1760, 'square', 0.2), 50);
            },

            playCrash: function() {
                if (!this.ctx) return;
                // White noise burst
                const bufferSize = this.ctx.sampleRate * 0.5; // 0.5 seconds
                const buffer = this.ctx.createBuffer(1, bufferSize, this.ctx.sampleRate);
                const data = buffer.getChannelData(0);
                for (let i = 0; i < bufferSize; i++) data[i] = Math.random() * 2 - 1;

                const noise = this.ctx.createBufferSource();
                noise.buffer = buffer;
                const gain = this.ctx.createGain();
                gain.gain.setValueAtTime(0.5, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, this.ctx.currentTime + 0.5);
                noise.connect(gain);
                gain.connect(this.masterGain);
                noise.start();
            },

            startEngine: function() {
                if (!this.ctx) return;
                // Low drone
                this.engineOsc = this.ctx.createOscillator();
                this.engineOsc.type = 'sawtooth';
                this.engineOsc.frequency.value = 100;
                this.engineGain = this.ctx.createGain();
                this.engineGain.gain.value = 0.05;
                this.engineOsc.connect(this.engineGain);
                this.engineGain.connect(this.masterGain);
                this.engineOsc.start();
            },

            updateEngine: function(speedNormalized) {
                if (this.engineOsc) {
                    // Pitch up engine as game gets faster
                    this.engineOsc.frequency.value = 60 + (speedNormalized * 100);
                }
            }
        };

        // --- SCENE SETUP ---
        const scene = new THREE.Scene();
        scene.fog = new THREE.FogExp2(0x000000, 0.03); // Black fog

        const camera = new THREE.PerspectiveCamera(70, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 3, 8);
        camera.lookAt(0, 0, -10);

        const renderer = new THREE.WebGLRenderer({ antialias: false }); // False because Bloom handles AA feeling
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)); // Performance optimization
        renderer.toneMapping = THREE.ReinhardToneMapping;
        document.body.appendChild(renderer.domElement);

        // --- POST PROCESSING (THE GLOW) ---
        const renderScene = new RenderPass(scene, camera);
        const bloomPass = new UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 1.5, 0.4, 0.85);
        bloomPass.threshold = 0;
        bloomPass.strength = 2.0; // Intense glow
        bloomPass.radius = 0.5;

        const composer = new EffectComposer(renderer);
        composer.addPass(renderScene);
        composer.addPass(bloomPass);

        // --- OBJECTS ---
        
        // 1. The Grid (Retrowave Floor)
        const gridHelper = new THREE.GridHelper(200, 100, 0xff00de, 0x220044);
        gridHelper.position.y = -1;
        gridHelper.position.z = -50;
        // Stretch it to look endless
        gridHelper.scale.z = 5; 
        scene.add(gridHelper);

        const movingGrid = new THREE.GridHelper(200, 20, 0x00ffff, 0x00ffff);
        movingGrid.position.y = -1;
        movingGrid.scale.z = 2;
        scene.add(movingGrid);

        // 2. The Ship (Built from primitives)
        const shipGroup = new THREE.Group();
        
        // Main body
        const bodyGeo = new THREE.ConeGeometry(0.5, 2, 4);
        const bodyMat = new THREE.MeshBasicMaterial({ color: 0x000000 }); // Black body
        const body = new THREE.Mesh(bodyGeo, bodyMat);
        body.rotation.x = Math.PI / 2;
        body.rotation.y = Math.PI / 4;
        
        // Glowing edges (Wireframe)
        const wireGeo = new THREE.EdgesGeometry(bodyGeo);
        const wireMat = new THREE.LineBasicMaterial({ color: 0x00ffff });
        const wire = new THREE.LineSegments(wireGeo, wireMat);
        wire.rotation.copy(body.rotation);
        
        // Engine glow
        const engineGeo = new THREE.BoxGeometry(0.2, 0.2, 0.2);
        const engineMat = new THREE.MeshBasicMaterial({ color: 0x00ffff });
        const engine = new THREE.Mesh(engineGeo, engineMat);
        engine.position.z = 1;

        shipGroup.add(body);
        shipGroup.add(wire);
        shipGroup.add(engine);
        scene.add(shipGroup);

        // 3. Warp Stars (Speed effect)
        const starGeo = new THREE.BufferGeometry();
        const starCount = 500;
        const starPos = new Float32Array(starCount * 3);
        for(let i=0; i<starCount * 3; i++) {
            starPos[i] = (Math.random() - 0.5) * 100;
        }
        starGeo.setAttribute('position', new THREE.BufferAttribute(starPos, 3));
        const starMat = new THREE.PointsMaterial({ color: 0xffffff, size: 0.2 });
        const stars = new THREE.Points(starGeo, starMat);
        scene.add(stars);

        // --- GAME LOGIC ---
        let gameRunning = false;
        let speed = 0;
        let baseSpeed = 0.5;
        let score = 0;
        let highscore = localStorage.getItem('neon_highscore') || 0;
        let time = 0;
        
        // Object Pools
        const obstacles = [];
        const coins = [];
        const particles = [];

        document.getElementById('highscore').innerText = highscore;

        // Input
        let mouseX = 0;
        const handleInput = (x) => {
            mouseX = (x / window.innerWidth) * 2 - 1;
        };
        document.addEventListener('mousemove', (e) => handleInput(e.clientX));
        document.addEventListener('touchmove', (e) => handleInput(e.touches[0].clientX), {passive: false});

        document.getElementById('start-btn').addEventListener('click', () => {
            document.getElementById('overlay').style.display = 'none';
            Audio.init();
            Audio.startEngine();
            resetGame();
        });

        function spawnObstacle() {
            const geo = new THREE.BoxGeometry(1, 5, 1);
            const mat = new THREE.MeshBasicMaterial({ color: 0xff00de }); // Pink
            const obs = new THREE.Mesh(geo, mat);
            
            // Glowing edges
            const edges = new THREE.LineSegments(
                new THREE.EdgesGeometry(geo),
                new THREE.LineBasicMaterial({ color: 0xffffff })
            );
            obs.add(edges);

            obs.position.set((Math.random() - 0.5) * 20, 0, -100);
            scene.add(obs);
            obstacles.push(obs);
        }

        function spawnCoin() {
            const geo = new THREE.OctahedronGeometry(0.5);
            const mat = new THREE.MeshBasicMaterial({ color: 0xffd700 }); // Gold
            const coin = new THREE.Mesh(geo, mat);
            coin.position.set((Math.random() - 0.5) * 20, 0.5, -100);
            scene.add(coin);
            coins.push(coin);
        }

        function createExplosion(pos, color) {
            for(let i=0; i<20; i++) {
                const geo = new THREE.BoxGeometry(0.2, 0.2, 0.2);
                const mat = new THREE.MeshBasicMaterial({ color: color });
                const p = new THREE.Mesh(geo, mat);
                p.position.copy(pos);
                p.userData.vel = new THREE.Vector3(
                    (Math.random()-0.5), (Math.random()-0.5), (Math.random()-0.5)
                ).normalize().multiplyScalar(0.5);
                scene.add(p);
                particles.push(p);
            }
        }

        function resetGame() {
            gameRunning = true;
            speed = baseSpeed;
            score = 0;
            document.getElementById('score').innerText = score;
            
            // Clear scene items
            obstacles.forEach(o => scene.remove(o));
            coins.forEach(c => scene.remove(c));
            obstacles.length = 0;
            coins.length = 0;

            shipGroup.position.set(0, 0, 0);
            shipGroup.visible = true;
            shipGroup.rotation.z = 0;
        }

        function gameOver() {
            gameRunning = false;
            Audio.playCrash();
            shipGroup.visible = false;
            createExplosion(shipGroup.position, 0x00ffff);
            
            if (score > highscore) {
                highscore = score;
                localStorage.setItem('neon_highscore', highscore);
                document.getElementById('highscore').innerText = highscore;
            }

            setTimeout(() => {
                document.getElementById('overlay').style.display = 'flex';
                document.querySelector('#overlay h2').innerText = "SYSTEM CRASHED";
                document.querySelector('#start-btn').innerText = "REBOOT";
            }, 1500);
        }

        // --- ANIMATION LOOP ---
        function animate() {
            requestAnimationFrame(animate);
            time += 0.01;

            // 1. Dynamic World Colors
            const hue = (time * 0.1) % 1;
            const color = new THREE.Color().setHSL(hue, 0.5, 0.1); // Dark BG cycling
            scene.fog.color.lerp(color, 0.05);
            // gridHelper.material.color.setHSL(hue, 1, 0.5);

            if (gameRunning) {
                // Increase speed slowly
                speed += 0.0001;
                Audio.updateEngine(speed - baseSpeed); // Update sound pitch

                // Ship Movement
                const targetX = mouseX * 8;
                shipGroup.position.x += (targetX - shipGroup.position.x) * 0.1;
                // Banking
                shipGroup.rotation.z = -(shipGroup.position.x - targetX) * 0.15;
                // Engine wobble
                shipGroup.position.y = Math.sin(time * 20) * 0.05;

                // Move Floor Grid (Parallax illusion)
                movingGrid.position.z += speed;
                if(movingGrid.position.z > 10) movingGrid.position.z = -10;

                // Move Stars
                const positions = stars.geometry.attributes.position.array;
                for(let i=2; i<positions.length; i+=3) {
                    positions[i] += speed * 10;
                    if(positions[i] > 10) positions[i] = -100;
                }
                stars.geometry.attributes.position.needsUpdate = true;

                // Spawn Logic
                if (Math.random() < 0.03) spawnObstacle();
                if (Math.random() < 0.01) spawnCoin();

                // Update Obstacles
                const shipBox = new THREE.Box3().setFromObject(shipGroup);
                shipBox.expandByScalar(-0.3); // Forgiving hitbox

                for (let i = obstacles.length - 1; i >= 0; i--) {
                    let o = obstacles[i];
                    o.position.z += speed;
                    
                    if (shipBox.intersectsBox(new THREE.Box3().setFromObject(o))) {
                        gameOver();
                    }

                    if (o.position.z > 5) {
                        scene.remove(o);
                        obstacles.splice(i, 1);
                        score += 10;
                        document.getElementById('score').innerText = score;
                    }
                }

                // Update Coins
                for (let i = coins.length - 1; i >= 0; i--) {
                    let c = coins[i];
                    c.position.z += speed;
                    c.rotation.x += 0.05;
                    c.rotation.y += 0.05;

                    if (shipBox.intersectsBox(new THREE.Box3().setFromObject(c))) {
                        scene.remove(c);
                        coins.splice(i, 1);
                        score += 50;
                        Audio.playCollect();
                        document.getElementById('score').innerText = score;
                        // Visual feedback
                        createExplosion(c.position, 0xffd700);
                    } else if (c.position.z > 5) {
                        scene.remove(c);
                        coins.splice(i, 1);
                    }
                }
            }

            // Update Particles (Explosions) always
            for(let i=particles.length-1; i>=0; i--) {
                let p = particles[i];
                p.position.add(p.userData.vel);
                p.rotation.x += 0.1;
                p.scale.multiplyScalar(0.9);
                if(p.scale.x < 0.01) {
                    scene.remove(p);
                    particles.splice(i, 1);
                }
            }

            // Render with Bloom
            composer.render();
        }

        // Handle Window Resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
            composer.setSize(window.innerWidth, window.innerHeight);
        });

        animate();
    </script>
</body>
</html>
</textarea>

    <script>
        function loadGame(gameId) {
            // 1. Hide the menu
            document.getElementById('menu-container').style.opacity = '0';
            setTimeout(() => {
                document.getElementById('menu-container').style.display = 'none';
                
                // 2. Get the game code
                const code = document.getElementById('code-' + gameId).value;
                
                // 3. Inject into iframe
                const frame = document.getElementById('game-frame');
                const wrapper = document.getElementById('game-wrapper');
                
                wrapper.style.display = 'block';
                
                // Using srcdoc to render the full HTML document inside the iframe
                frame.srcdoc = code;
            }, 500);
        }

        function closeGame() {
            // 1. Clear iframe (stop game music/logic)
            document.getElementById('game-frame').srcdoc = '';
            document.getElementById('game-wrapper').style.display = 'none';

            // 2. Show menu
            const menu = document.getElementById('menu-container');
            menu.style.display = 'block';
            
            // Short delay to allow display:block to apply before opacity fade-in
            setTimeout(() => {
                menu.style.opacity = '1';
            }, 50);
        }
    </script>
</body>
</html>
