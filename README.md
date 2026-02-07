<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free Cash</title>

<style>
*{box-sizing:border-box;}
body{
    margin:0;
    font-family:Arial, sans-serif;
}

/* ========== SIGNUP ========== */
#signup{
    height:100vh;
    background:#000;
    color:#fff;
    padding:20px;
    display:flex;
    flex-direction:column;
    justify-content:center;
}
#signup h2{
    margin-bottom:20px;
}
#signup input{
    width:100%;
    padding:14px;
    margin:10px 0;
    background:#222;
    border:none;
    border-radius:8px;
    color:#fff;
}
.signup-btn{
    margin-top:20px;
    padding:16px;
    background:#2b2b2b;
    border:none;
    border-radius:30px;
    color:#fff;
    font-size:16px;
}
.agree{
    margin-top:15px;
    font-size:12px;
    color:#aaa;
}
.agree span{color:red;}

/* ========== WITHDRAW ========== */
#withdraw{
    display:none;
    height:100vh;
    background:#fff;
    overflow:hidden;
}
.header{
    background:#ffd700;
    padding:12px;
    text-align:center;
}
.balance{font-size:24px;font-weight:bold;}
.notification{
    padding:8px;
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
    font-weight:bold;
}
.tab.active{border-bottom:2px solid #ffd700;}
.tab-content{padding:10px;}
.hidden{display:none;}

input,select{
    width:100%;
    padding:10px;
    margin:8px 0;
}
.amount-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:8px;
}
.amount-btn{
    padding:10px;
    border:1px solid #ddd;
    text-align:center;
}
.withdraw-btn{
    background:#ffd700;
    padding:14px;
    text-align:center;
    font-weight:bold;
    margin-top:10px;
}

/* LIVE LIST */
.live{
    background:#f7f7f7;
    padding:6px;
    font-size:12px;
    height:60px;
    overflow:hidden;
}
.live div{
    animation:scroll 6s linear infinite;
}
@keyframes scroll{
    0%{transform:translateY(100%);}
    100%{transform:translateY(-100%);}
}

/* POPUP */
#popup{
    display:none;
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.6);
    align-items:center;
    justify-content:center;
}
.popup-box{
    background:#fff;
    padding:20px;
    border-radius:10px;
    text-align:center;
}
</style>
</head>

<body>

<!-- SIGNUP -->
<div id="signup">
    <h2>कमाना शुरू करने के लिए<br>अपना account बनाओ!</h2>
    <input placeholder="+91 Phone">
    <input type="password" placeholder="Password डालो">
    <input placeholder="Invitation Code">
    <input placeholder="Verify Code">
    <button class="signup-btn" onclick="goWithdraw()">Account बनाओ</button>
    <div class="agree">● मैं agree करता हूँ <span>Terms of Service</span> and <span>Privacy Policy</span></div>
</div>

<!-- WITHDRAW -->
<div id="withdraw">

    <div class="header">
        <div>Withdraw</div>
        <div class="balance">₹517.32</div>
        <div>Earning cash</div>
    </div>

    <div class="notification">🔔 रोज ₹20 से ₹1000 निकाल सकते हैं</div>

    <div class="live">
        <div>
            Rahul ₹200 withdrawn<br>
            Aman ₹500 withdrawn<br>
            Neha ₹100 withdrawn<br>
            Pooja ₹300 withdrawn
        </div>
    </div>

    <div class="tabs">
        <div class="tab active" onclick="openTab('paytm',this)">Paytm</div>
        <div class="tab" onclick="openTab('bank',this)">BANK</div>
        <div class="tab" onclick="openTab('recharge',this)">MOBILE Recharge</div>
    </div>

    <div id="paytm" class="tab-content">
        <input value="335258xxx05">
        <div class="amount-grid">
            <div class="amount-btn">₹10</div><div class="amount-btn">₹20</div><div class="amount-btn">₹50</div>
            <div class="amount-btn">₹100</div><div class="amount-btn">₹500</div><div class="amount-btn">₹2000</div>
        </div>
        <div class="withdraw-btn">पैसा निकालें</div>
    </div>

    <div id="bank" class="tab-content hidden">
        <input placeholder="Bank Account">
        <div class="withdraw-btn">पैसा निकालें</div>
    </div>

    <div id="recharge" class="tab-content hidden">
        <input placeholder="Mobile Number">
        <select><option>Jio</option><option>Airtel</option></select>
        <div class="withdraw-btn" onclick="showPopup()">Recharge Now</div>
    </div>

</div>

<!-- POPUP -->
<div id="popup">
    <div class="popup-box">
        <b>Your Recharge successfully completed</b><br>
        please wait 10 Mint Only<br>
        Thankyou
    </div>
</div>

<script>
function goWithdraw(){
    signup.style.display="none";
    withdraw.style.display="block";
}
function openTab(id,el){
    document.querySelectorAll(".tab-content").forEach(t=>t.classList.add("hidden"));
    document.getElementById(id).classList.remove("hidden");
    document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
    el.classList.add("active");
}
function showPopup(){
    popup.style.display="flex";
    setTimeout(()=>popup.style.display="none",4000);
}
</script>

</body>
</html>
