<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Withdraw Demo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #fff;
            color: #000;
        }
        .header {
            background-color: #ffd700;
            padding: 10px;
            text-align: center;
            position: relative;
        }
        .back-arrow {
            position: absolute;
            left: 10px;
            top: 15px;
            font-size: 20px;
        }
        .balance {
            font-size: 24px;
            font-weight: bold;
        }
        .earning-cash {
            font-size: 12px;
        }
        .my-withdrawal {
            position: absolute;
            right: 10px;
            top: 20px;
            font-size: 14px;
            color: blue;
        }
        .notification {
            background-color: #fff;
            padding: 10px;
            text-align: center;
            font-size: 14px;
            color: #ff8c00;
        }
        .bell-icon {
            color: #ff8c00;
        }
        .tabs {
            display: flex;
            justify-content: space-around;
            background-color: #fff;
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }
        .tab {
            cursor: pointer;
            padding: 10px;
            font-weight: bold;
        }
        .tab.active {
            border-bottom: 2px solid #ffd700;
        }
        .tab-content {
            padding: 20px;
        }
        .hidden {
            display: none;
        }
        .edit {
            color: green;
            font-size: 12px;
        }
        .account-input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
        }
        .amount-label {
            font-size: 16px;
            margin: 10px 0;
        }
        .amount-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
        }
        .amount-btn {
            background-color: #f5f5f5;
            padding: 10px;
            text-align: center;
            border: 1px solid #ddd;
            cursor: pointer;
        }
        .note {
            font-size: 12px;
            color: #666;
            margin: 20px 0;
        }
        .withdraw-btn {
            background-color: #ffd700;
            color: #000;
            padding: 15px;
            text-align: center;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
        }
        .bottom-nav {
            display: flex;
            justify-content: space-around;
            background-color: #fff;
            padding: 10px;
            border-top: 1px solid #ddd;
            position: fixed;
            bottom: 0;
            width: 100%;
        }
        .nav-item {
            text-align: center;
            font-size: 12px;
        }
        .select-operator {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
        }
        #confirm-page {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #fff;
            z-index: 10;
            padding: 20px;
            text-align: center;
        }
        #confirm-page .header {
            background-color: #ffd700;
            padding: 10px;
        }
        .confirm-text {
            margin: 20px 0;
            font-size: 16px;
        }
        .confirm-btn {
            background-color: #ffd700;
            color: #000;
            padding: 15px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 20px;
        }
        #success-page {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #fff;
            z-index: 11;
            padding: 20px;
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        .success-animation {
            font-size: 24px;
            font-weight: bold;
            color: #ff0000; /* Starting color */
            animation: color-change 2s infinite;
        }
        @keyframes color-change {
            0% { color: #ff0000; }
            25% { color: #00ff00; }
            50% { color: #0000ff; }
            75% { color: #ffff00; }
            100% { color: #ff0000; }
        }
        .back-btn {
            background-color: #ffd700;
            color: #000;
            padding: 15px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="header">
        <div class="back-arrow">&lt;</div>
        <div>Withdraw</div>
        <div class="balance">₹517.32</div>
        <div class="earning-cash">Earning cash</div>
        <div class="my-withdrawal">My Withdrawal</div>
    </div>
    <div class="notification">
        <span class="bell-icon">🔔</span> रोज ₹20 से लेकर ₹1000 निकाल सकते हैं
    </div>
    <div class="tabs">
        <div class="tab active" onclick="openTab('paytm')">Paytm</div>
        <div class="tab" onclick="openTab('bank')">BANK</div>
        <div class="tab" onclick="openTab('recharge')">MOBILE Recharge</div>
    </div>
    <div id="paytm" class="tab-content">
        <div class="edit">• Edit</div>
        <div>मेरा अकाउंट नंबर</div>
        <input type="text" class="account-input" value="335258xxx05">
        <div class="amount-label">राशि</div>
        <div class="amount-grid">
            <div class="amount-btn">₹199</div>
            <div class="amount-btn">₹399</div>
            <div class="amount-btn">₹99</div>
            <div class="amount-btn">₹20</div>
            <div class="amount-btn">₹299</div>
        </div>
        <div class="note">अपना पैसा 30 मिनट के भीतर आपके अकाउंट में आए दिया जाएगा। कृपया समय पर अकाउंट visa निकालें!</div>
        <div class="withdraw-btn" onclick="alert('Withdrawal Successful!')">पेसा निकालें</div>
    </div>
    <div id="bank" class="tab-content hidden">
        <div class="edit">• Edit</div>
        <div>Bank Account</div>
        <input type="text" class="account-input" placeholder="Enter Bank Details">
        <div class="amount-label">राशि</div>
        <div class="amount-grid">
            <div class="amount-btn">₹199</div>
            <div class="amount-btn">₹399</div>
            <div class="amount-btn">₹99</div>
            <div class="amount-btn">₹20</div>
            <div class="amount-btn">₹299</div>
        </div>
        <div class="note">अपना पैसा 30 मिनट के भीतर आपके अकाउंट में आए दिया जाएगा। कृपया समय पर अकाउंट visa निकालें!</div>
        <div class="withdraw-btn" onclick="alert('Withdrawal Successful!')">पेसा निकालें</div>
    </div>
    <div id="recharge" class="tab-content hidden">
        <div>मोबाइल नंबर</div>
        <input type="text" class="account-input" placeholder="Enter Mobile Number">
        <div>सिम चुनें</div>
        <select class="select-operator">
            <option>Jio</option>
            <option>Airtel</option>
            <option>Vodafone</option>
            <option>BSNL</option>
            <option>Other</option>
        </select>
        <div class="amount-label">राशि</div>
        <div class="amount-grid">
            <div class="amount-btn">₹199</div>
            <div class="amount-btn">₹399</div>
            <div class="amount-btn">₹99</div>
            <div class="amount-btn">₹20</div>
            <div class="amount-btn">₹299</div>
        </div>
        <div class="note">अपना पैसा 30 मिनट के भीतर आपके अकाउंट में आए दिया जाएगा। कृपया समय पर अकाउंट visa निकालें!</div>
        <div class="withdraw-btn" onclick="showConfirmPage()">Recharge Now</div>
    </div>
    <div class="bottom-nav">
        <div class="nav-item">Play</div>
        <div class="nav-item">Daily</div>
        <div class="nav-item">NEW</div>
        <div class="nav-item">Free Earn</div>
        <div class="nav-item">₹ Wallet</div>
        <div class="nav-item">Watch Videos Free Money</div>
    </div>

    <!-- Confirm Page -->
    <div id="confirm-page" class="hidden">
        <div class="header">
            <div>Confirm Recharge</div>
        </div>
        <div class="confirm-text">रिचार्ज करने के लिए कन्फर्म करें Free</div>
        <div class="confirm-btn" onclick="showSuccessPage()">Confirm</div>
    </div>

    <!-- Success Page with Animation -->
    <div id="success-page" class="hidden">
        <div class="success-animation">Your Free Rs.199 Recharge Successfully Activate Within 15 min</div>
        <div class="back-btn" onclick="backToHome()">Back to Home Page</div>
    </div>

    <script>
        function openTab(tabName) {
            var tabs = document.getElementsByClassName('tab-content');
            for (var i = 0; i < tabs.length; i++) {
                tabs[i].classList.add('hidden');
            }
            document.getElementById(tabName).classList.remove('hidden');

            var tabLinks = document.getElementsByClassName('tab');
            for (var i = 0; i < tabLinks.length; i++) {
                tabLinks[i].classList.remove('active');
            }
            event.currentTarget.classList.add('active');
        }

        function showConfirmPage() {
            document.getElementById('confirm-page').classList.remove('hidden');
        }

        function showSuccessPage() {
            document.getElementById('confirm-page').classList.add('hidden');
            document.getElementById('success-page').classList.remove('hidden');
        }

        function backToHome() {
            document.getElementById('success-page').classList.add('hidden');
            // Optionally reset to main page or recharge tab
        }
    </script>
</body>
</html>ementById('success-page').classList.add('hidden');
            // Optionally reset to main page or recharge tab
        }
    </script>
</body>
</html>
