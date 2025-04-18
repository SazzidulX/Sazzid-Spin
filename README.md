<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sazzid Spin - Earn Real Money</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            color: #333;
            text-align: center;
        }
        header {
            background: linear-gradient(to right, #ff4b2b, #ff416c);
            color: white;
            padding: 2rem;
        }
        header h1 {
            margin: 0;
            font-size: 2.5rem;
        }
        .container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }
        .wallet {
            margin: 1rem 0;
            font-size: 1.2rem;
        }
        .wallet span {
            font-weight: bold;
            color: #ff4b2b;
        }
        .spinner-container {
            margin: 2rem 0;
            position: relative;
        }
        #wheel {
            width: 300px;
            height: 300px;
            border-radius: 50%;
            background: conic-gradient(
                #f44336 0% 14.28%,
                #2196f3 14.28% 28.56%,
                #4caf50 28.56% 42.84%,
                #ffeb3b 42.84% 57.12%,
                #9c27b0 57.12% 71.4%,
                #ff9800 71.4% 85.68%,
                #00bcd4 85.68% 100%
            );
            position: relative;
            transition: transform 3s ease-out;
            margin: 0 auto;
        }
        #wheel::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            background: white;
            border-radius: 50%;
            transform: translate(-50%, -50%);
        }
        #pointer {
            position: absolute;
            top: 0;
            left: 50%;
            width: 0;
            height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-top: 20px solid black;
            transform: translateX(-50%);
        }
        #spin-btn, .btn {
            background: #ff4b2b;
            color: white;
            border: none;
            padding: 1rem 2rem;
            font-size: 1.2rem;
            cursor: pointer;
            border-radius: 5px;
            margin-top: 1rem;
        }
        #spin-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
        }
        #result {
            margin-top: 1rem;
            font-size: 1.5rem;
            color: #ff4b2b;
        }
        .actions {
            margin-top: 2rem;
        }
        .actions button, .actions a {
            margin: 0.5rem;
            text-decoration: none;
            display: inline-block;
        }
        footer {
            background: #333;
            color: white;
            padding: 1rem;
            position: relative;
            bottom: 0;
            width: 100%;
        }
        #admin-login, #admin-panel {
            margin: 2rem auto;
            max-width: 400px;
            padding: 1rem;
            background: white;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        #admin-login input, #admin-login button {
            padding: 0.5rem;
            margin: 0.5rem;
            width: calc(100% - 1rem);
        }
        @media (max-width: 600px) {
            #wheel {
                width: 250px;
                height: 250px;
            }
            header h1 {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Sazzid Spin</h1>
        <p>Spin the wheel, earn real cash, and withdraw instantly!</p>
    </header>
    <div class="container">
        <div class="wallet">Your Balance: ₹<span id="wallet-balance">0.00</span></div>
        <h2>Spin to Win!</h2>
        <div class="spinner-container">
            <div id="wheel">
                <div id="pointer"></div>
            </div>
            <button id="spin-btn">Spin Now</button>
            <div id="result">Spin to see your reward!</div>
        </div>
        <p>10 free spins daily | Rewards: ₹0.01 to ₹10 | 10-second cooldown</p>
        <div class="actions">
            <button class="btn" onclick="withdrawMoney()">Withdraw Money</button>
            <button class="btn" onclick="referFriend()">Refer & Earn</button>
            <a href="https://t.me/SazzidSpin" class="btn" target="_blank">Join Telegram</a>
        </div>
        <div id="admin-login">
            <h3>Admin Login</h3>
            <input type="password" id="admin-password" placeholder="Enter password">
            <button onclick="loginAdmin()">Login</button>
        </div>
        <div id="admin-panel" style="display: none;">
            <h3>Admin Panel</h3>
            <p>Current Balance: ₹<span id="admin-balance">0.00</span></p>
            <button onclick="resetBalance()">Reset Balance</button>
            <button onclick="logoutAdmin()">Logout</button>
        </div>
    </div>
    <footer>
        <p>© 2025 Sazzid Spin. All rights reserved.</p>
        <p>Contact: support@sazzidspin.com | <a href="https://t.me/SazzidSpin" style="color: #ff4b2b;">Join our Telegram Channel</a></p>
        <!-- Ad Code -->
        <script type="text/javascript">
            atOptions = {
                'key': '78eb2a14604ca5d5446c50ea2b9f5852',
                'format': 'iframe',
                'height': 50,
                'width': 320,
                'params': {}
            };
        </script>
        <script type="text/javascript" src="//www.highperformanceformat.com/78eb2a14604ca5d5446c50ea2b9f5852/invoke.js"></script>
    </footer>

    <script>
        const rewards = [0.01, 0.05, 0.1, 0.5, 1, 5, 10];
        const wheel = document.getElementById('wheel');
        const spinBtn = document.getElementById('spin-btn');
        const result = document.getElementById('result');
        const walletBalance = document.getElementById('wallet-balance');
        const adminBalance = document.getElementById('admin-balance');
        const adminLogin = document.getElementById('admin-login');
        const adminPanel = document.getElementById('admin-panel');
        let isSpinning = false;
        let balance = 0.00;

        spinBtn.addEventListener('click', () => {
            if (isSpinning) return;
            isSpinning = true;
            spinBtn.disabled = true;

            const randomSpin = Math.floor(Math.random() * 360) + 1800;
            wheel.style.transform = `rotate(${randomSpin}deg)`;

            setTimeout(() => {
                const rewardIndex = Math.floor(((randomSpin % 360) / 360) * rewards.length);
                const reward = rewards[rewardIndex];
                balance += reward;
                walletBalance.textContent = balance.toFixed(2);
                adminBalance.textContent = balance.toFixed(2);
                result.textContent = `You won ₹${reward.toFixed(2)}!`;

                setTimeout(() => {
                    isSpinning = false;
                    spinBtn.disabled = false;
                }, 10000);
            }, 3000);
        });

        function withdrawMoney() {
            if (balance >= 10) {
                const upiId = prompt("Enter your UPI ID:");
                if (upiId) {
                    alert(`Withdrawal request for ₹${balance.toFixed(2)} with UPI ID: ${upiId} submitted! Please send this request to our Telegram channel: https://t.me/SazzidSpin`);
                    balance = 0;
                    walletBalance.textContent = balance.toFixed(2);
                    adminBalance.textContent = balance.toFixed(2);
                } else {
                    alert("UPI ID is required to proceed with withdrawal.");
                }
            } else {
                alert('Minimum ₹10 required to withdraw.');
            }
        }

        function referFriend() {
            const code = Math.random().toString(36).substring(2, 8).toUpperCase();
            alert(`Your referral code is: ${code}`);
        }

        function loginAdmin() {
            const password = document.getElementById('admin-password').value;
            if (password === 'Sazzidul@190') {
                adminLogin.style.display = 'none';
                adminPanel.style.display = 'block';
                adminBalance.textContent = balance.toFixed(2);
            } else {
                alert('Incorrect password!');
            }
        }

        function resetBalance() {
            balance = 0;
            walletBalance.textContent = balance.toFixed(2);
            adminBalance.textContent = balance.toFixed(2);
            alert('Balance reset to ₹0.00');
        }

        function logoutAdmin() {
            adminPanel.style.display = 'none';
            adminLogin.style.display = 'block';
            document.getElementById('admin-password').value = '';
        }
    </script>
</body>
</html>
