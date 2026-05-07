<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Free Fire Topup Demo</title>

<style>

body{
    margin:0;
    font-family:Arial,sans-serif;
    background:#0f172a;
    color:white;
}

.container{
    max-width:420px;
    margin:auto;
    padding:20px;
}

.title{
    text-align:center;
    font-size:32px;
    font-weight:bold;
    color:#facc15;
    margin-top:20px;
}

.card{
    background:#1e293b;
    padding:20px;
    border-radius:18px;
    margin-top:20px;
    box-shadow:0 0 15px rgba(0,0,0,0.4);
}

label{
    display:block;
    margin-top:10px;
    margin-bottom:6px;
}

input{
    width:100%;
    padding:12px;
    border:none;
    border-radius:10px;
    font-size:16px;
}

.package{
    background:#334155;
    padding:14px;
    border-radius:12px;
    margin-top:12px;
    cursor:pointer;
    transition:0.2s;
    border:2px solid transparent;
}

.package:hover{
    background:#475569;
}

.package.active{
    border:2px solid #facc15;
}

button{
    width:100%;
    padding:14px;
    margin-top:20px;
    border:none;
    border-radius:12px;
    background:#facc15;
    color:black;
    font-size:18px;
    font-weight:bold;
    cursor:pointer;
}

button:hover{
    opacity:0.9;
}

.qr-section{
    text-align:center;
    margin-top:25px;
    display:none;
}

.qr-section img{
    width:240px;
    border-radius:16px;
    background:white;
    padding:10px;
}

.info{
    margin-top:12px;
    color:#cbd5e1;
}

.success{
    background:#065f46;
    padding:14px;
    border-radius:12px;
    margin-top:18px;
    display:none;
}

</style>
</head>

<body>

<div class="container">

    <div class="title">
        FREE FIRE TOPUP
    </div>

    <div class="card">

        <label>UID ผู้เล่น</label>
        <input type="text" id="uid" placeholder="กรอก UID">

        <label>เลือกแพ็กเกจ</label>

        <div class="package" onclick="selectPackage(this,100,35)">
            💎 100 Diamonds - 35 บาท
        </div>

        <div class="package" onclick="selectPackage(this,310,99)">
            💎 310 Diamonds - 99 บาท
        </div>

        <div class="package" onclick="selectPackage(this,520,150)">
            💎 520 Diamonds - 150 บาท
        </div>

        <div class="package" onclick="selectPackage(this,1060,300)">
            💎 1060 Diamonds - 300 บาท
        </div>

        <button onclick="generateQR()">
            สร้าง QR ชำระเงิน
        </button>

        <div class="qr-section" id="qrSection">

            <h2>สแกนเพื่อชำระเงิน</h2>

            <!-- เปลี่ยนลิงก์รูป QR ได้ -->
            <img id="qrImage"
            src="https://api.qrserver.com/v1/create-qr-code/?size=250x250&data=PromptPayDemo">

            <div class="info" id="paymentInfo"></div>

            <button onclick="confirmPayment()">
                แจ้งว่าชำระแล้ว
            </button>

        </div>

        <div class="success" id="successBox"></div>

    </div>

</div>

<script>

let selectedDiamond = 0;
let selectedPrice = 0;

function selectPackage(element,diamond,price){

    selectedDiamond = diamond;
    selectedPrice = price;

    document.querySelectorAll(".package")
    .forEach(p => p.classList.remove("active"));

    element.classList.add("active");
}

function generateQR(){

    let uid = document.getElementById("uid").value;

    if(uid === ""){
        alert("กรุณากรอก UID");
        return;
    }

    if(selectedDiamond === 0){
        alert("กรุณาเลือกแพ็กเกจ");
        return;
    }

    document.getElementById("qrSection").style.display = "block";

    document.getElementById("paymentInfo").innerHTML = `
        UID: ${uid}<br>
        จำนวน: ${selectedDiamond} Diamonds<br>
        ราคา: ${selectedPrice} บาท
    `;
}

function confirmPayment(){

    let uid = document.getElementById("uid").value;

    let successBox = document.getElementById("successBox");

    successBox.style.display = "block";

    successBox.innerHTML = `
        ✅ ระบบได้รับคำสั่งซื้อแล้ว<br><br>

        UID: ${uid}<br>
        Diamonds: ${selectedDiamond}<br>
        ราคา: ${selectedPrice} บาท<br><br>

        สถานะ: รอตรวจสอบสลิป
    `;
}

</script>

</body>
</html>
