<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surat Rahasia</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Dancing+Script:wght@700&display=swap" rel="stylesheet">
    <style>
        *{ margin:0; padding:0; box-sizing:border-box; }
        body{ background: linear-gradient(135deg,#e9d5ff,#fce7f3); height:100vh; overflow:hidden; display:flex; justify-content:center; align-items:center; font-family:'Poppins',sans-serif; }
        .container{ text-align:center; }
        .hidden{ display:none; }
        .password-box{ background:white; padding:30px; border-radius:25px; box-shadow:0 10px 30px rgba(0,0,0,0.15); width:320px; }
        .password-box h2{ margin-bottom:20px; color:#8b5cf6; }
        .display{ height:50px; border-radius:12px; background:#f3e8ff; margin-bottom:20px; font-size:28px; display:flex; align-items:center; justify-content:center; letter-spacing:8px; }
        .keypad{ display:grid; grid-template-columns:repeat(3,1fr); gap:10px; }
        .key{ padding:18px; border:none; border-radius:15px; background:#c084fc; color:white; font-size:20px; cursor:pointer; transition:0.2s; }
        .key:hover{ transform:scale(1.05); background:#a855f7; }
        .gift-scene{ position:relative; }
        .gift-box{ width:220px; height:220px; background:#d8b4fe; margin:auto; position:relative; border-radius:20px; cursor:pointer; animation:float 2s ease-in-out infinite; box-shadow:0 10px 25px rgba(0,0,0,0.15); }
        .ribbon-v{ position:absolute; width:40px; height:220px; background:#ef4444; left:90px; }
        .ribbon-h{ position:absolute; width:220px; height:40px; background:#ef4444; top:90px; }
        .bow{ position:absolute; width:90px; height:90px; background:#dc2626; border-radius:50%; top:-35px; left:65px; }
        .bow::before, .bow::after{ content:''; position:absolute; width:60px; height:60px; background:#ef4444; border-radius:50%; top:15px; }
        .bow::before{ left:-30px; }
        .bow::after{ right:-30px; }
        @keyframes float{ 0%{transform:translateY(0);} 50%{transform:translateY(-10px);} 100%{transform:translateY(0);} }
        .heart{ position:absolute; color:pink; font-size:28px; animation:up 4s linear infinite; }
        @keyframes up{ 0%{ transform:translateY(0) scale(1); opacity:1; } 100%{ transform:translateY(-500px) scale(1.5); opacity:0; } }
        .letter{ background:white; width:380px; padding:35px; border-radius:25px; box-shadow:0 10px 30px rgba(0,0,0,0.2); position:relative; }
        .letter h1{ font-family:'Dancing Script',cursive; color:#a855f7; margin-bottom:20px; font-size:42px; }
        .typing{ font-size:20px; color:#444; min-height:120px; line-height:1.8; }
        .cursor{ display:inline-block; width:3px; background:#333; margin-left:3px; animation:blink .6s infinite; }
        @keyframes blink{ 0%,100%{opacity:1;} 50%{opacity:0;} }
        .rose{ font-size:45px; position:absolute; animation:spin 4s linear infinite; }
        .rose1{ left:-30px; top:20px; }
        .rose2{ right:-30px; bottom:20px; }
        @keyframes spin{ from{transform:rotate(0);} to{transform:rotate(360deg);} }
    </style>
</head>
<body>
    <audio autoplay loop>
        <source src="https://files.catbox.moe/8kq2kd.mp3" type="audio/mpeg">
    </audio>
    <div class="container">
        <div class="password-box" id="passwordPage">
            <h2>Masukkan Password 💜</h2>
            <div class="display" id="display"></div>
            <div class="keypad">
                <button class="key">1</button>
                <button class="key">2</button>
                <button class="key">3</button>
                <button class="key">4</button>
                <button class="key">5</button>
                <button class="key">6</button>
                <button class="key">7</button>
                <button class="key">8</button>
                <button class="key">9</button>
                <button class="key">0</button>
                <button class="key" id="clear">⌫</button>
                <button class="key" id="enter">OK</button>
            </div>
        </div>
        <div class="gift-scene hidden" id="giftPage">
            <div class="gift-box" id="gift">
                <div class="ribbon-v"></div>
                <div class="ribbon-h"></div>
                <div class="bow"></div>
            </div>
            <div class="heart" style="left:20%">❤️</div>
            <div class="heart" style="left:40%; animation-delay:1s;">💖</div>
            <div class="heart" style="left:60%; animation-delay:2s;">💕</div>
            <div class="heart" style="left:80%; animation-delay:3s;">💗</div>
        </div>
        <div class="letter hidden" id="letterPage">
            <div class="rose rose1">🌹</div>
            <div class="rose rose2">🌹</div>
            <h1>Untuk Kamu 💌</h1>
            <div class="typing">
                <span id="text"></span><span class="cursor"></span>
            </div>
        </div>
    </div>
    <script>
        const PASSWORD = "2003";
        let input = "";
        const display = document.getElementById("display");
        document.querySelectorAll(".key").forEach(btn=>{
            btn.addEventListener("click",()=>{
                const value = btn.innerText;
                if(value === "⌫"){
                    input = input.slice(0,-1);
                } else if(value === "OK"){
                    if(input === PASSWORD){
                        document.getElementById("passwordPage").classList.add("hidden");
                        document.getElementById("giftPage").classList.remove("hidden");
                    }else{
                        alert("Password salah 💔");
                        input = "";
                    }
                } else{
                    if(input.length < 6){
                        input += value;
                    }
                }
                display.innerText = "*".repeat(input.length);
            });
        });
        document.getElementById("gift").addEventListener("click",()=>{
            document.getElementById("giftPage").
