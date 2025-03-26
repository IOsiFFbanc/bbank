<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Кликер-Терминал | ЯжРубь Банк</title>
    <style>
        :root {
            --primary: #005b82;
            --secondary: #e6f2f7;
            --accent: #ff7e00;
            --text: #333333;
            --light: #ffffff;
        }
        
        body {
            font-family: 'Roboto', Arial, sans-serif;
            background-color: #f5f9fc;
            margin: 0;
            padding: 0;
            color: var(--text);
            min-height: 100vh;
        }
        
        .bank-header {
            background-color: var(--primary);
            color: var(--light);
            padding: 15px 0;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: relative;
        }
        
        .bank-header h1 {
            margin: 0;
            font-size: 24px;
            font-weight: 500;
        }
        
        .bank-header p {
            margin: 5px 0 0;
            font-size: 14px;
            opacity: 0.9;
        }
        
        .settings-btn {
            position: absolute;
            top: 15px;
            right: 20px;
            background: none;
            border: none;
            color: var(--light);
            font-size: 20px;
            cursor: pointer;
            transition: transform 0.3s;
            padding: 5px;
        }
        
        .settings-btn:hover {
            transform: rotate(30deg);
        }
        
        .main-container {
            max-width: 600px;
            margin: 30px auto;
            padding: 0 20px;
        }
        
        .account-card {
            background: linear-gradient(135deg, var(--primary), #0088cc);
            color: var(--light);
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 5px 15px rgba(0,91,130,0.2);
            position: relative;
            overflow: hidden;
        }
        
        .account-card::after {
            content: "";
            position: absolute;
            top: -50px;
            right: -50px;
            width: 200px;
            height: 200px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
        }
        
        .account-title {
            font-size: 16px;
            margin-bottom: 5px;
            opacity: 0.9;
        }
        
        .account-balance {
            font-size: 36px;
            font-weight: 700;
            margin: 10px 0;
            letter-spacing: 1px;
        }
        
        .account-number {
            font-size: 14px;
            opacity: 0.8;
            font-family: monospace;
        }
        
        .clicker-button {
            width: 100%;
            padding: 25px;
            background-color: var(--accent);
            color: var(--light);
            border: none;
            border-radius: 10px;
            font-size: 22px;
            font-weight: bold;
            cursor: pointer;
            margin: 20px 0;
            box-shadow: 0 5px 0 #cc6600;
            transition: all 0.1s;
        }
        
        .clicker-button:active {
            transform: translateY(3px);
            box-shadow: 0 2px 0 #cc6600;
        }
        
        .upgrades-section {
            margin-top: 40px;
        }
        
        .section-title {
            color: var(--primary);
            font-size: 18px;
            font-weight: 500;
            margin-bottom: 15px;
            padding-bottom: 5px;
            border-bottom: 2px solid var(--secondary);
        }
        
        .upgrade-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
            gap: 15px;
        }
        
        .upgrade-card {
            background-color: var(--light);
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            transition: all 0.3s;
        }
        
        .upgrade-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .upgrade-name {
            font-weight: 500;
            margin-bottom: 5px;
            color: var(--primary);
        }
        
        .upgrade-multiplier {
            font-size: 12px;
            color: var(--accent);
            font-weight: bold;
        }
        
        .upgrade-price {
            margin: 10px 0;
            font-weight: bold;
        }
        
        .buy-button {
            width: 100%;
            padding: 8px;
            background-color: var(--primary);
            color: var(--light);
            border: none;
            border-radius: 5px;
            font-size: 14px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .buy-button:hover {
            background-color: #004466;
        }
        
        .buy-button:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        
        .bank-navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 40px;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .nav-button {
            padding: 12px 25px;
            background-color: var(--primary);
            color: var(--light);
            border: none;
            border-radius: 30px;
            font-size: 16px;
            cursor: pointer;
            text-decoration: none;
            text-align: center;
            transition: all 0.3s;
            flex: 1;
            min-width: 120px;
        }
        
        .nav-button:hover {
            background-color: #004466;
        }
        
        .income-rate {
            font-size: 14px;
            color: #27ae60;
            margin-top: 5px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <header class="bank-header">
        <button class="settings-btn" id="settingsBtn">⚙️</button>
        <h1>ЯжРубь Банк</h1>
        <p>Кликер-Терминал для увеличения капитала</p>
    </header>
    
    <div class="main-container">
        <div class="account-card">
            <div class="account-title">Текущий баланс</div>
            <div class="account-balance" id="balance">0 ₽</div>
            <div class="income-rate" id="incomeRate">+0 ₽/сек | +0 ₽/клик | x1</div>
            <div class="account-number">Клиент #CLK-<span id="clientId">0001</span></div>
        </div>
        
        <button class="clicker-button" id="clickBtn">ПОЛУЧИТЬ ДОХОД</button>
        
        <div class="upgrades-section">
            <h2 class="section-title">Инвестиционные пакеты</h2>
            <div class="upgrade-grid">
                <div class="upgrade-card">
                    <div class="upgrade-name">Стартовый</div>
                    <div class="upgrade-multiplier">+1 ₽ за клик</div>
                    <div class="upgrade-price">10 ₽</div>
                    <button class="buy-button" data-multiplier="1" data-cost="10">Приобрести</button>
                </div>
                
                <div class="upgrade-card">
                    <div class="upgrade-name">Стандарт</div>
                    <div class="upgrade-multiplier">+2 ₽ за клик</div>
                    <div class="upgrade-price">50 ₽</div>
                    <button class="buy-button" data-multiplier="2" data-cost="50">Приобрести</button>
                </div>
                
                <div class="upgrade-card">
                    <div class="upgrade-name">Премиум</div>
                    <div class="upgrade-multiplier">+5 ₽ за клик</div>
                    <div class="upgrade-price">100 ₽</div>
                    <button class="buy-button" data-multiplier="5" data-cost="100">Приобрести</button>
                </div>
                
                <div class="upgrade-card">
                    <div class="upgrade-name">VIP</div>
                    <div class="upgrade-multiplier">+10 ₽ за клик</div>
                    <div class="upgrade-price">500 ₽</div>
                    <button class="buy-button" data-multiplier="10" data-cost="500">Приобрести</button>
                </div>
            </div>
        </div>
        
        <div class="bank-navigation">
            <a href="market.html" class="nav-button">Биржа ценных бумаг</a>
            <a href="inventory.html" class="nav-button">Мой портфель</a>
            <a href="kripto.html" class="nav-button">Криптотрейдинг</a>
        </div>
    </div>

    <script>
        // Элементы
        const balanceDisplay = document.getElementById('balance');
        const clickBtn = document.getElementById('clickBtn');
        const buyButtons = document.querySelectorAll('.buy-button');
        const clientIdDisplay = document.getElementById('clientId');
        const settingsBtn = document.getElementById('settingsBtn');
        const incomeRateDisplay = document.getElementById('incomeRate');
        
        // Игровые данные
        let gameState = {
            balance: localStorage.getItem('clickerBalance') ? parseFloat(localStorage.getItem('clickerBalance')) : 0,
            multiplier: localStorage.getItem('clickerMultiplier') ? parseInt(localStorage.getItem('clickerMultiplier')) : 1,
            upgrades: localStorage.getItem('clickerUpgrades') ? JSON.parse(localStorage.getItem('clickerUpgrades')) : [],
            passiveIncome: localStorage.getItem('passiveIncome') ? parseFloat(localStorage.getItem('passiveIncome')) : 0,
            clickBonus: localStorage.getItem('clickBonus') ? parseInt(localStorage.getItem('clickBonus')) : 0,
            incomeMultiplier: localStorage.getItem('incomeMultiplier') ? parseInt(localStorage.getItem('incomeMultiplier')) : 1
        };
        
        // Генерация ID клиента
        function generateClientId() {
            const id = Math.floor(1000 + Math.random() * 9000);
            clientIdDisplay.textContent = id;
            localStorage.setItem('clientId', id.toString());
            return id;
        }
        
        // Обновление интерфейса
        function updateUI() {
            balanceDisplay.textContent = gameState.balance.toLocaleString('ru-RU') + ' ₽';
            incomeRateDisplay.textContent = 
                `+${gameState.passiveIncome.toFixed(1)} ₽/сек | ` +
                `+${(gameState.multiplier + gameState.clickBonus) * gameState.incomeMultiplier} ₽/клик | ` +
                `x${gameState.incomeMultiplier}`;
            
            // Сохраняем баланс для других страниц
            localStorage.setItem('clickerBalance', gameState.balance.toString());
            
            buyButtons.forEach(button => {
                const cost = parseInt(button.dataset.cost);
                const multiplier = parseInt(button.dataset.multiplier);
                
                if (gameState.upgrades.includes(multiplier)) {
                    button.disabled = true;
                    button.textContent = 'Приобретено';
                    button.style.backgroundColor = '#27ae60';
                } else {
                    button.disabled = gameState.balance < cost;
                }
            });
        }
        
        // Сохранить игру
        function saveGame() {
            localStorage.setItem('clickerBalance', gameState.balance.toString());
            localStorage.setItem('clickerMultiplier', gameState.multiplier.toString());
            localStorage.setItem('clickerUpgrades', JSON.stringify(gameState.upgrades));
        }
        
        // Обработчики событий
        clickBtn.addEventListener('click', () => {
            const clickIncome = (gameState.multiplier + gameState.clickBonus) * gameState.incomeMultiplier;
            gameState.balance += clickIncome;
            saveGame();
            updateUI();
        });
        
        buyButtons.forEach(button => {
            button.addEventListener('click', function() {
                const cost = parseInt(this.dataset.cost);
                const multiplier = parseInt(this.dataset.multiplier);
                
                if (gameState.balance >= cost && !gameState.upgrades.includes(multiplier)) {
                    gameState.balance -= cost;
                    gameState.multiplier += multiplier;
                    gameState.upgrades.push(multiplier);
                    
                    saveGame();
                    updateUI();
                }
            });
        });
        
        // Пассивный доход
        function updatePassiveIncome() {
            if (gameState.passiveIncome > 0) {
                gameState.balance += gameState.passiveIncome;
                saveGame();
                updateUI();
            }
        }
        
        // Проверка обновлений из других вкладок
        function checkForUpdates() {
            // Проверяем баланс
            const newBalance = localStorage.getItem('clickerBalance') ? parseFloat(localStorage.getItem('clickerBalance')) : 0;
            if (newBalance !== gameState.balance) {
                gameState.balance = newBalance;
                updateUI();
            }
            
            // Проверяем доходы из market.html
            const newPassiveIncome = localStorage.getItem('passiveIncome') ? parseFloat(localStorage.getItem('passiveIncome')) : 0;
            const newClickBonus = localStorage.getItem('clickBonus') ? parseInt(localStorage.getItem('clickBonus')) : 0;
            const newIncomeMultiplier = localStorage.getItem('incomeMultiplier') ? parseInt(localStorage.getItem('incomeMultiplier')) : 1;
            
            if (newPassiveIncome !== gameState.passiveIncome || 
                newClickBonus !== gameState.clickBonus || 
                newIncomeMultiplier !== gameState.incomeMultiplier) {
                gameState.passiveIncome = newPassiveIncome;
                gameState.clickBonus = newClickBonus;
                gameState.incomeMultiplier = newIncomeMultiplier;
                updateUI();
            }
        }
        
        // Переход на страницу настроек
        settingsBtn.addEventListener('click', () => {
            window.location.href = 'Nas.html';
        });
        
        // Инициализация
        if (!localStorage.getItem('clientId')) {
            generateClientId();
        } else {
            clientIdDisplay.textContent = localStorage.getItem('clientId');
        }
        
        // Запускаем таймеры
        setInterval(updatePassiveIncome, 1000);
        setInterval(checkForUpdates, 1000);
        
        // Первоначальная загрузка
        updateUI();
        
        // Обработчик сообщений между вкладками
        window.addEventListener('storage', function(event) {
            if (event.key === 'clickerBalance') {
                gameState.balance = parseFloat(event.newValue) || 0;
                updateUI();
            }
            if (event.key === 'passiveIncome' || event.key === 'clickBonus' || event.key === 'incomeMultiplier') {
                checkForUpdates();
            }
        });
    </script>
</body>
</html>
