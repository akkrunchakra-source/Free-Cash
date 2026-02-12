<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Free-Cash - Earn & Recharge</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;padding-bottom:80px}

/* Signup */
#signup{background:#000;color:#fff;padding:20px;min-height:100vh}
#signup input{width:100%;padding:14px;margin:8px 0;background:#222;border:none;border-radius:8px;color:#fff}
.signup-btn{padding:16px;background:red;border:none;border-radius:30px;color:#fff;font-weight:bold}

/* Wallet */
#withdraw{display:none}
.header{background:#ffd700;padding:12px;text-align:center}
.balance{font-size:24px;font-weight:bold}

/* Tabs */
.tabs{display:flex;border-bottom:1px solid #ddd}
.tab{flex:1;text-align:center;padding:12px;font-weight:bold;cursor:pointer}
.tab.active{border-bottom:3px solid #ffd700}
.tab-content{padding:10px}
.hidden{display:none}

input,select{width:100%;padding:12px;margin:8px 0;border-radius:6px;border:1px solid #ccc}

/* Plans */
.amount-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.amount-btn{padding:14px;border:1px solid #ddd;border-radius:8px;text-align:center;font-weight:bold}
.amount-btn.selected{border:2px solid #2ecc71;background:#eafaf1}

/* Buttons */
.withdraw-btn{background:#ffd700;padding:14px;text-align:center;font-weight:bold;border-radius:8px;margin-top:10px}

/* Transaction */
.transaction-section{margin-top:15px;background:#f9f9f9;border-radius:12px;overflow:hidden}
.transaction-header{background:#333;color:#fff;padding:12px;text-align:center;cursor:pointer}
.transaction-list{display:none;max-height:250px;overflow:auto}
.transaction-item{padding:10px;border-bottom:1px solid #eee;font-size:14px}

/* Live Recharge */
.live-box{margin:15px;border-radius:12px;overflow:hidden}
.live-header{background:linear-gradient(90deg,#ff0080,#ff8c00,#40e0d0);color:#fff;padding:10px;text-align:center}
.live-list{height:140px;background:#000;overflow:hidden}
.live-list ul{list-style:none;padding:0;margin:0;animation:scroll 6s linear infinite}
.live-list li{
padding:8px 12px;
border-bottom:1px solid #222;
animation:colorChange 2s infinite alternate;
}

@keyframes colorChange{
0%{color:#00ff9d;}
25%{color:#ff4d4d;}
50%{color:#ffd700;}
75%{color:#40e0d0;}
100%{color:#ff00ff;}
}
@keyframes scroll{
0%{transform:translateY(100%)}
100%{transform:translateY(-100%)}
}

/* INSTALL SECTION */
.install-box{
text-align:center;
padding:20px;
background:#111;
}

.install-text{
font-weight:bold;
color:#fff;
font-size:16px;
margin-bottom:15px;
}

.install-btn{
padding:14px 30px;
font-size:16px;
font-weight:bold;
border:none;
border-radius:30px;
background:linear-gradient(45deg,#00ff9d,#00c3ff);
color:#000;
cursor:pointer;
animation:pulse 1.2s infinite;
}

@keyframes pulse{
0%{transform:scale(1);}
50%{transform:scale(1.08);}
100%{transform:scale(1);}
}

/* Bottom Nav */
.bottom-nav{position:fixed;bottom:0;left:0;right:0;height:70px;display:flex;background:#111}
.nav-item{flex:1;text-align:center;color:#fff;padding:12px;font-weight:bold}

button{padding:10px 20px;border:none;border-radius:20px;font-weight:bold}
</style>
</head>

<body>

<!-- Signup -->
<div id="signup">
<h2>Free Mobile Recharge & Cash Earn</h2>
<input placeholder="+91 Mobile">
<input placeholder="Password">
<input placeholder="Enter OTP">
<input placeholder="Referral Code">
<button class="signup-btn" onclick="showSignupPopup()">Signup</button>
</div>

<!-- Wallet -->
<div id="withdraw">
<div class="header">
<div>Wallet Balance</div>
<div class="balance">₹180.00</div>
</div>

<!-- Live Recharge -->
<div class="live-box">
<div class="live-header">LIVE Recharge</div>
<div class="live-list">
<ul>
<li>+91 98****4321 recharged ₹19</li>
<li>+91 87****1123 recharged ₹29</li>
<li>+91 76****9988 recharged ₹69</li>
</ul>
</div>
</div>

<!-- INSTALL BUTTON (Live List ke niche center me) -->
<div class="install-box">
<p class="install-text">
⚡ Apna task complete kare niche Install button par click karke  
aur wapas isi site par aaye ⚡
</p>

<a href="https://6gain.com/in/#/?rcode=Pcpb6h" target="_blank">
<button class="install-btn">INSTALL & COMPLETE TASK</button>
</a>
</div>

</div>

<!-- Bottom Nav -->
<div class="bottom-nav">
<div class="nav-item">Home</div>
<div class="nav-item">Earn</div>
<div class="nav-item">Watch</div>
<div class="nav-item">Data</div>
</div>

<script>
function showSignupPopup(){
document.getElementById("signup").style.display="none";
document.getElementById("withdraw").style.display="block";
}
</script>

</body>
</html>
