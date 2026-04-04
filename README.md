

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Richard Jabastin | Elite Cyber Ops</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;500;600;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: #000;
            color: #00ff41;
            font-family: 'Rajdhani', monospace;
            overflow-x: hidden;
            cursor: crosshair;
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
        
        .scanlines {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(
                0deg,
                transparent,
                transparent 2px,
                rgba(0, 255, 65, 0.03) 2px,
                rgba(0, 255, 65, 0.03) 4px
            );
            pointer-events: none;
            z-index: 1;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 10;
        }
        
        .header {
            text-align: center;
            margin-bottom: 60px;
        }
        
        .name {
            font-family: 'Orbitron', monospace;
            font-size: clamp(3rem, 8vw, 6rem);
            font-weight: 900;
            background: linear-gradient(45deg, #00ff41, #00bfff, #ff00ff, #ffff00);
            background-size: 400% 400%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: glitch 2s infinite, gradientShift 3s ease infinite;
            text-shadow: 0 0 20px #00ff41;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-family: 'Orbitron', monospace;
            font-size: clamp(1.2rem, 3vw, 2rem);
            font-weight: 700;
            color: #00bfff;
            text-shadow: 0 0 15px #00bfff;
            animation: pulse 2s infinite;
        }
        
        .status-bar {
            background: rgba(0, 0, 0, 0.8);
            border: 1px solid #00ff41;
            padding: 15px 25px;
            margin: 30px 0;
            border-radius: 0;
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.3);
            position: relative;
            overflow: hidden;
        }
        
        .status-bar::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 65, 0.2), transparent);
            animation: scan 3s infinite;
        }
        
        .status-text {
            font-family: 'Orbitron', monospace;
            font-size: 1.1rem;
            letter-spacing: 2px;
        }
        
        .section {
            margin: 50px 0;
        }
        
        .section-title {
            font-family: 'Orbitron', monospace;
            font-size: 1.8rem;
            font-weight: 700;
            color: #ff00ff;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin-bottom: 25px;
            position: relative;
            display: inline-block;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 3px;
            background: linear-gradient(90deg, #ff00ff, #00ff41);
            animation: underline 2s 1s forwards;
        }
        
        .tech-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(60px, 1fr));
            gap: 20px;
            padding: 30px;
            background: rgba(0, 0, 0, 0.6);
            border: 2px solid #00ff41;
            border-radius: 0;
            position: relative;
        }
        
        .tech-item {
            text-align: center;
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
        }
        
        .tech-item:hover {
            transform: scale(1.2) rotate(5deg);
            filter: drop-shadow(0 0 20px #00ff41);
        }
        
        .tech-item:hover img {
            filter: brightness(1.5) drop-shadow(0 0 15px #00ff41);
            animation: bounce 0.6s infinite;
        }
        
        .tech-item img {
            width: 50px;
            height: 50px;
            transition: all 0.3s ease;
            filter: saturate(0.7) brightness(1.2);
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 40px 0;
        }
        
        .social-btn {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 15px 30px;
            background: rgba(0, 255, 65, 0.1);
            border: 2px solid #00ff41;
            color: #00ff41;
            text-decoration: none;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 2px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .social-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 65, 0.3), transparent);
            transition: left 0.5s;
        }
        
        .social-btn:hover::before {
            left: 100%;
        }
        
        .social-btn:hover {
            background: rgba(0, 255, 65, 0.2);
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.6);
            transform: translateY(-3px);
        }
        
        .typing {
            border-right: 3px solid #00ff41;
            animation: blink 1s infinite;
        }
        
        @keyframes glitch {
            0%, 100% { transform: translate(0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(-2px, -2px); }
            60% { transform: translate(2px, 2px); }
            80% { transform: translate(2px, -2px); }
        }
        
        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        
        @keyframes scan {
            0% { left: -100%; }
            100% { left: 100%; }
        }
        
        @keyframes underline {
            to { width: 100%; }
        }
        
        @keyframes blink {
            0%, 50% { border-color: #00ff41; }
            51%, 100% { border-color: transparent; }
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .glitch-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 100;
            opacity: 0;
        }
        
        @media (max-width: 768px) {
            .tech-grid {
                grid-template-columns: repeat(auto-fit, minmax(50px, 1fr));
                gap: 15px;
            }
            
            .social-links {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <canvas class="matrix-bg" id="matrix"></canvas>
    <div class="scanlines"></div>
    
    <div class="container">
        <div class="header">
            <h1 class="name" id="hackerName">RICHARD JABASTIN</h1>
            <h3 class="subtitle">ELITE CYBERSECURITY | ETHICAL HACKER | DIGITAL WARRIOR</h3>
        </div>
        
        <div class="status-bar">
            <div class="status-text">
                <span class="typing" id="status">INITIALIZING HACKER PROFILE... </span>
                <span id="counter">00:00</span>
            </div>
        </div>
        
        <div class="section">
            <h3 class="section-title">BREACH ACCESS</h3>
            <div class="social-links">
                <a href="https://instagram.com/jd.h4x" target="_blank" class="social-btn">
                    <img src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="Instagram" width="30" height="30">
                    JD.H4X
                </a>
            </div>
        </div>
        
        <div class="section">
            <h3 class="section-title">WEAPONIZED STACK</h3>
            <div class="tech-grid">
                <!-- Core Cybersecurity Tools -->
                <a href="#" class="tech-item" title="Kali Linux"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" alt="linux"></a>
                <a href="#" class="tech-item" title="Metasploit"><img src="https://www.vectorlogo.zone/logos/metasploit/metasploit-icon.svg" alt="metasploit"></a>
                <a href="#" class="tech-item" title="Burp Suite"><img src="https://www.vectorlogo.zone/logos/portswigger/portswigger-icon.svg" alt="burp"></a>
                <a href="#" class="tech-item" title="Wireshark"><img src="https://www.vectorlogo.zone/logos/wireshark/wireshark-icon.svg" alt="wireshark"></a>
                <a href="#" class="tech-item" title="Nmap"><img src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTE5IDFMNSAxNEw5IDlMMTMgMTNMMjAgMTBaIiBmaWxsPSIjRkZGRkZGIi8+Cjwvc3ZnPgo=" alt="nmap"></a>
                
                <!-- Programming Arsenal -->
                <a href="#" class="tech-item" title="Python"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python"></a>
                <a href="#" class="tech-item" title="Bash"><img src="https://www.vectorlogo.zone/logos/gnu_bash/gnu_bash-icon.svg" alt="bash"></a>
                <a href="#" class="tech-item" title="JavaScript"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript"></a>
                <a href="#" class="tech-item" title="Go"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/go/go-original.svg" alt="go"></a>
                <a href="#" class="tech-item" title="Rust"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/rust/rust-plain.svg" alt="rust"></a>
                
                <!-- Cloud & Infra -->
                <a href="#" class="tech-item" title="AWS"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" alt="aws"></a>
                <a href="#" class="tech-item" title="Docker"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker"></a>
                <a href="#" class="tech-item" title="Kubernetes"><img src="https://www.vectorlogo.zone/logos/kubernetes/kubernetes-icon.svg" alt="kubernetes"></a>
                
                <!-- DevOps & Monitoring -->
                <a href="#" class="tech-item" title="Jenkins"><img src="https://www.vectorlogo.zone/logos/jenkins/jenkins-icon.svg" alt="jenkins"></a>
                <a href="#" class="tech-item" title="Grafana"><img src="https://www.vectorlogo.zone/logos/grafana/grafana-icon.svg" alt="grafana"></a>
                
                <!-- Mobile & Web -->
                <a href="#" class="tech-item" title="Android"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/android/android-original-wordmark.svg" alt="android"></a>
                <a href="#" class="tech-item" title="React"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg" alt="react"></a>
            </div>
        </div>
    </div>

    <script>
        // Matrix rain effect
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const matrix = "ABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@#$%^&*()*&^%+-/~{[|`]}";
        const matrixArray = matrix.split("");
        
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);
        
        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.04)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = '#00ff41';
            ctx.font = fontSize + 'px monospace';
            
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
        
        // Dynamic typing effect
        const statusText = document.getElementById('status');
        const messages = [
            "INITIALIZING HACKER PROFILE...",
            "SCANNING NETWORK INTERFACES...",
            "LOADING EXPLOIT MODULES...",
            "DECRYPTING PAYLOADS...",
            "PROFILE ONLINE | READY FOR BREACH",
            "RICHARD JABASTIN | ELITE OPS ACTIVE"
        ];
        
        let messageIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        
        function typeStatus() {
            const currentMessage = messages[messageIndex];
            
            if (isDeleting) {
                statusText.textContent = currentMessage.substring(0, charIndex - 1);
                charIndex--;
            } else {
                statusText.textContent = currentMessage.substring(0, charIndex + 1);
                charIndex++;
            }
            
            let typeSpeed = isDeleting ? 50 : 100;
            
            if (!isDeleting && charIndex === currentMessage.length) {
                typeSpeed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                messageIndex = (messageIndex + 1) % messages.length;
                typeSpeed = 500;
            }
            
            setTimeout(typeStatus, typeSpeed);
        }
        
        typeStatus();
        
        // Counter
        let seconds = 0;
        setInterval(() => {
            seconds++;
            const mins = Math.floor(seconds / 60);
            const secs = seconds % 60;
            document.getElementById('counter').textContent = 
                `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }, 1000);
        
        // Responsive canvas
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
        
        // Glitch effect on hover
        document.querySelectorAll('.tech-item').forEach(item => {
            item.addEventListener('mouseenter', function() {
                this.style.animation = 'glitch 0.3s infinite';
            });
            item.addEventListener('mouseleave', function() {
                this.style.animation = '';
            });
        });
    </script>
</body>
</html>
