# AAlexandriAI
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AlexandriAI - Revolución de Inteligencia Futura</title>
    <style>
        :root {
            --neon-blue: #00f3ff;
            --matrix-green: #00ff5f;
            --cyber-purple: #bc13fe;
        }

        body {
            background: #0a0a0f;
            color: white;
            font-family: monospace;
            overflow-x: hidden;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(12px);
            border: 1px solid var(--neon-blue);
            box-shadow: 0 0 15px var(--neon-blue);
            border-radius: 15px;
            padding: 20px;
            margin: 15px;
        }

        #nav-container {
            display: grid;
            grid-template-columns: repeat(5, auto);
            gap: 10px;
            position: fixed;
            top: 20px;
            right: 20px;
        }

        .nav-atom {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--cyber-purple);
            cursor: pointer;
            transition: transform 0.3s;
        }

        #ai-chat {
            max-width: 800px;
            margin: 100px auto;
            height: 60vh;
            overflow-y: auto;
        }

        .message {
            padding: 10px;
            margin: 10px;
            border-radius: 10px;
            max-width: 70%;
        }

        #lineup-builder {
            display: grid;
            grid-template-columns: 1fr 3fr;
            gap: 20px;
        }

        .player-drag {
            cursor: grab;
            padding: 10px;
            margin: 5px;
            background: rgba(0, 255, 95, 0.1);
            border: 1px dashed var(--matrix-green);
        }

        #ig-float {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: linear-gradient(45deg, #405de6, #833ab4);
            padding: 15px;
            border-radius: 25px;
            animation: glow 2s infinite;
        }

        @keyframes glow {
            0% { box-shadow: 0 0 5px #833ab4; }
            50% { box-shadow: 0 0 20px #405de6; }
            100% { box-shadow: 0 0 5px #833ab4; }
        }
    </style>
</head>
<body>
    <nav id="nav-container">
        <div class="nav-atom" onclick="showSection('chat')"></div>
        <div class="nav-atom" onclick="showSection('futbol')"></div>
        <div class="nav-atom" onclick="showSection('art')"></div>
        <div class="nav-atom" onclick="changeLanguage()"></div>
        <div class="nav-atom" onclick="toggleTheme()"></div>
    </nav>

    <div id="ai-chat" class="glass-panel">
        <div id="chat-messages"></div>
        <input type="text" id="user-input" placeholder="Pregunta cualquier cosa...">
        <button onclick="sendMessage()">🚀</button>
    </div>

    <div id="futbol-section" class="glass-panel" style="display:none;">
        <h2>⚽ Football Genius</h2>
        <div id="lineup-builder">
            <div id="players-list">
                <div class="player-drag" draggable="true">Messi</div>
                <div class="player-drag" draggable="true">CR7</div>
            </div>
            <div id="field" class="glass-panel" style="height:500px;"></div>
        </div>
        <button onclick="analyzeTactics()">🔍 Analizar con AlexandriAI</button>
    </div>

    <footer style="text-align: center; padding: 30px;">
        <p>Creado por Alexander | 
            <a href="https://instagram.com/7alex.07" id="ig-float" target="_blank">
                Instagram @7alex.07
            </a>
        </p>
    </footer>

    <script>
        function showSection(sectionId) {
            document.querySelectorAll('.glass-panel').forEach(panel => {
                panel.style.display = 'none';
            });
            document.getElementById(`${sectionId}-section`).style.display = 'block';
        }

        function sendMessage() {
            const input = document.getElementById('user-input');
            const chat = document.getElementById('chat-messages');
            
            chat.innerHTML += `<div class="message" style="background: #1a1a2e; margin-left:30%">${input.value}</div>`;
            
            setTimeout(() => {
                chat.innerHTML += `<div class="message" style="background: #0f3460;">${simulateAIResponse(input.value)}</div>`;
                chat.scrollTop = chat.scrollHeight;
            }, 1000);
            
            input.value = '';
        }

        function simulateAIResponse(query) {
            const responses = {
                fútbol: "🔮 Predicción: 3-1 a favor del equipo local con un 78% de posesión",
                arte: "🎨 Generando imagen: 'Futuro cyberpunk en Jakarta 3023'...",
                técnica: "📊 Análisis completado: Rendimiento óptimo con un 92% de eficiencia"
            };
            return responses[query.toLowerCase()] || "✅ Procesado con éxito por AlexandriAI v3.1";
        }

        document.querySelectorAll('.player-drag').forEach(player => {
            player.addEventListener('dragstart', e => {
                e.dataTransfer.setData('text/plain', e.target.textContent);
            });
        });

        document.getElementById('field').addEventListener('dragover', e => {
            e.preventDefault();
            e.target.style.backgroundColor = 'rgba(0, 255, 95, 0.2)';
        });

        document.getElementById('field').addEventListener('dragleave', e => {
            e.target.style.backgroundColor = '';
        });

        document.getElementById('field').addEventListener('drop', e => {
            e.preventDefault();
            const playerName = e.dataTransfer.getData('text/plain');
            const newPlayer = document.createElement('div');
            newPlayer.className = 'player-drag';
            newPlayer.textContent = playerName;
            e.target.appendChild(newPlayer);
            e.target.style.backgroundColor = '';
        });
    </script>
</body>
</html>
