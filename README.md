<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎮 Interactive Bettercap Mastery Guide</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 50%, #16213e 100%);
            color: #ffffff;
            line-height: 1.6;
            overflow-x: hidden;
        }

        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.1;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        .header {
            text-align: center;
            padding: 40px 0;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1);
            background-size: 400% 400%;
            animation: gradientShift 3s ease infinite;
            border-radius: 20px;
            margin-bottom: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        .warning-box {
            background: linear-gradient(45deg, #ff4757, #ff3838);
            padding: 30px;
            border-radius: 15px;
            margin: 30px 0;
            border-left: 5px solid #ff1744;
            box-shadow: 0 10px 30px rgba(255, 71, 87, 0.3);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }

        .achievement-system {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(0,0,0,0.8);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            z-index: 1000;
        }

        .achievement {
            padding: 10px;
            margin: 5px 0;
            background: linear-gradient(45deg, #4ecdc4, #45b7d1);
            border-radius: 5px;
            font-size: 0.9em;
            opacity: 0;
            transform: translateX(100px);
            animation: slideIn 0.5s ease forwards;
        }

        @keyframes slideIn {
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: rgba(255,255,255,0.1);
            border-radius: 5px;
            overflow: hidden;
            margin: 20px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4ecdc4, #45b7d1);
            width: 0%;
            transition: width 0.3s ease;
            border-radius: 5px;
        }

        .section {
            background: rgba(255,255,255,0.05);
            backdrop-filter: blur(10px);
            padding: 30px;
            margin: 30px 0;
            border-radius: 15px;
            border: 1px solid rgba(255,255,255,0.1);
            transition: all 0.3s ease;
            opacity: 0;
            transform: translateY(50px);
        }

        .section.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .section:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.3);
        }

        .command-block {
            background: #1a1a1a;
            padding: 20px;
            border-radius: 10px;
            margin: 15px 0;
            border-left: 4px solid #4ecdc4;
            font-family: 'Courier New', monospace;
            position: relative;
            overflow: hidden;
        }

        .command-block::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.5s ease;
        }

        .command-block:hover::before {
            left: 100%;
        }

        .command-block code {
            color: #4ecdc4;
            font-size: 0.9em;
        }

        .interactive-button {
            background: linear-gradient(45deg, #4ecdc4, #45b7d1);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1em;
            margin: 10px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .interactive-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        .interactive-button:active {
            transform: translateY(0);
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            margin: 10% auto;
            padding: 30px;
            border-radius: 15px;
            width: 80%;
            max-width: 600px;
            border: 1px solid rgba(255,255,255,0.1);
            animation: modalSlide 0.3s ease;
        }

        @keyframes modalSlide {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }

        .close:hover {
            color: #fff;
        }

        .skill-tree {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .skill-node {
            background: linear-gradient(45deg, #2c3e50, #34495e);
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            position: relative;
        }

        .skill-node:hover {
            border-color: #4ecdc4;
            transform: scale(1.05);
        }

        .skill-node.unlocked {
            background: linear-gradient(45deg, #4ecdc4, #45b7d1);
            box-shadow: 0 0 20px rgba(78, 205, 196, 0.5);
        }

        .xp-counter {
            position: fixed;
            top: 20px;
            left: 20px;
            background: rgba(0,0,0,0.8);
            padding: 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            z-index: 1000;
        }

        .xp-gain {
            position: fixed;
            font-size: 1.5em;
            color: #4ecdc4;
            font-weight: bold;
            z-index: 1001;
            animation: xpPop 2s ease forwards;
        }

        @keyframes xpPop {
            0% { transform: scale(0.5); opacity: 0; }
            20% { transform: scale(1.2); opacity: 1; }
            100% { transform: scale(1) translateY(-50px); opacity: 0; }
        }

        .terminal-simulator {
            background: #000;
            color: #00ff00;
            padding: 20px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            margin: 20px 0;
            min-height: 200px;
            overflow-y: auto;
        }

        .terminal-line {
            margin: 5px 0;
            opacity: 0;
            animation: typewriter 0.5s ease forwards;
        }

        @keyframes typewriter {
            to { opacity: 1; }
        }

        .easter-egg {
            position: fixed;
            font-size: 2em;
            z-index: 1001;
            animation: bounce 2s ease infinite;
            cursor: pointer;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-30px); }
            60% { transform: translateY(-15px); }
        }

        .particle {
            position: fixed;
            width: 4px;
            height: 4px;
            background: #4ecdc4;
            border-radius: 50%;
            z-index: 999;
            animation: particle 2s ease forwards;
        }

        @keyframes particle {
            0% { transform: scale(1); opacity: 1; }
            100% { transform: scale(0) translateY(-100px); opacity: 0; }
        }

        .tooltip {
            position: relative;
            display: inline-block;
            cursor: help;
        }

        .tooltip .tooltiptext {
            visibility: hidden;
            width: 200px;
            background: rgba(0,0,0,0.9);
            color: #fff;
            text-align: center;
            padding: 10px;
            border-radius: 6px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -100px;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }

        .mini-game {
            background: linear-gradient(45deg, #2c3e50, #34495e);
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            text-align: center;
        }

        .network-visual {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 200px;
            margin: 20px 0;
        }

        .node {
            width: 30px;
            height: 30px;
            background: #4ecdc4;
            border-radius: 50%;
            margin: 10px;
            animation: pulse 2s infinite;
            position: relative;
        }

        .node::before {
            content: '';
            position: absolute;
            width: 50px;
            height: 2px;
            background: #4ecdc4;
            right: -50px;
            top: 50%;
            transform: translateY(-50%);
        }

        .node:last-child::before {
            display: none;
        }
    </style>
</head>
<body>
    <canvas class="matrix-bg" id="matrixCanvas"></canvas>
    
    <div class="achievement-system" id="achievements">
        <h4>🏆 Achievements</h4>
        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>
        <div id="achievementList"></div>
    </div>

    <div class="xp-counter">
        <h4>⚡ Experience</h4>
        <div>Level: <span id="level">1</span></div>
        <div>XP: <span id="xp">0</span> / <span id="nextLevelXP">100</span></div>
    </div>

    <div class="container">
        <div class="header">
            <h1>🎮 Interactive Bettercap Mastery Guide</h1>
            <p>Level up your network security skills with this gamified learning experience!</p>
        </div>

        <div class="warning-box">
            <h3>⚠️ CRITICAL DISCLAIMER - READ BEFORE PROCEEDING</h3>
            <p><strong>This guide is for educational purposes and authorized penetration testing ONLY.</strong></p>
            <p>Bettercap is a powerful network security tool that should only be used on networks you own or have explicit written permission to test. Unauthorized network attacks are illegal and unethical.</p>
            <button class="interactive-button" onclick="acceptDisclaimer()">I Understand and Accept</button>
        </div>

        <div class="section" id="whatIs">
            <h2>🎯 What is Bettercap?</h2>
            <p>Bettercap is a comprehensive, modular MITM framework for network security assessments.</p>
            
            <div class="network-visual">
                <div class="node" title="Attacker"></div>
                <div class="node" title="Target"></div>
                <div class="node" title="Router"></div>
            </div>

            <div class="skill-tree">
                <div class="skill-node" onclick="unlockSkill('discovery')">
                    <h4>🔍 Network Discovery</h4>
                    <p>Identify active devices</p>
                </div>
                <div class="skill-node" onclick="unlockSkill('mitm')">
                    <h4>🕸️ MITM Attacks</h4>
                    <p>Intercept network traffic</p>
                </div>
                <div class="skill-node" onclick="unlockSkill('analysis')">
                    <h4>📊 Traffic Analysis</h4>
                    <p>Analyze captured data</p>
                </div>
            </div>
            
            <button class="interactive-button" onclick="gainXP(10)">Explore Features (+10 XP)</button>
        </div>

        <div class="section" id="installation">
            <h2>📦 Installation Quest</h2>
            <p>Complete the installation to unlock advanced modules!</p>
            
            <div class="mini-game">
                <h4>🎮 Installation Mini-Game</h4>
                <p>Click the commands in the correct order:</p>
                <div id="installationGame">
                    <button class="interactive-button" onclick="installStep(1)">Update System</button>
                    <button class="interactive-button" onclick="installStep(2)">Install Dependencies</button>
                    <button class="interactive-button" onclick="installStep(3)">Clone Repository</button>
                    <button class="interactive-button" onclick="installStep(4)">Build & Install</button>
                </div>
            </div>

            <div class="command-block">
                <h4>Step 1: System Dependencies</h4>
                <code>
sudo apt update<br>
sudo apt install -y build-essential libpcap-dev libusb-1.0-0-dev pkg-config git ruby-dev libnetfilter-queue-dev golang
                </code>
            </div>

            <div class="command-block">
                <h4>Step 2: Clone Repository</h4>
                <code>
cd ~<br>
git clone https://github.com/bettercap/bettercap.git
                </code>
            </div>

            <div class="command-block">
                <h4>Step 3: Build and Install</h4>
                <code>
cd bettercap<br>
make build<br>
sudo make install
                </code>
            </div>
        </div>

        <div class="section" id="basicUsage">
            <h2>🚀 Basic Usage Training</h2>
            
            <div class="terminal-simulator" id="terminalSim">
                <div class="terminal-line">bettercap@kali:~$ sudo bettercap -iface wlan0</div>
                <div class="terminal-line">bettercap > net.probe on</div>
                <div class="terminal-line">bettercap > net.recon on</div>
                <div class="terminal-line">bettercap > net.show</div>
            </div>

            <button class="interactive-button" onclick="simulateCommand()">Run Simulation</button>
            <button class="interactive-button" onclick="openModal('basicCommands')">View All Commands</button>
        </div>

        <div class="section" id="modules">
            <h2>🔧 Core Modules Mastery</h2>
            
            <div class="skill-tree">
                <div class="skill-node tooltip" onclick="moduleDemo('arp')">
                    <h4>🎯 ARP Spoofing</h4>
                    <p>MITM via ARP poisoning</p>
                    <span class="tooltiptext">Intercept traffic by poisoning ARP tables</span>
                </div>
                <div class="skill-node tooltip" onclick="moduleDemo('dns')">
                    <h4>🌐 DNS Spoofing</h4>
                    <p>Redirect domain queries</p>
                    <span class="tooltiptext">Redirect users to malicious sites</span>
                </div>
                <div class="skill-node tooltip" onclick="moduleDemo('sniff')">
                    <h4>📡 Packet Sniffing</h4>
                    <p>Capture network traffic</p>
                    <span class="tooltiptext">Monitor and log network packets</span>
                </div>
                <div class="skill-node tooltip" onclick="moduleDemo('https')">
                    <h4>🔐 HTTPS Proxy</h4>
                    <p>SSL/TLS interception</p>
                    <span class="tooltiptext">Decrypt HTTPS traffic</span>
                </div>
            </div>
        </div>

        <div class="section" id="advanced">
            <h2>🧪 Advanced Techniques</h2>
            
            <div class="command-block">
                <h4>🎯 Full MITM Setup</h4>
                <code>
# Enable ARP spoofing for entire subnet<br>
set arp.spoof.targets 192.168.1.0/24<br>
set arp.spoof.internal true<br>
arp.spoof on<br><br>

# Start packet capture<br>
net.sniff on<br><br>

# Enable HTTPS proxy with SSL stripping<br>
set https.proxy.sslstrip true<br>
https.proxy on
                </code>
            </div>

            <div class="command-block">
                <h4>🌐 DNS Spoofing Attack</h4>
                <code>
# Redirect Facebook to Google<br>
set dns.spoof.domains facebook.com<br>
set dns.spoof.address 142.250.190.14<br>
dns.spoof on<br><br>

# Block a website completely<br>
set dns.spoof.domains badsite.com<br>
set dns.spoof.address 0.0.0.0<br>
dns.spoof on
                </code>
            </div>

            <div class="command-block">
                <h4>📊 Advanced Logging</h4>
                <code>
# Verbose logging to file<br>
set net.sniff.verbose true<br>
set net.sniff.output /tmp/capture.log<br>
net.sniff on<br><br>

# Stream events to file<br>
set events.stream.output /tmp/events.log<br>
events.stream on
                </code>
            </div>
        </div>

        <div class="section" id="gui">
            <h2>🖥️ Web Interface</h2>
            <p>Access the real-time GUI for visual monitoring!</p>
            
            <div class="command-block">
                <h4>Enable Web UI</h4>
                <code>
caplets.update<br>
ui.update<br>
ui.enable<br><br>
# Access at https://localhost:8080
                </code>
            </div>
            
            <button class="interactive-button" onclick="openModal('guiDemo')">View GUI Demo</button>
        </div>

        <div class="section" id="caplets">
            <h2>📜 Caplets (Batch Scripts)</h2>
            
            <div class="command-block">
                <h4>Create Custom Caplet</h4>
                <code>
# Create mitm.cap file<br>
echo "set arp.spoof.internal true<br>
set arp.spoof.targets 192.168.1.0/24<br>
arp.spoof on<br>
net.sniff on<br>
ui.enable" > mitm.cap<br><br>

# Run caplet<br>
sudo bettercap -iface wlan0 -caplet mitm.cap
                </code>
            </div>
        </div>

        <div class="section" id="troubleshooting">
            <h2>🔧 Troubleshooting</h2>
            
            <div class="command-block">
                <h4>Common Issues & Solutions</h4>
                <code>
# Enable IP forwarding<br>
echo 1 > /proc/sys/net/ipv4/ip_forward<br><br>

# Fix permission issues<br>
sudo setcap cap_net_raw,cap_net_admin+eip /usr/local/bin/bettercap<br><br>

# Check interface status<br>
ip addr show<br>
iwconfig
                </code>
            </div>
        </div>

        <div class="section" id="reset">
            <h2>🔄 Reset All Attacks</h2>
            <div class="command-block">
                <code>
# Stop all modules<br>
net.recon off<br>
arp.spoof off<br>
dns.spoof off<br>
net.sniff off<br>
https.proxy off<br>
http.proxy off<br><br>

# Or press Ctrl+C to exit
                </code>
            </div>
            <button class="interactive-button" onclick="resetProgress()">Reset Learning Progress</button>
        </div>
    </div>

    <!-- Modals -->
    <div id="basicCommands" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('basicCommands')">&times;</span>
            <h3>📚 Essential Commands</h3>
            <div class="command-block">
                <code>
help                    # Show all modules<br>
help &lt;module&gt;          # Get module info<br>
net.probe on           # Start network discovery<br>
net.recon on           # Start network reconnaissance<br>
net.show               # Display discovered hosts<br>
arp.spoof on           # Start ARP spoofing<br>
dns.spoof on           # Start DNS spoofing<br>
net.sniff on           # Start packet capture<br>
events.stream on       # Start event logging<br>
ui.enable              # Enable web interface
                </code>
            </div>
        </div>
    </div>

    <div id="guiDemo" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('guiDemo')">&times;</span>
            <h3>🖥️ Web Interface Demo</h3>
            <p>The Bettercap web interface provides:</p>
            <ul>
                <li>Real-time network mapping</li>
                <li>Live traffic monitoring</li>
                <li>Module control panels</li>
                <li>Event logging dashboard</li>
                <li>Interactive network graph</li>
            </ul>
            <p>Access it at <strong>https://localhost:8080</strong> after running <code>ui.enable</code></p>
        </div>
    </div>

    <script>
        // Game state
        let gameState = {
            level: 1,
            xp: 0,
            nextLevelXP: 100,
            achievements: [],
            unlockedSkills: [],
            installStep: 0
        };

        // Load saved progress
        if (localStorage.getItem('bettercapProgress')) {
            gameState = JSON.parse(localStorage.getItem('bettercapProgress'));
            updateUI();
        }

        // Matrix background animation
        const canvas = document.getElementById('matrixCanvas');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const matrix = "ABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@#$%^&*()*&^%+-/~{[|`]}";
        const matrixArray = matrix.split("");
        
        const fontSize = 10;
        const columns = canvas.width / fontSize;
        const drops = [];
        
        for (let x = 0; x < columns; x++) {
            drops[x] = 1;
        }
        
        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.04)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = '#0F3460';
            ctx.font = fontSize + 'px arial';
            
            for (let i = 0; i < drops.length; i++) {
                const text = matrixArray[Math.floor(Math.random() * matrixArray.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }
        
        setInterval(drawMatrix, 35);

        // Intersection Observer for animations
        const observer = new IntersectionObserver((entries) => {
            entries.forEach((entry) => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        });

        document.querySelectorAll('.section').forEach((section) => {
            observer.observe(section);
        });

        // Game functions
        function gainXP(amount) {
            gameState.xp += amount;
            showXPGain(amount);
            
            if (gameState.xp >= gameState.nextLevelXP) {
                levelUp();
            }
            
            updateUI();
            saveProgress();
        }

        function showXPGain(amount) {
            const xpGain = document.createElement('div');
            xpGain.className = 'xp-gain';
            xpGain.textContent = `+${amount} XP`;
            xpGain.style.left = Math.random() * (window.innerWidth - 100) + 'px';
            xpGain.style.top = Math.random() * (window.innerHeight - 100) + 'px';
            document.body.appendChild(xpGain);
            
            setTimeout(() => {
                document.body.removeChild(xpGain);
            }, 2000);
        }

        function levelUp() {
            gameState.level++;
            gameState.xp = 0;
            gameState.nextLevelXP = Math.floor(gameState.nextLevelXP * 1.5);
            
            addAchievement(`🎉 Level ${gameState.level} Achieved!`);
            createParticles();
        }

        function addAchievement(text) {
            const achievement = document.createElement('div');
            achievement.className = 'achievement';
            achievement.textContent = text;
            document.getElementById('achievementList').appendChild(achievement);
            
            gameState.achievements.push(text);
            
            setTimeout(() => {
                achievement.style.animationDelay = '0s';
            }, 100);
        }

        function createParticles() {
            for (let i = 0; i < 20; i++) {
                setTimeout(() => {
                    const particle = document.createElement('div');
                    particle.className = 'particle';
                    particle.style.left = Math.random() * window.innerWidth + 'px';
                    particle.style.top = Math.random() * window.innerHeight + 'px';
                    document.body.appendChild(particle);
                    
                    setTimeout(() => {
                        document.body.removeChild(particle);
                    }, 2000);
                }, i * 50);
            }
        }

        function unlockSkill(skillName) {
            if (!gameState.unlockedSkills.includes(skillName)) {
                gameState.unlockedSkills.push(skillName);
                gainXP(25);
                addAchievement(`🔓 Unlocked ${skillName}!`);
                
                // Visual feedback
                event.target.classList.add('unlocked');
            }
        }

        function moduleDemo(moduleName) {
            const demos = {
                arp: "ARP Spoofing redirects network traffic through your machine by poisoning ARP tables.",
                dns: "DNS Spoofing redirects domain queries to IP addresses you specify.",
                sniff: "Packet Sniffing captures and analyzes network traffic in real-time.",
                https: "HTTPS Proxy intercepts and potentially decrypts SSL/TLS traffic."
            };
            
            alert(`🎯 ${moduleName.toUpperCase()} MODULE\n\n${demos[moduleName]}\n\nGained 15 XP for exploring!`);
            gainXP(15);
            unlockSkill(moduleName);
        }

        function installStep(step) {
            if (step === gameState.installStep + 1) {
                gameState.installStep++;
                gainXP(20);
                
                const button = event.target;
                button.style.background = 'linear-gradient(45deg, #27ae60, #2ecc71)';
                button.textContent += ' ✅';
                button.disabled = true;
                
                if (gameState.installStep === 4) {
                    addAchievement('🎉 Installation Complete!');
                    setTimeout(() => {
                        alert('🎊 Congratulations! You\'ve successfully installed Bettercap!\n\n+50 Bonus XP!');
                        gainXP(50);
                    }, 1000);
                }
            } else {
                alert('❌ Wrong order! Follow the installation steps sequentially.');
                createShakeEffect(event.target);
            }
        }

        function createShakeEffect(element) {
            element.style.animation = 'shake 0.5s ease-in-out';
            setTimeout(() => {
                element.style.animation = '';
            }, 500);
        }

        function simulateCommand() {
            const terminal = document.getElementById('terminalSim');
            const commands = [
                'bettercap > Scanning network...',
                'bettercap > Found 5 active hosts',
                'bettercap > 192.168.1.1    router.local',
                'bettercap > 192.168.1.100  smartphone.local',
                'bettercap > 192.168.1.101  laptop.local',
                'bettercap > Network scan complete!'
            ];
            
            terminal.innerHTML = '';
            
            commands.forEach((cmd, index) => {
                setTimeout(() => {
                    const line = document.createElement('div');
                    line.className = 'terminal-line';
                    line.textContent = cmd;
                    terminal.appendChild(line);
                    
                    if (index === commands.length - 1) {
                        gainXP(30);
                        addAchievement('🖥️ Terminal Master!');
                    }
                }, index * 800);
            });
        }

        function acceptDisclaimer() {
            event.target.textContent = 'Disclaimer Accepted ✅';
            event.target.disabled = true;
            event.target.style.background = 'linear-gradient(45deg, #27ae60, #2ecc71)';
            gainXP(10);
            addAchievement('📋 Ethical Hacker Pledge');
        }

        function openModal(modalId) {
            document.getElementById(modalId).style.display = 'block';
            gainXP(5);
        }

        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }

        function updateUI() {
            document.getElementById('level').textContent = gameState.level;
            document.getElementById('xp').textContent = gameState.xp;
            document.getElementById('nextLevelXP').textContent = gameState.nextLevelXP;
            
            const progressPercent = (gameState.xp / gameState.nextLevelXP) * 100;
            document.getElementById('progressFill').style.width = progressPercent + '%';
            
            // Update skill nodes
            gameState.unlockedSkills.forEach(skill => {
                const skillNodes = document.querySelectorAll('.skill-node');
                skillNodes.forEach(node => {
                    if (node.textContent.toLowerCase().includes(skill)) {
                        node.classList.add('unlocked');
                    }
                });
            });
        }

        function saveProgress() {
            localStorage.setItem('bettercapProgress', JSON.stringify(gameState));
        }

        function resetProgress() {
            if (confirm('Are you sure you want to reset all progress? This cannot be undone!')) {
                localStorage.removeItem('bettercapProgress');
                location.reload();
            }
        }

        // Easter eggs and special effects
        let clickCount = 0;
        document.addEventListener('click', function(e) {
            clickCount++;
            if (clickCount % 50 === 0) {
                createEasterEgg();
            }
        });

        function createEasterEgg() {
            const eggs = ['🥚', '🐰', '🎯', '💎', '⚡', '🔥', '🌟'];
            const egg = document.createElement('div');
            egg.className = 'easter-egg';
            egg.textContent = eggs[Math.floor(Math.random() * eggs.length)];
            egg.style.left = Math.random() * (window.innerWidth - 50) + 'px';
            egg.style.top = Math.random() * (window.innerHeight - 50) + 'px';
            
            egg.onclick = function() {
                gainXP(100);
                addAchievement('🥚 Easter Egg Found!');
                document.body.removeChild(egg);
                createParticles();
            };
            
            document.body.appendChild(egg);
            
            setTimeout(() => {
                if (document.body.contains(egg)) {
                    document.body.removeChild(egg);
                }
            }, 5000);
        }

        // Keyboard shortcuts
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey && e.shiftKey && e.key === 'X') {
                gainXP(1000);
                addAchievement('⌨️ Keyboard Ninja!');
            }
            
            if (e.key === 'Escape') {
                document.querySelectorAll('.modal').forEach(modal => {
                    modal.style.display = 'none';
                });
            }
        });

        // Add CSS for shake animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes shake {
                0% { transform: translateX(0); }
                25% { transform: translateX(-5px); }
                50% { transform: translateX(5px); }
                75% { transform: translateX(-5px); }
                100% { transform: translateX(0); }
            }
        `;
        document.head.appendChild(style);

        // Initialize tooltips and final setup
        window.addEventListener('load', function() {
            updateUI();
            
            // Add random floating elements
            setInterval(() => {
                if (Math.random() > 0.95) {
                    createFloatingIcon();
                }
            }, 2000);
        });

        function createFloatingIcon() {
            const icons = ['🔐', '🌐', '📡', '⚡', '🔍', '🛡️'];
            const icon = document.createElement('div');
            icon.textContent = icons[Math.floor(Math.random() * icons.length)];
            icon.style.position = 'fixed';
            icon.style.left = Math.random() * window.innerWidth + 'px';
            icon.style.top = window.innerHeight + 'px';
            icon.style.fontSize = '2em';
            icon.style.zIndex = '998';
            icon.style.animation = 'floatUp 10s linear forwards';
            icon.style.opacity = '0.3';
            
            document.body.appendChild(icon);
            
            setTimeout(() => {
                if (document.body.contains(icon)) {
                    document.body.removeChild(icon);
                }
            }, 10000);
        }

        // Add floating animation
        const floatStyle = document.createElement('style');
        floatStyle.textContent = `
            @keyframes floatUp {
                from {
                    transform: translateY(0);
                    opacity: 0.3;
                }
                to {
                    transform: translateY(-${window.innerHeight + 100}px);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(floatStyle);

        // Close modals when clicking outside
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.style.display = 'none';
            }
        };

        // Responsive canvas
        window.addEventListener('resize', function() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // Achievement system trigger
        setTimeout(() => {
            if (gameState.achievements.length === 0) {
                addAchievement('🎮 Welcome to the Game!');
            }
        }, 2000);

        // Progress tracking
        let scrollProgress = 0;
        window.addEventListener('scroll', function() {
            const totalHeight = document.body.scrollHeight - window.innerHeight;
            const currentProgress = (window.scrollY / totalHeight) * 100;
            
            if (currentProgress > scrollProgress + 20) {
                scrollProgress = currentProgress;
                gainXP(5);
                
                if (scrollProgress > 80 && !gameState.achievements.includes('📜 Guide Explorer!')) {
                    addAchievement('📜 Guide Explorer!');
                }
            }
        });
    </script>
</body>
</html>
