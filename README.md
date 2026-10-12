# bull_tap
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bull Earn Mini App</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: #0d0d0d;
            color: #ffffff;
            display: flex;
            flex-direction: column;
            height: 100vh;
            justify-content: space-between;
        }

        /* --- HEADER --- */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 16px;
            background-color: #141414;
            border-bottom: 1px solid #222;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ef4444, #b91c1c);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .user-details .username {
            font-weight: bold;
            font-size: 0.95rem;
        }

        .user-details .status {
            font-size: 0.75rem;
            color: #22c55e;
        }

        .balance-box {
            text-align: right;
        }

        .balance-label {
            font-size: 0.7rem;
            color: #a1a1aa;
            text-transform: uppercase;
        }

        .balance-amount {
            font-size: 1.1rem;
            font-weight: bold;
            color: #f59e0b;
        }

        /* --- CONTENT CONTAINER --- */
        .content {
            flex: 1;
            overflow-y: auto;
            padding: 16px;
        }

        .tab-page {
            display: none;
        }

        .tab-page.active {
            display: block;
        }

        /* --- CARDS & PANELS --- */
        .card {
            background-color: #1a1a1a;
            border: 1px solid #2a2a2a;
            border-radius: 14px;
            padding: 16px;
            margin-bottom: 14px;
        }

        .card-title {
            font-size: 0.85rem;
            font-weight: bold;
            color: #a1a1aa;
            text-transform: uppercase;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* --- CHECKLIST ITEMS --- */
        .check-item {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
            font-size: 0.9rem;
        }

        .check-icon {
            width: 18px;
            height: 18px;
            border-radius: 4px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75rem;
        }

        .check-icon.done {
            background-color: #22c55e;
            color: #000;
        }

        .check-icon.pending {
            background-color: #333;
            border: 1px solid #555;
        }

        /* --- BUTTONS --- */
        .btn-primary {
            width: 100%;
            background: linear-gradient(135deg, #ef4444, #dc2626);
            border: none;
            color: #ffffff;
            font-weight: bold;
            padding: 14px;
            border-radius: 12px;
            font-size: 1rem;
            cursor: pointer;
            margin-top: 10px;
            box-shadow: 0 4px 12px rgba(239, 68, 68, 0.3);
        }

        .btn-primary:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            box-shadow: none;
        }

        /* --- LINKS COMUNIDAD --- */
        .link-btn {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #222222;
            border: 1px solid #333333;
            color: #ffffff;
            text-decoration: none;
            padding: 12px 16px;
            border-radius: 10px;
            margin-bottom: 8px;
            font-size: 0.9rem;
            transition: background 0.2s;
        }

        .link-btn:active {
            background-color: #333333;
            border-color: #f59e0b;
        }

        /* --- BOTTOM NAVIGATION --- */
        .nav-bar {
            display: flex;
            justify-content: space-around;
            align-items: center;
            background-color: #141414;
            border-top: 1px solid #222;
            padding: 8px 0;
            position: relative;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #71717a;
            font-size: 0.75rem;
            text-decoration: none;
            cursor: pointer;
            width: 20%;
        }

        .nav-item.active {
            color: #ef4444;
        }

        .nav-icon {
            font-size: 1.2rem;
            margin-bottom: 2px;
        }

        .nav-item.center-btn .nav-icon-bg {
            background: linear-gradient(135deg, #ef4444, #b91c1c);
            color: #fff;
            width: 48px;
            height: 48px;
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: -15px;
            box-shadow: 0 4px 12px rgba(239, 68, 68, 0.4);
        }

        .nav-item.center-btn.active .nav-icon-bg {
            box-shadow: 0 4px 18px rgba(239, 68, 68, 0.7);
        }
    </style>
</head>
<body>

    <!-- HEADER TOP -->
    <div class="header">
        <div class="user-info">
            <div class="avatar">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M2 5C4 7 7 8 12 8C17 8 20 7 22 5C21 11 18 14 12 16C6 14 3 11 2 5Z" fill="#fbbf24"/>
                    <path d="M4 12L2 18L7 16L12 19L17 16L22 18L20 12" stroke="#fef3c7" stroke-width="1.5" stroke-linejoin="round"/>
                    <circle cx="9" cy="11" r="1.5" fill="#000"/>
                    <circle cx="15" cy="11" r="1.5" fill="#000"/>
                    <path d="M10 14H14" stroke="#000" stroke-width="1.5" stroke-linecap="round"/>
                </svg>
            </div>
            <div class="user-details">
                <div class="username" id="userHandle">@Usuario</div>
                <div class="status">● Online</div>
            </div>
        </div>
        <div class="balance-box">
            <div class="balance-label">BALANCE</div>
            <div class="balance-amount"><span id="tokenBalance">11,562</span> BULL</div>
        </div>
    </div>

    <!-- MAIN CONTENT AREA -->
    <div class="content">

        <!-- TAB 1: HOME -->
        <div id="tab-home" class="tab-page">
            <div class="card">
                <div class="card-title">⛏️ Minado Pasivo</div>
                <p style="font-size: 0.9rem; color: #ccc;">Gana 100 BULL por hora de forma automática.</p>
                <button class="btn-primary" onclick="claimMining()">Reclamar Minado</button>
            </div>
            
            <div class="card">
                <div class="card-title">📢 COMUNIDAD Y CANALES</div>
                <a href="https://t.me/TuCanalOficial" target="_blank" class="link-btn">
                    <span>📢 Canal de Novedades</span>
                    <span>➔</span>
                </a>
                <a href="https://t.me/TuCanalDePagos" target="_blank" class="link-btn">
                    <span>💳 Canal de Pruebas de Pago</span>
                    <span>➔</span>
                </a>
            </div>
        </div>

        <!-- TAB 2: TASKS -->
        <div id="tab-tasks" class="tab-page">
            <div class="card">
                <div class="card-title">📋 Anuncios Diarios</div>
                <p style="font-size: 0.9rem; color: #ccc; margin-bottom: 10px;">Mira anuncios para desbloquear tus retiros.</p>
                <div class="check-item">
                    <div class="check-icon pending" id="adStatusIcon">⏳</div>
                    <span>Anuncios vistos hoy: <b id="adsWatchedCount">0</b> / 15</span>
                </div>
                <button class="btn-primary" onclick="watchAdsgramAd()">📺 Ver Anuncio (+50 BULL)</button>
            </div>
        </div>

        <!-- TAB 3: EARN (BOTÓN PRINCIPAL) -->
        <div id="tab-earn" class="tab-page active">
            <div class="card" style="text-align: center; padding: 30px 10px;">
                <h2>🐂 Bull Tap Game</h2>
                <p style="color: #aaa; margin: 10px 0 20px 0;">¡Toca la cara del Toro y acumula tokens!</p>
                
                <button class="btn-primary" style="width: 150px; height: 150px; border-radius: 50%; margin: 0 auto; display: flex; align-items: center; justify-content: center; background: linear-gradient(135deg, #f59e0b, #d97706); border: 4px solid #fbbf24;" onclick="tapCoin()">
                    <svg width="85" height="85" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M2 4C4 7 7 9 12 9C17 9 20 7 22 4C21 11 18 15 12 17C6 15 3 11 2 4Z" fill="#1f2937"/>
                        <path d="M4 12L1 19L7 17L12 20L17 17L23 19L20 12" stroke="#fbbf24" stroke-width="1.5" stroke-linejoin="round"/>
                        <circle cx="9" cy="11" r="1.5" fill="#ef4444"/>
                        <circle cx="15" cy="11" r="1.5" fill="#ef4444"/>
                        <path d="M9 14.5C10 15.5 14 15.5 15 14.5" stroke="#fbbf24" stroke-width="1.5" stroke-linecap="round"/>
                    </svg>
                </button>
            </div>
        </div>

        <!-- TAB 4: REFER -->
        <div id="tab-refer" class="tab-page">
            <div class="card">
                <div class="card-title">🔗 Tu Enlace de Invitación</div>
                <input type="text" readonly value="https://t.me/TuBot?start=123456" style="width:100%; padding: 10px; background:#111; border:1px solid #333; color:#fff; border-radius:8px; margin-bottom: 10px;">
                <button class="btn-primary" onclick="copyLink()">Copiar Enlace</button>
            </div>
        </div>

        <!-- TAB 5: PROFILE & WITHDRAW -->
        <div id="tab-profile" class="tab-page">
            <div class="card">
                <div class="card-title">📋 REQUISITOS DE RETIRO</div>
                
                <div class="check-item">
                    <div class="check-icon done">✓</div>
                    <span>Dirección de Wallet configurada</span>
                </div>
                <div class="check-item">
                    <div class="check-icon done">✓</div>
                    <span>Mínimo 10,000 BULL</span>
                </div>
                <div class="check-item">
                    <div class="check-icon pending" id="reqAdCheck">✗</div>
                    <span>Ver 15 anuncios hoy (<span id="reqAdsVal">0</span>/15)</span>
                </div>
                <div class="check-item">
                    <div class="check-icon done">✓</div>
                    <span>2 Referidos válidos</span>
                </div>

                <button class="btn-primary" id="withdrawBtn" disabled onclick="processWithdrawal()">
                    🔒 Completa los requisitos para retirar
                </button>
            </div>

            <div class="card">
                <div class="card-title">🧮 Conversor</div>
                <p style="font-size: 0.9rem; color: #aaa;">100,000 BULL = <b>$1.00 USDT</b></p>
            </div>
        </div>

    </div>

    <!-- BOTTOM NAVIGATION BAR -->
    <div class="nav-bar">
        <div class="nav-item" onclick="switchTab('home', this)">
            <div class="nav-icon">🏠</div>
            <span>Home</span>
        </div>
        <div class="nav-item" onclick="switchTab('tasks', this)">
            <div class="nav-icon">☑️</div>
            <span>Tasks</span>
        </div>
        <div class="nav-item center-btn active" onclick="switchTab('earn', this)">
            <div class="nav-icon-bg">
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M2 4C4 7 7 9 12 9C17 9 20 7 22 4C21 11 18 15 12 17C6 15 3 11 2 4Z" fill="#fbbf24"/>
                </svg>
            </div>
            <span style="margin-top: 4px;">Earn</span>
        </div>
        <div class="nav-item" onclick="switchTab('refer', this)">
            <div class="nav-icon">👥</div>
            <span>Refer</span>
        </div>
        <div class="nav-item" onclick="switchTab('profile', this)">
            <div class="nav-icon">👤</div>
            <span>Profile</span>
        </div>
    </div>

    <script>
        let balance = 11562;
        let adsWatched = 0;

        function switchTab(tabId, element) {
            document.querySelectorAll('.tab-page').forEach(page => page.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));

            document.getElementById('tab-' + tabId).classList.add('active');
            element.classList.add('active');
        }

        function tapCoin() {
            balance += 1;
            updateUI();
        }

        function watchAdsgramAd() {
            alert("[Simulación Adsgram] Viendo anuncio de 15 segundos...");
            adsWatched += 1;
            balance += 50;
            updateUI();
        }

        function claimMining() {
            balance += 100;
            alert("¡Has reclamado 100 BULL del minado!");
            updateUI();
        }

        function updateUI() {
            document.getElementById('tokenBalance').innerText = balance.toLocaleString();
            document.getElementById('adsWatchedCount').innerText = adsWatched;
            document.getElementById('reqAdsVal').innerText = adsWatched;

            if (adsWatched >= 15) {
                const reqAdCheck = document.getElementById('reqAdCheck');
                reqAdCheck.classList.remove('pending');
                reqAdCheck.classList.add('done');
                reqAdCheck.innerText = '✓';

                const withdrawBtn = document.getElementById('withdrawBtn');
                withdrawBtn.disabled = false;
                withdrawBtn.innerText = '💸 Solicitar Retiro';
            }
        }

        function processWithdrawal() {
            alert("¡Solicitud de retiro enviada con éxito!");
        }

        function copyLink() {
            alert("Enlace copiado al portapapeles.");
        }
    </script>
</body>
</html>