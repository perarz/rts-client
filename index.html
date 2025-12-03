<!DOCTYPE html>
<html lang="pl">
<head>
    <meta http-equiv="Content-Security-Policy"
      content="connect-src 'self' ws://localhost:3001 wss://rts-server-zt9x.onrender.com;">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RTS Multiplayer v0.8 BETA - 4 Graczy</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            overflow: hidden;
            font-family: Arial, sans-serif;
        }
        #gameCanvas {
            display: block;
            background: linear-gradient(135deg, #1a5f3e 0%, #2d7a52 100%);
            cursor: crosshair;
        }
        .ui-panel {
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(10px);
        }
        .btn-produce {
            transition: all 0.2s;
        }
        .btn-produce:hover:not(:disabled) {
            transform: scale(1.05);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
        }
        .btn-produce:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        #joinModal {
            background: rgba(0, 0, 0, 0.9);
        }
        .team-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 6px;
        }
        .waiting-overlay {
            background: rgba(0, 0, 0, 0.7);
        }
        .version-badge {
            position: fixed;
            bottom: 10px;
            right: 10px;
            background: rgba(0, 0, 0, 0.7);
            color: #fbbf24;
            padding: 8px 16px;
            border-radius: 8px;
            font-size: 14px;
            font-weight: bold;
            z-index: 100;
            backdrop-filter: blur(5px);
        }
    </style>
