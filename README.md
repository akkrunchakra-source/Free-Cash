<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free Cash</title>

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#000;
}

/* ---------- SIGNUP PAGE ---------- */
#signup{
    min-height:100vh;
    background:#000;
    color:#fff;
    padding:20px;
}
.signup-box{
    margin-top:40px;
}
.signup-box h2{
    font-size:22px;
    margin-bottom:20px;
}
.signup-box input{
    width:100%;
    padding:14px;
    margin:10px 0;
    background:#222;
    border:none;
    border-radius:8px;
    color:#fff;
}
.signup-btn{
    width:100%;
    padding:16px;
    margin-top:20px;
    background:#2b2b2b;
    color:#fff;
    border:none;
    border-radius:30px;
    font-size:16px;
    cursor:pointer;
}
.agree{
    margin-top:20px;
    font-size:13px;
    color:#aaa;
}
.agree span{
    color:red;
}

/* ---------- WITHDRAW PAGE ---------- */
#withdraw{
    display:none;
    background:#fff;
    color:#000;
    min-height:100vh;
}
.header{
    background:#ffd700;
    padding:12px;
    text-align:center;
    position:relative;
}
.balance{
    font-size:24px;
    font-weight:bold;
}
.notification{
    padding:10px;
    text-align:center;
    color:#ff8c00;
}
.tabs{
    display:flex;
    justify-content:space-around;
    border-bottom:1px solid #ddd;
}
.tab{
    padding:10px;
    cursor:pointer;
    font-weight:bold;
}
.tab.active{
    border-bottom:2px solid #ffd700;
}
.tab-content{
    padding:15px;
}
.hidden{display:none;}
.account-input, select{
    width:100%;
    padding:10px;
    margin:10px 0;
}
.amount-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:10px;
}
.amount-btn{
    padding:10px;
    border:1px solid #ddd;
    text-align:center;
}
.withdraw-btn{
    background:#ffd700;
    padding:15px;
    text-align:center;
    font-weight:bold;
    margin-top:15px;
}
.bottom-nav{
    display:flex;
    justify-content:space-around;
    border-top:1px solid #ddd;
    padding:10px;
    font-size:12px;
}
</style>
</head>

<body>

<!-- ================= SIGNUP SCREEN ================= -->
<div id="signup">
    <div class="signup-box">
        <h2>कमाना शुरू करने के लिए<br>अपना account बनाओ!</h2>

        <input type="tel" placeholder="+91 Phone">
        <input type="password" placeholder="Password डालो">
        <input type="text" placeholder="Invitation Code">
        <input type="text" placeholder="Verify Code">

        <button class="signup-btn" onclick="goWithdraw()">Account बनाओ</button>

        <div class="agree">
            ● मैं agree करता हूँ <span>Terms of Service</span> and <span>Privacy Policy</span>
        </div>
    </div>
</div>

<!-- ================= WITHDRAW SCREEN ================= -->
<div id="withdraw">

    <div class="header">
        <div>Withdraw</div>
        <div class="balance">₹517.32</div>
        <div>Earning cash</div>
    </div>

    <div class="notification">🔔 रोज ₹20 से लेकर ₹1000 निकाल सकते हैं</div>

    <div class="tabs">
        <div class="tab active" onclick="openTab('paytm',this)">Paytm</div>
        <div class="tab" onclick="openTab('bank',this)">BANK</div>
        <div class="tab" onclick="openTab('recharge',this)">MOBILE Recharge</div>
    </div>

    <div id="paytm" class="tab-content">
        <input class="account-input" value="335258xxx05">
        <div class="amount-grid">
            <div class="amount-btn">₹10</div>
            <div class="amount-btn">₹20</div>
            <div class="amount-btn">₹50</div>
            <div class="amount-btn">₹100</div>
            <div class="amount-btn">₹500</div>
            <div class="amount-btn">₹2000</div>
        </div>
        <div class="withdraw-btn">पैसा निकालें</div>
    </div>

    <div id="bank" class="tab-content hidden">
        <input class="account-input" placeholder="Bank Account">
        <div class="withdraw-btn">पैसा निकालें</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input class="account-input" placeholder="Mobile Number">
        <select>
            <option>Jio</option>
            <option>Airtel</option>
            <option>Vodafone</option>
        </select>
        <div class="withdraw-btn">Recharge Now</div>
    </div>

    <div class="bottom-nav">
        <div>Play</div>
        <div>Daily</div>
        <div>NEW</div>
        <div>Free Earn</div>
        <div>₹ Wallet</div>
    </div>
</div>

<script>
function goWithdraw(){
    document.getElementById("signup").style.display="none";
    document.getElementById("withdraw").style.display="block";
}

function openTab(id,el){
    document.querySelectorAll(".tab-content").forEach(t=>t.classList.add("hidden"));
    document.getElementById(id).classList.remove("hidden");

    document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
    el.classList.add("active");
}
</script>

</body>
</html>