</head>
<body class="bg-gray-900">
    <!-- Version Badge -->
    <div class="version-badge">v0.8 BETA</div>

    <!-- Modal dołączania -->
    <div id="joinModal" class="fixed inset-0 flex items-center justify-center z-50">
        <div class="bg-gray-800 p-8 rounded-lg shadow-2xl max-w-md w-full">
            <h1 class="text-3xl font-bold text-white mb-6 text-center">🎮 RTS Multiplayer</h1>
            <p class="text-gray-300 mb-4 text-center">Gra 1v1v1v1 - Maksymalnie 4 graczy</p>
            
            <input 
                type="text" 
                id="playerName" 
                placeholder="Twoja nazwa (opcjonalnie)" 
                maxlength="20"
                class="w-full px-4 py-3 bg-gray-700 text-white rounded-lg mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
            
            <input 
                type="text" 
                id="serverUrl" 
                placeholder="ws://localhost:3001" 
                value="ws://localhost:3001"
                class="w-full px-4 py-3 bg-gray-700 text-white rounded-lg mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
            
            <button 
                id="joinButton" 
                class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg transition"
            >
                Dołącz do gry 🚀
            </button>
            
            <div id="joinStatus" class="mt-4 text-center text-sm"></div>
        </div>
    </div>

    <!-- Waiting overlay -->
    <div id="waitingOverlay" class="hidden fixed inset-0 flex items-center justify-center z-40 waiting-overlay">
        <div class="bg-gray-800 p-8 rounded-lg shadow-2xl text-center">
            <h2 class="text-3xl font-bold text-white mb-4">⏳ Czekam na graczy...</h2>
            <p class="text-gray-300 mb-4">Gra rozpocznie się gdy dołączy minimum 2 graczy</p>
            <div class="animate-pulse text-6xl">👥</div>
            <p class="text-gray-400 mt-4 text-sm" id="playerCountText">Gracze: 1/4</p>
        </div>
    </div>

    <!-- UI Gry -->
    <div id="gameUI" class="hidden">
        <div class="fixed top-0 left-0 right-0 ui-panel text-white p-4 z-10">
            <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-4">
                <div class="flex items-center gap-6">
                    <div class="text-xl font-bold">
                        <span class="team-indicator" id="myTeamColor"></span>
                        <span id="myPlayerName">Gracz</span>
                    </div>
                    <div class="text-2xl font-bold">
                        💰 <span id="goldDisplay">500</span>
                    </div>
                    <div class="text-sm opacity-75">
                        👷 <span id="workerCount">1</span>/25 | 
                        ⚔️ <span id="knightCount">0</span> |
                        👑 <span id="championCount">0</span>
                    </div>
                </div>
                <div class="flex gap-2 flex-wrap">
                    <button id="deselectAll" class="btn-produce bg-gray-600 hover:bg-gray-700 px-3 py-2 rounded-lg font-semibold text-sm">
                        ❌ Odznacz
                    </button>
                    <button id="upgradeBase" class="btn-produce bg-indigo-600 hover:bg-indigo-700 px-3 py-2 rounded-lg font-semibold text-sm" title="Upgrade: +HP, +DMG, +Range, +Passive Income">
                        🏰 Upgrade Bazy (1000💰)
                    </button>
                    <button id="upgradeWorkers" class="btn-produce bg-purple-600 hover:bg-purple-700 px-3 py-2 rounded-lg font-semibold text-sm" title="Upgrade: +Speed, +HP, +Capacity">
                        ⚡ Upgrade (?)
                    </button>
                    <button id="produceWorker" class="btn-produce bg-blue-600 hover:bg-blue-700 px-3 py-2 rounded-lg font-semibold text-sm">
                        👷 Robotnik (200💰)
                    </button>
                    <button id="produceKnight" class="btn-produce bg-red-600 hover:bg-red-700 px-3 py-2 rounded-lg font-semibold text-sm">
                        ⚔️ Rycerz (400💰)
                    </button>
                    <button id="produceChampion" class="btn-produce bg-yellow-600 hover:bg-yellow-700 px-3 py-2 rounded-lg font-semibold text-sm">
                        👑 Champion (1500💰)
                    </button>
                </div>
            </div>
        </div>

        <!-- Lista graczy -->
        <div class="fixed top-20 right-4 ui-panel text-white p-4 z-10 rounded-lg" style="min-width: 200px;">
            <h3 class="text-sm font-bold mb-2 opacity-75">👥 GRACZE</h3>
            <div id="playersList" class="text-sm space-y-1"></div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 ui-panel text-white p-3 z-10">
            <div class="max-w-7xl mx-auto">
                <div id="statusLog" class="text-sm opacity-90 h-6 overflow-hidden">
                    Witaj w grze RTS Multiplayer v0.7 BETA!
                </div>
            </div>
        </div>
    </div>

    <canvas id="gameCanvas"></canvas>

    <script>
        // ============================================
        // MULTIPLAYER CLIENT v0.7 BETA
        // ============================================
        
        const CANVAS_WIDTH = 2000;
        const CANVAS_HEIGHT = 1200;
        
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        canvas.width = CANVAS_WIDTH;
        canvas.height = CANVAS_HEIGHT;

        let ws = null;
        let myClientId = null;
        let myTeamId = null;
        let myPlayerName = '';

        const TEAM_COLORS = ['#3b82f6', '#10b981', '#ef4444', '#f59e0b'];

        const gameState = {
            units: new Map(),
            buildings: new Map(),
            players: new Map(),
            goldMines: [],
            selectedUnits: new Set(), // Changed from selectedUnit to selectedUnits
            gameStarted: false,
            
            // Box selection
            isBoxSelecting: false,
            boxStartX: 0,
            boxStartY: 0,
            boxEndX: 0,
            boxEndY: 0,
            
            prevSnapshot: null,
            nextSnapshot: null,
            snapshotTime: 0,
            interpolationFactor: 0
        };

        const joinModal = document.getElementById('joinModal');
        const joinButton = document.getElementById('joinButton');
        const joinStatus = document.getElementById('joinStatus');
        const playerNameInput = document.getElementById('playerName');
        const serverUrlInput = document.getElementById('serverUrl');
        const gameUI = document.getElementById('gameUI');
        const waitingOverlay = document.getElementById('waitingOverlay');

        // ============================================
        // WEBSOCKET CONNECTION
        // ============================================
        
        function connect() {
            const serverUrl = serverUrlInput.value.trim();
            const playerName = playerNameInput.value.trim() || undefined;
            
            joinStatus.textContent = '🔄 Łączenie...';
            joinStatus.className = 'mt-4 text-center text-sm text-yellow-400';
            joinButton.disabled = true;

            ws = new WebSocket(serverUrl);

            ws.onopen = () => {
                console.log('✅ Połączono z serwerem');
                ws.send(JSON.stringify({
                    type: 'join',
                    name: playerName
                }));
            };

            ws.onmessage = (event) => {
                const message = JSON.parse(event.data);
                handleServerMessage(message);
            };

            ws.onerror = (error) => {
                console.error('❌ WebSocket error:', error);
                joinStatus.textContent = '❌ Błąd połączenia';
                joinStatus.className = 'mt-4 text-center text-sm text-red-400';
                joinButton.disabled = false;
            };

            ws.onclose = () => {
                console.log('🔌 Rozłączono z serwerem');
                if (myClientId) {
                    updateStatus('🔌 Rozłączono z serwerem');
                    setTimeout(() => {
                        location.reload();
                    }, 3000);
                } else {
                    joinStatus.textContent = '🔌 Rozłączono';
                    joinStatus.className = 'mt-4 text-center text-sm text-red-400';
                    joinButton.disabled = false;
                }
            };
        }

        joinButton.addEventListener('click', connect);
        
        playerNameInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') connect();
        });

        // ============================================
        // SERVER MESSAGE HANDLER
        // ============================================
        
        function handleServerMessage(message) {
            switch (message.type) {
                case 'joined':
                    myClientId = message.clientId;
                    myTeamId = message.teamId;
                    myPlayerName = message.name;
                    
                    joinModal.classList.add('hidden');
                    gameUI.classList.remove('hidden');
                    
                    document.getElementById('myPlayerName').textContent = myPlayerName;
                    document.getElementById('myTeamColor').style.backgroundColor = TEAM_COLORS[myTeamId];
                    
                    updateStatus(`Dołączyłeś jako ${myPlayerName} (Team ${myTeamId + 1})`);
                    console.log(`✅ Dołączono: ${myPlayerName}, Team ${myTeamId + 1}`);
                    break;

                case 'room_full':
                    joinStatus.textContent = message.message;
                    joinStatus.className = 'mt-4 text-center text-sm text-red-400';
                    joinButton.disabled = false;
                    break;

                case 'snapshot':
                    handleSnapshot(message);
                    break;

                case 'event':
                    handleEvent(message);
                    break;

                case 'game_over':
                    handleGameOver(message);
                    break;

                case 'game_reset':
                    updateStatus(message.message);
                    break;

                case 'pong':
                    break;
            }
        }

        // ============================================
        // SNAPSHOT HANDLING & INTERPOLATION
        // ============================================
        
        function handleSnapshot(snapshot) {
            gameState.prevSnapshot = gameState.nextSnapshot;
            gameState.nextSnapshot = snapshot;
            gameState.snapshotTime = Date.now();
            gameState.interpolationFactor = 0;
            
            gameState.gameStarted = snapshot.gameStarted;

            if (!gameState.gameStarted) {
                waitingOverlay.classList.remove('hidden');
                const playerCount = snapshot.players.length;
                document.getElementById('playerCountText').textContent = `Gracze: ${playerCount}/4`;
            } else {
                waitingOverlay.classList.add('hidden');
            }

            const newUnits = new Map();
            snapshot.units.forEach(unitData => {
                const existing = gameState.units.get(unitData.id);
                if (existing) {
                    unitData.prevX = existing.x;
                    unitData.prevY = existing.y;
                } else {
                    unitData.prevX = unitData.x;
                    unitData.prevY = unitData.y;
                }
                newUnits.set(unitData.id, unitData);
            });
            gameState.units = newUnits;

            const newBuildings = new Map();
            snapshot.buildings.forEach(buildingData => {
                newBuildings.set(buildingData.id, buildingData);
            });
            gameState.buildings = newBuildings;

            const newPlayers = new Map();
            snapshot.players.forEach(playerData => {
                newPlayers.set(playerData.clientId, playerData);
            });
            gameState.players = newPlayers;

            if (snapshot.goldMines && snapshot.goldMines.length > 0) {
                gameState.goldMines = snapshot.goldMines;
            }

            updateUI();
        }

        function handleEvent(event) {
            switch (event.event) {
                case 'player_joined':
                    updateStatus(`${event.name} dołączył do gry! (Team ${event.teamId + 1})`);
                    break;
                case 'player_left':
                    updateStatus(`${event.name} opuścił grę`);
                    break;
                case 'game_started':
                    updateStatus(event.message);
                    break;
                case 'game_paused':
                    updateStatus(event.message);
                    break;
                case 'unit_produced':
                    if (event.teamId === myTeamId) {
                        const unitName = event.unitType === 'worker' ? 'robotnika 👷' : 
                                        event.unitType === 'knight' ? 'rycerza ⚔️' : 
                                        'championa 👑';
                        updateStatus(`Wyprodukowano ${unitName}`);
                    }
                    break;
                case 'worker_upgraded':
                    if (event.teamId === myTeamId) {
                        updateStatus(`⚡ Robotnicy zostali ulepszeni!`);
                    } else {
                        updateStatus(`⚡ ${event.playerName} ulepszył robotników`);
                    }
                    break;
                case 'base_upgraded':
                    if (event.teamId === myTeamId) {
                        updateStatus(`🏰 Baza została ulepszona!`);
                    } else {
                        updateStatus(`🏰 ${event.playerName} ulepszył bazę`);
                    }
                    break;
                case 'base_destroyed':
                    updateStatus(`💀 Baza gracza ${event.playerName} została zniszczona!`);
                    break;
                case 'mine_depleted':
                    updateStatus(`⛏️ Kopalnia została wyczerpana!`);
                    break;
                case 'base_attack':
                    // Wizualizacja strzału wieży
                    break;
                case 'unit_died':
                    break;
            }
        }

        function handleGameOver(message) {
            const overlay = document.createElement('div');
            overlay.className = 'fixed inset-0 bg-black bg-opacity-80 flex items-center justify-center z-50';
            overlay.innerHTML = `
                <div class="bg-gray-800 p-12 rounded-lg shadow-2xl text-center max-w-lg">
                    <h1 class="text-5xl font-bold text-white mb-4">${message.message}</h1>
                    ${message.winner ? `<p class="text-2xl text-yellow-400 mb-6">👑 ${message.winner}</p>` : ''}
                    <p class="text-gray-300 mb-6">Gra zostanie zresetowana za 5 sekund...</p>
                    <div class="animate-pulse text-6xl">🏆</div>
                </div>
            `;
            document.body.appendChild(overlay);

            setTimeout(() => {
                overlay.remove();
            }, 5000);
        }

        // ============================================
        // UI UPDATES
        // ============================================
        
        function updateUI() {
            const myPlayer = gameState.players.get(myClientId);
            if (!myPlayer) return;

            document.getElementById('goldDisplay').textContent = myPlayer.gold;
            
            const myUnits = Array.from(gameState.units.values()).filter(u => u.teamId === myTeamId);
            const workers = myUnits.filter(u => u.type === 'worker').length;
            const knights = myUnits.filter(u => u.type === 'knight').length;
            const champions = myUnits.filter(u => u.type === 'champion').length;
            
            // Update upgrade workers button
            const upgradeCost = 1000 + (workers * 100);
            const upgradeBtn = document.getElementById('upgradeWorkers');
            upgradeBtn.textContent = `⚡ Upgrade (${upgradeCost}💰)`;
            upgradeBtn.disabled = myPlayer.gold < upgradeCost || myPlayer.workerUpgraded;
            
            if (myPlayer.workerUpgraded) {
                upgradeBtn.textContent = '⚡ Upgraded ✓';
                upgradeBtn.classList.remove('bg-purple-600', 'hover:bg-purple-700');
                upgradeBtn.classList.add('bg-green-600');
            }
            
            const myBase = gameState.buildings.get(`base-${myClientId}`);
            const baseAlive = myBase && myBase.health > 0;
            const baseUpgraded = myBase && myBase.upgraded;
            
            // Update base upgrade button
            const baseUpgradeBtn = document.getElementById('upgradeBase');
            baseUpgradeBtn.disabled = myPlayer.gold < 1000 || !baseAlive || baseUpgraded;
            
            if (baseUpgraded) {
                baseUpgradeBtn.textContent = '🏰 Upgraded ✓';
                baseUpgradeBtn.classList.remove('bg-indigo-600', 'hover:bg-indigo-700');
                baseUpgradeBtn.classList.add('bg-green-600');
            }
            
            document.getElementById('produceWorker').disabled = myPlayer.gold < 200 || !baseAlive || workers >= 25;
            document.getElementById('produceKnight').disabled = myPlayer.gold < 400 || !baseAlive;
            document.getElementById('produceChampion').disabled = myPlayer.gold < 1500 || !baseAlive;
            
            // Update deselect button
            document.getElementById('deselectAll').disabled = gameState.selectedUnits.size === 0;
            
            document.getElementById('workerCount').textContent = workers;
            document.getElementById('knightCount').textContent = knights;
            document.getElementById('championCount').textContent = champions;

            updatePlayersList();
        }

        function updatePlayersList() {
            const playersList = document.getElementById('playersList');
            playersList.innerHTML = '';

            gameState.players.forEach(player => {
                const div = document.createElement('div');
                div.className = 'flex items-center justify-between';
                
                const base = gameState.buildings.get(`base-${player.clientId}`);
                const isAlive = base && base.health > 0;
                
                const upgradeIcon = player.workerUpgraded ? ' ⚡' : '';
                
                div.innerHTML = `
                    <div class="flex items-center">
                        <span class="team-indicator" style="background: ${TEAM_COLORS[player.teamId]}"></span>
                        <span class="${player.clientId === myClientId ? 'font-bold' : ''} ${!isAlive ? 'line-through opacity-50' : ''}">
                            ${player.name}${upgradeIcon}
                        </span>
                    </div>
                    <span class="text-yellow-400">${player.gold}💰</span>
                `;
                
                playersList.appendChild(div);
            });
        }

        function updateStatus(message) {
            document.getElementById('statusLog').textContent = message;
        }

        // ============================================
        // COMMAND SENDING
        // ============================================
        
        function sendCommand(command, payload) {
            if (ws && ws.readyState === WebSocket.OPEN) {
                ws.send(JSON.stringify({
                    type: 'command',
                    command,
                    payload
                }));
            }
        }

        document.getElementById('produceWorker').addEventListener('click', () => {
            sendCommand('produce', { unitType: 'worker' });
        });

        document.getElementById('produceKnight').addEventListener('click', () => {
            sendCommand('produce', { unitType: 'knight' });
        });

        document.getElementById('produceChampion').addEventListener('click', () => {
            sendCommand('produce', { unitType: 'champion' });
        });

        document.getElementById('upgradeWorkers').addEventListener('click', () => {
            sendCommand('upgrade_workers', {});
        });

        document.getElementById('upgradeBase').addEventListener('click', () => {
            sendCommand('upgrade_base', {});
        });

        document.getElementById('deselectAll').addEventListener('click', () => {
            gameState.selectedUnits.forEach(unit => {
                unit.selected = false;
            });
            gameState.selectedUnits.clear();
            updateStatus('Odznaczono wszystkie jednostki');
        });

        // ============================================
        // CANVAS INTERACTIONS - BOX SELECTION
        // ============================================
        
        canvas.addEventListener('mousedown', (e) => {
            const rect = canvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;

            // Start box selection
            gameState.isBoxSelecting = true;
            gameState.boxStartX = x;
            gameState.boxStartY = y;
            gameState.boxEndX = x;
            gameState.boxEndY = y;
        });

        canvas.addEventListener('mousemove', (e) => {
            if (!gameState.isBoxSelecting) return;

            const rect = canvas.getBoundingClientRect();
            gameState.boxEndX = e.clientX - rect.left;
            gameState.boxEndY = e.clientY - rect.top;
        });

        canvas.addEventListener('mouseup', (e) => {
            if (!gameState.isBoxSelecting) return;

            const rect = canvas.getBoundingClientRect();
            const endX = e.clientX - rect.left;
            const endY = e.clientY - rect.top;

            gameState.isBoxSelecting = false;

            const minX = Math.min(gameState.boxStartX, endX);
            const maxX = Math.max(gameState.boxStartX, endX);
            const minY = Math.min(gameState.boxStartY, endY);
            const maxY = Math.max(gameState.boxStartY, endY);

            const boxWidth = maxX - minX;
            const boxHeight = maxY - minY;

            // If box is very small (< 10px), treat as click
            if (boxWidth < 10 && boxHeight < 10) {
                handleClick(gameState.boxStartX, gameState.boxStartY);
                return;
            }

            // Box selection - select all units in box
            const unitsInBox = [];
            gameState.units.forEach(unit => {
                if (unit.teamId === myTeamId && 
                    unit.x >= minX && unit.x <= maxX &&
                    unit.y >= minY && unit.y <= maxY) {
                    unitsInBox.push(unit);
                }
            });

            if (unitsInBox.length > 0) {
                // Deselect old units
                gameState.selectedUnits.forEach(unit => {
                    unit.selected = false;
                });
                gameState.selectedUnits.clear();

                // Select new units
                unitsInBox.forEach(unit => {
                    unit.selected = true;
                    gameState.selectedUnits.add(unit);
                });

                updateStatus(`Zaznaczono ${unitsInBox.length} jednostek`);
            }
        });

        function handleClick(x, y) {
            // Check if clicked on unit
            let clickedUnit = null;
            gameState.units.forEach(unit => {
                if (unit.teamId === myTeamId && distance(unit.x, unit.y, x, y) < unit.size + 5) {
                    clickedUnit = unit;
                }
            });

            // Check if clicked on mine
            let clickedMine = null;
            gameState.goldMines.forEach(mine => {
                if (!mine.depleted && distance(mine.x, mine.y, x, y) < mine.size / 2 + 5) {
                    clickedMine = mine;
                }
            });

            if (clickedUnit) {
                // Single click on unit - select only this unit
                gameState.selectedUnits.forEach(unit => {
                    unit.selected = false;
                });
                gameState.selectedUnits.clear();

                clickedUnit.selected = true;
                gameState.selectedUnits.add(clickedUnit);

                const unitName = clickedUnit.type === 'worker' ? 'robotnika 👷' : 
                                 clickedUnit.type === 'knight' ? 'rycerza ⚔️' : 
                                 'championa 👑';
                updateStatus(`Wybrano ${unitName}`);
            } else if (clickedMine && gameState.selectedUnits.size > 0) {
                // Check if all selected units are workers
                const allWorkers = Array.from(gameState.selectedUnits).every(u => u.type === 'worker');
                
                if (allWorkers) {
                    // Send all workers to mine
                    gameState.selectedUnits.forEach(unit => {
                        sendCommand('mine', {
                            unitId: unit.id,
                            mineId: clickedMine.id
                        });
                    });
                    updateStatus(`Wysłano ${gameState.selectedUnits.size} robotników do kopalni 💰`);
                } else {
                    updateStatus('⚠️ Tylko robotnicy mogą kopać!');
                }
            } else if (gameState.selectedUnits.size > 0) {
                // Move selected units
                gameState.selectedUnits.forEach(unit => {
                    sendCommand('move', {
                        unitId: unit.id,
                        x,
                        y
                    });
                });
                updateStatus(`Wysłano ${gameState.selectedUnits.size} jednostek do (${Math.floor(x)}, ${Math.floor(y)})`);
            }
        }

        function distance(x1, y1, x2, y2) {
            return Math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2);
        }

        // ============================================
        // RENDERING
        // ============================================
        
        function draw() {
            ctx.clearRect(0, 0, CANVAS_WIDTH, CANVAS_HEIGHT);

            const timeSinceSnapshot = Date.now() - gameState.snapshotTime;
            gameState.interpolationFactor = Math.min(timeSinceSnapshot / 100, 1);

            // Draw mines
            gameState.goldMines.forEach(mine => {
                if (mine.depleted) {
                    // Depleted mine - gray
                    ctx.fillStyle = '#4b5563';
                    ctx.beginPath();
                    ctx.arc(mine.x, mine.y, mine.size / 2, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.strokeStyle = '#1f2937';
                    ctx.lineWidth = 3;
                    ctx.stroke();

                    ctx.fillStyle = '#1f2937';
                    ctx.font = 'bold 16px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('❌', mine.x, mine.y);
                } else {
                    // Active mine
                    const percent = mine.remainingGold / mine.totalGold;
                    const color = percent > 0.5 ? '#fbbf24' : percent > 0.25 ? '#f59e0b' : '#dc2626';
                    
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(mine.x, mine.y, mine.size / 2, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.strokeStyle = '#92400e';
                    ctx.lineWidth = 3;
                    ctx.stroke();

                    ctx.fillStyle = '#92400e';
                    ctx.font = 'bold 20px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('💰', mine.x, mine.y);

                    // Show remaining gold
                    ctx.fillStyle = '#fff';
                    ctx.font = 'bold 12px Arial';
                    ctx.fillText(`${mine.remainingGold}`, mine.x, mine.y + 30);
                }
            });

            // Draw buildings
            gameState.buildings.forEach(building => {
                if (building.health <= 0) {
                    // Destroyed base - rubble
                    ctx.fillStyle = '#4b5563';
                    ctx.fillRect(building.x - building.size/2, building.y - building.size/2, building.size, building.size);
                    ctx.strokeStyle = '#1f2937';
                    ctx.lineWidth = 3;
                    ctx.strokeRect(building.x - building.size/2, building.y - building.size/2, building.size, building.size);

                    ctx.fillStyle = '#dc2626';
                    ctx.font = 'bold 24px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('💀', building.x, building.y);
                    return;
                }

                const color = TEAM_COLORS[building.teamId];
                
                // Base color - darker if upgraded
                const baseColor = building.upgraded ? '#1e3a8a' : color;
                
                ctx.fillStyle = baseColor;
                ctx.fillRect(building.x - building.size/2, building.y - building.size/2, building.size, building.size);
                ctx.strokeStyle = building.upgraded ? '#fbbf24' : '#000';
                ctx.lineWidth = building.upgraded ? 4 : 3;
                ctx.strokeRect(building.x - building.size/2, building.y - building.size/2, building.size, building.size);

                // Roof
                ctx.fillStyle = building.upgraded ? '#92400e' : '#8b4513';
                ctx.beginPath();
                ctx.moveTo(building.x, building.y - building.size/2 - 15);
                ctx.lineTo(building.x - building.size/2 - 10, building.y - building.size/2);
                ctx.lineTo(building.x + building.size/2 + 10, building.y - building.size/2);
                ctx.closePath();
                ctx.fill();
                ctx.stroke();

                // Upgraded icon
                if (building.upgraded) {
                    ctx.fillStyle = '#fbbf24';
                    ctx.font = 'bold 20px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('🏰', building.x, building.y);
                }

                const barWidth = building.size;
                const barHeight = 6;
                const hpPercent = building.health / building.maxHealth;
                
                ctx.fillStyle = '#333';
                ctx.fillRect(building.x - barWidth/2, building.y - building.size/2 - 25, barWidth, barHeight);
                ctx.fillStyle = hpPercent > 0.5 ? '#10b981' : hpPercent > 0.25 ? '#f59e0b' : '#ef4444';
                ctx.fillRect(building.x - barWidth/2, building.y - building.size/2 - 25, barWidth * hpPercent, barHeight);

                // Turret range visualization for own base
                if (building.teamId === myTeamId && building.health > 0) {
                    const range = building.upgraded ? 1200 : 800;
                    ctx.strokeStyle = building.upgraded ? 'rgba(251, 191, 36, 0.3)' : 'rgba(239, 68, 68, 0.3)';
                    ctx.lineWidth = 2;
                    ctx.setLineDash([5, 5]);
                    ctx.beginPath();
                    ctx.arc(building.x, building.y, range, 0, Math.PI * 2);
                    ctx.stroke();
                    ctx.setLineDash([]);
                }
            });

            // Draw units
            gameState.units.forEach(unit => {
                const displayX = unit.prevX + (unit.x - unit.prevX) * gameState.interpolationFactor;
                const displayY = unit.prevY + (unit.y - unit.prevY) * gameState.interpolationFactor;

                const color = TEAM_COLORS[unit.teamId];

                if (unit.type === 'worker') {
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(displayX, displayY, unit.size, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.strokeStyle = '#000';
                    ctx.lineWidth = 2;
                    ctx.stroke();

                    if (unit.upgraded) {
                        ctx.strokeStyle = '#fbbf24';
                        ctx.lineWidth = 3;
                        ctx.stroke();
                    }

                    ctx.fillStyle = '#fff';
                    ctx.font = 'bold 16px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText(unit.upgraded ? '👷⚡' : '👷', displayX, displayY);

                    if (unit.carryingGold > 0) {
                        ctx.fillStyle = '#fbbf24';
                        ctx.font = 'bold 12px Arial';
                        ctx.fillText(`${unit.carryingGold}💰`, displayX, displayY - 25);
                    }

                    const wBarWidth = 40;
                    const wBarHeight = 3;
                    const wHpPercent = unit.health / unit.maxHealth;
                    
                    ctx.fillStyle = '#333';
                    ctx.fillRect(displayX - wBarWidth/2, displayY - unit.size - 8, wBarWidth, wBarHeight);
                    ctx.fillStyle = wHpPercent > 0.5 ? '#10b981' : wHpPercent > 0.25 ? '#f59e0b' : '#ef4444';
                    ctx.fillRect(displayX - wBarWidth/2, displayY - unit.size - 8, wBarWidth * wHpPercent, wBarHeight);
                } else if (unit.type === 'knight') {
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.moveTo(displayX, displayY - unit.size);
                    ctx.lineTo(displayX - unit.size, displayY + unit.size);
                    ctx.lineTo(displayX + unit.size, displayY + unit.size);
                    ctx.closePath();
                    ctx.fill();
                    ctx.strokeStyle = '#000';
                    ctx.lineWidth = 2;
                    ctx.stroke();

                    ctx.fillStyle = '#fff';
                    ctx.font = 'bold 14px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('⚔️', displayX, displayY);

                    const barWidth = 40;
                    const barHeight = 4;
                    const hpPercent = unit.health / unit.maxHealth;
                    
                    ctx.fillStyle = '#333';
                    ctx.fillRect(displayX - barWidth/2, displayY - unit.size - 10, barWidth, barHeight);
                    ctx.fillStyle = hpPercent > 0.5 ? '#10b981' : hpPercent > 0.25 ? '#f59e0b' : '#ef4444';
                    ctx.fillRect(displayX - barWidth/2, displayY - unit.size - 10, barWidth * hpPercent, barHeight);
                } else if (unit.type === 'champion') {
                    // Champion - larger shield shape
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.moveTo(displayX, displayY - unit.size);
                    ctx.lineTo(displayX - unit.size, displayY);
                    ctx.lineTo(displayX - unit.size * 0.7, displayY + unit.size);
                    ctx.lineTo(displayX + unit.size * 0.7, displayY + unit.size);
                    ctx.lineTo(displayX + unit.size, displayY);
                    ctx.closePath();
                    ctx.fill();
                    ctx.strokeStyle = '#fbbf24';
                    ctx.lineWidth = 3;
                    ctx.stroke();

                    ctx.fillStyle = '#fff';
                    ctx.font = 'bold 18px Arial';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('👑', displayX, displayY);

                    const barWidth = 50;
                    const barHeight = 5;
                    const hpPercent = unit.health / unit.maxHealth;
                    
                    ctx.fillStyle = '#333';
                    ctx.fillRect(displayX - barWidth/2, displayY - unit.size - 12, barWidth, barHeight);
                    ctx.fillStyle = hpPercent > 0.5 ? '#10b981' : hpPercent > 0.25 ? '#f59e0b' : '#ef4444';
                    ctx.fillRect(displayX - barWidth/2, displayY - unit.size - 12, barWidth * hpPercent, barHeight);
                }

                // RED highlight for selected units
                if (unit.selected && unit.teamId === myTeamId) {
                    ctx.strokeStyle = '#ef4444'; // RED
                    ctx.lineWidth = 4;
                    ctx.beginPath();
                    ctx.arc(displayX, displayY, unit.size + 10, 0, Math.PI * 2);
                    ctx.stroke();
                }
            });

            // Draw box selection rectangle (YELLOW)
            if (gameState.isBoxSelecting) {
                const minX = Math.min(gameState.boxStartX, gameState.boxEndX);
                const minY = Math.min(gameState.boxStartY, gameState.boxEndY);
                const width = Math.abs(gameState.boxEndX - gameState.boxStartX);
                const height = Math.abs(gameState.boxEndY - gameState.boxStartY);

                ctx.strokeStyle = '#fbbf24'; // YELLOW
                ctx.lineWidth = 2;
                ctx.setLineDash([5, 5]);
                ctx.strokeRect(minX, minY, width, height);
                ctx.setLineDash([]);

                // Fill with transparent yellow
                ctx.fillStyle = 'rgba(251, 191, 36, 0.1)';
                ctx.fillRect(minX, minY, width, height);
            }

            requestAnimationFrame(draw);
        }

        draw();
    </script>
</body>
</html>
