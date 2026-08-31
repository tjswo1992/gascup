<html lang="ko">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>가스트론 승부차기 | GAS CUP 2026</title>
<style>
  :root {
    --navy: #071a2f;
    --blue: #00a7e8;
    --cyan: #7fe9ff;
    --lime: #b9f52f;
    --orange: #ff9f1c;
    --white: #f7fbff;
    --panel: rgba(3, 18, 34, .82);
    --line: rgba(255,255,255,.18);
  }
  * { box-sizing: border-box; }
  html, body { margin: 0; min-height: 100%; font-family: Inter, Pretendard, "Noto Sans KR", Arial, sans-serif; background: #03111f; color: var(--white); overflow-x: hidden; }
  body { display: flex; justify-content: center; align-items: center; min-height: 100vh; min-height: 100svh; }
  button { font: inherit; }

  .game-shell {
    width: min(1120px, 100vw);
    min-height: min(760px, 100vh);
    position: relative;
    overflow: hidden;
    background:
      radial-gradient(circle at 50% -10%, rgba(0,167,232,.24), transparent 42%),
      linear-gradient(180deg, #0a263f 0%, #0d3b43 42%, #0a553f 43%, #06412f 100%);
    box-shadow: 0 24px 80px rgba(0,0,0,.6);
  }

  .game-shell::before {
    content: "";
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(255,255,255,.025) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,.025) 1px, transparent 1px);
    background-size: 34px 34px;
    pointer-events: none;
  }

  .topbar {
    height: 92px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px 24px;
    position: relative;
    z-index: 10;
    border-bottom: 1px solid var(--line);
    background: linear-gradient(180deg, rgba(3,18,34,.96), rgba(3,18,34,.65));
    backdrop-filter: blur(12px);
  }
  .brand { display: flex; align-items: center; gap: 14px; }
  .brand-logo-wrap {
    display:flex; align-items:center; justify-content:center;
    width: 210px; height: 52px; padding: 6px 12px;
    border-radius: 16px;
    background: linear-gradient(135deg, rgba(255,255,255,.95), rgba(245,250,255,.86));
    box-shadow: 0 0 0 1px rgba(255,255,255,.16), 0 10px 30px rgba(0,167,232,.18);
  }
  .brand-logo { display:block; max-width:100%; max-height:100%; object-fit:contain; }
  .brand-meta strong { display: block; letter-spacing: .08em; font-size: 20px; }
  .brand-meta span { color: var(--cyan); font-size: 12px; letter-spacing: .24em; font-weight: 800; }

  .score-card {
    display: flex; align-items: center; gap: 14px;
    background: rgba(0,0,0,.24);
    border: 1px solid var(--line);
    border-radius: 18px;
    padding: 10px 14px;
  }
  .score-label { font-size: 12px; color: #a9c3d9; font-weight: 800; letter-spacing: .08em; }
  .shots { display: flex; gap: 8px; }
  .shot-dot {
    width: 24px; height: 24px; border-radius: 50%;
    border: 2px solid rgba(255,255,255,.4);
    display: grid; place-items: center;
    font-size: 14px; font-weight: 1000;
    background: rgba(255,255,255,.05);
    transition: .25s ease;
  }
  .shot-dot.goal { background: var(--lime); color: #153500; border-color: var(--lime); box-shadow: 0 0 18px rgba(185,245,47,.55); }
  .shot-dot.miss { background: #ff435f; border-color: #ff435f; box-shadow: 0 0 18px rgba(255,67,95,.5); }

  .arena {
    position: relative;
    height: calc(min(760px, 100vh) - 92px);
    min-height: 620px;
    overflow: hidden;
  }
  .stadium-lights { position:absolute; inset:0; pointer-events:none; opacity:.62; }
  .beam { position:absolute; top:-30px; width:180px; height:520px; filter: blur(4px); background: linear-gradient(180deg, rgba(255,255,255,.28), rgba(255,255,255,0)); transform-origin: top; }
  .beam.b1{ left:8%; transform:rotate(-16deg); } .beam.b2{ right:8%; transform:rotate(16deg); }

  .banner {
    position: absolute; top: 22px; left: 50%; transform: translateX(-50%);
    width: min(92%, 860px); height: 48px;
    border: 1px solid rgba(127,233,255,.35);
    background: linear-gradient(90deg, rgba(0,167,232,.12), rgba(7,26,47,.8), rgba(0,167,232,.12));
    clip-path: polygon(2% 0, 98% 0, 100% 50%, 98% 100%, 2% 100%, 0 50%);
    display: flex; align-items: center; justify-content: center;
    font-weight: 950; letter-spacing: .18em;
    color: #ddf8ff;
    text-shadow: 0 0 16px rgba(127,233,255,.5);
  }

  .goal-wrap {
    position: absolute;
    left: 50%; top: 100px;
    transform: translateX(-50%);
    width: min(84vw, 760px);
    aspect-ratio: 2.25 / 1;
  }
  .goal {
    position: absolute; inset: 0;
    border: 10px solid #f4fbff;
    border-bottom-width: 12px;
    border-radius: 5px 5px 0 0;
    background:
      linear-gradient(rgba(255,255,255,.20) 1.5px, transparent 1.5px),
      linear-gradient(90deg, rgba(255,255,255,.20) 1.5px, transparent 1.5px),
      linear-gradient(180deg, rgba(37,103,133,.22), rgba(5,32,45,.45));
    background-size: 34px 34px;
    box-shadow: inset 0 0 45px rgba(0,0,0,.35), 0 12px 50px rgba(0,0,0,.35);
    cursor: crosshair;
    overflow: hidden;
    touch-action: none;
  }
  .goal::after {
    content: "GOAL ZONE";
    position:absolute; left:50%; top:50%; transform:translate(-50%,-50%);
    letter-spacing:.45em; font-weight:900; color:rgba(255,255,255,.055); font-size:clamp(20px,4vw,42px); white-space:nowrap;
  }
  .post-glow { position:absolute; inset:-10px; pointer-events:none; box-shadow: 0 0 34px rgba(255,255,255,.36); }


  .keeper {
    --x: 50%; --y: 57%; --rot: 0deg;
    position: absolute;
    left: var(--x); top: var(--y);
    transform: translate(-50%, -50%) rotate(var(--rot));
    width: 154px; height: 194px;
    z-index: 5;
    transition: left .26s cubic-bezier(.15,.82,.18,1), top .26s cubic-bezier(.15,.82,.18,1), transform .26s cubic-bezier(.15,.82,.18,1);
    pointer-events: none;
    filter: drop-shadow(0 14px 14px rgba(0,0,0,.38));
  }
  .keeper .shadow {
    position:absolute; left:50%; bottom:4px; transform:translateX(-50%);
    width:92px; height:16px; border-radius:50%;
    background:rgba(2,12,22,.34); filter:blur(4px);
  }
  .keeper .helmet {
    position:absolute; left:42px; top:0;
    width:68px; height:34px;
    border-radius:30px 30px 18px 18px;
    background:linear-gradient(180deg,#ffffff,#e7eaef 68%, #d2d7de 100%);
    border:3px solid #c5cbd4;
    box-shadow:inset 0 5px 0 rgba(255,255,255,.75), 0 2px 0 rgba(0,0,0,.08);
  }
  .keeper .helmet::before {
    content:""; position:absolute; left:28px; top:-6px; width:12px; height:18px;
    border-radius:8px 8px 4px 4px; background:linear-gradient(180deg,#eef2f6,#d4dbe2);
    border:2px solid #c5cbd4; border-bottom:0;
  }
  .keeper .helmet::after {
    content:""; position:absolute; left:-4px; right:-4px; bottom:-6px; height:9px;
    border-radius:12px; background:linear-gradient(180deg,#ffffff,#d8dde5);
    border:2px solid #c5cbd4;
  }
  .keeper .head {
    position:absolute; left:48px; top:28px; width:56px; height:50px;
    border-radius:18px 18px 20px 20px;
    background:linear-gradient(180deg,#f8d1b5,#edb88d 100%);
    border:3px solid rgba(0,0,0,.06);
    box-shadow: inset 0 2px 0 rgba(255,255,255,.32);
  }
  .keeper .eye-box {
    position:absolute; top:8px; width:15px; height:22px;
    border-radius:7px 7px 8px 8px;
    background:linear-gradient(180deg,#ffffff,#edf7f3);
    border:2px solid #145342;
    overflow:hidden;
  }
  .keeper .eye-box.left { left:9px; }
  .keeper .eye-box.right { right:9px; }
  .keeper .eye-box::before {
    content:""; position:absolute; left:50%; top:56%; transform:translate(-50%,-50%);
    width:8px; height:12px; border-radius:50%;
    background:#10b085; box-shadow: inset 0 -3px 0 rgba(0,0,0,.14);
  }
  .keeper .eye-box::after {
    content:""; position:absolute; left:50%; top:58%; transform:translate(-50%,-50%);
    width:4px; height:6px; border-radius:50%; background:#122639;
    box-shadow:-2px -4px 0 0 rgba(255,255,255,.95);
  }
  .keeper .mouth {
    position:absolute; left:17px; bottom:8px; width:22px; height:9px;
    border-bottom:2px solid #6b412b; border-radius:0 0 14px 14px;
  }
  .keeper .torso {
    position:absolute; left:40px; top:78px; width:74px; height:68px;
    border-radius:8px 8px 6px 6px;
    background:linear-gradient(180deg,#2f2b83,#21206f 100%);
    border:3px solid rgba(0,0,0,.14);
    overflow:hidden;
    box-shadow: inset 0 2px 0 rgba(255,255,255,.18);
  }
  .keeper .torso::before {
    content:""; position:absolute; inset:0;
    background:
      linear-gradient(90deg, transparent 0 10px, #eaf0f6 10px 15px, transparent 15px 26px, #eaf0f6 26px 31px, transparent 31px 43px, #eaf0f6 43px 48px, transparent 48px 59px, #eaf0f6 59px 64px, transparent 64px 100%),
      linear-gradient(transparent 0 14px, #eaf0f6 14px 19px, transparent 19px 38px, #eaf0f6 38px 43px, transparent 43px 100%);
    opacity:.95;
  }
  .keeper .vest-v {
    position:absolute; left:70px; top:78px; width:14px; height:68px;
    background:linear-gradient(180deg,transparent 0 8px,#eaf0f6 8px 60px,transparent 60px 100%);
    z-index:1;
  }
  .keeper .neck {
    position:absolute; left:67px; top:73px; width:20px; height:10px;
    border-radius:0 0 5px 5px; background:#edb88d;
  }
  .keeper .arm {
    position:absolute; top:86px; width:34px; height:54px;
  }
  .keeper .arm.left { left:16px; }
  .keeper .arm.right { right:16px; }
  .keeper .upper-arm {
    position:absolute; left:0; top:0; width:32px; height:40px;
    border-radius:16px 16px 8px 8px;
    background:linear-gradient(180deg,#67d0e4,#44b8cf 100%);
    border:3px solid rgba(0,0,0,.12);
  }
  .keeper .arm.left .upper-arm { transform:rotate(6deg); }
  .keeper .arm.right .upper-arm { transform:rotate(-6deg); }
  .keeper .hand {
    position:absolute; bottom:0; width:22px; height:22px;
    border:4px solid #b8c0c9; border-right-color:transparent;
    border-radius:50%; background:transparent;
    box-shadow:inset 0 0 0 2px rgba(255,255,255,.25);
  }
  .keeper .arm.left .hand { left:-2px; transform:rotate(8deg); }
  .keeper .arm.right .hand { right:-2px; transform:scaleX(-1) rotate(8deg); }
  .keeper .hip {
    position:absolute; left:51px; top:143px; width:52px; height:12px;
    border-radius:4px; background:#284093;
  }
  .keeper .leg {
    position:absolute; top:152px; width:28px; height:40px;
    border-radius:5px 5px 4px 4px;
    background:linear-gradient(180deg,#1d4e8d,#153d72 100%);
    border:3px solid rgba(0,0,0,.14);
    box-shadow:inset 0 2px 0 rgba(255,255,255,.08);
  }
  .keeper .leg.left { left:48px; }
  .keeper .leg.right { right:48px; }


  .aim {
    position: absolute; width: 46px; height: 46px; border-radius: 50%;
    border: 3px solid var(--lime);
    left: 50%; top: 34%; transform: translate(-50%,-50%);
    z-index: 8; pointer-events: none;
    box-shadow: 0 0 0 8px rgba(185,245,47,.08), 0 0 24px rgba(185,245,47,.55);
    opacity: 0;
    transition: opacity .2s;
  }
  .aim::before, .aim::after { content:""; position:absolute; background:var(--lime); }
  .aim::before { width:64px; height:2px; left:50%; top:50%; transform:translate(-50%,-50%); }
  .aim::after { width:2px; height:64px; left:50%; top:50%; transform:translate(-50%,-50%); }
  .goal.ready .aim { opacity: 1; }

  .ball {
    position:absolute;
    left:50%; bottom:56px;
    transform:translate(-50%,0) scale(1) rotate(0deg);
    width:74px; height:74px; border-radius:50%;
    z-index:12;
    background:#fff;
    box-shadow:0 10px 16px rgba(0,0,0,.42);
    transition:left .44s cubic-bezier(.12,.78,.18,1), top .44s cubic-bezier(.12,.78,.18,1), bottom .44s, transform .44s cubic-bezier(.12,.78,.18,1);
    pointer-events:none;
    overflow:hidden;
  }
  .ball img {
    display:block; width:100%; height:100%; object-fit:cover; border-radius:50%;
    user-select:none; -webkit-user-drag:none;
  }
  .ball.kick { transform:translate(-50%,-50%) scale(.46) rotate(620deg); }
  .ball.reset { transition:none; }

  .penalty-spot { position:absolute; left:50%; bottom:50px; transform:translateX(-50%); width:86px; height:23px; border-radius:50%; background:rgba(255,255,255,.16); filter:blur(1px); }
  .field-line { position:absolute; left:50%; bottom:-150px; transform:translateX(-50%); width:740px; height:340px; border:4px solid rgba(255,255,255,.36); border-radius:50%; }

  .instruction {
    position:absolute; left:50%; bottom:112px; transform:translateX(-50%);
    width:min(92%,720px); text-align:center;
    font-weight:800; font-size:15px; color:#e7f7ff;
    text-shadow:0 2px 8px rgba(0,0,0,.5);
  }
  .instruction b { color:var(--lime); }

  .result-toast {
    position:absolute; left:50%; top:48%; transform:translate(-50%,-50%) scale(.8);
    z-index:30; pointer-events:none; opacity:0;
    font-size:clamp(40px,9vw,88px); font-weight:1000; font-style:italic;
    letter-spacing:.06em; text-transform:uppercase;
    text-shadow:0 8px 0 rgba(0,0,0,.3),0 0 30px rgba(255,255,255,.4);
    transition:.2s ease;
  }
  .result-toast.show { opacity:1; transform:translate(-50%,-50%) scale(1); }
  .result-toast.goal-text { color:var(--lime); }
  .result-toast.save-text { color:#ffcf5a; }
  .result-toast.miss-text { color:#ff5970; }

  .overlay {
    position:absolute; inset:0; z-index:50;
    display:flex; align-items:center; justify-content:center;
    background:radial-gradient(circle at 50% 30%, rgba(0,167,232,.20), transparent 45%), rgba(1,10,20,.88);
    backdrop-filter:blur(8px);
    padding:22px;
  }
  .overlay.hidden { display:none; }
  .panel {
    width:min(92vw,580px); text-align:center;
    padding:38px 34px 34px;
    border:1px solid rgba(127,233,255,.28);
    background:linear-gradient(180deg, rgba(8,35,57,.96), rgba(2,17,31,.96));
    border-radius:28px;
    box-shadow:0 30px 100px rgba(0,0,0,.5), inset 0 1px rgba(255,255,255,.08);
    position:relative; overflow:hidden;
  }
  .panel::before { content:""; position:absolute; inset:-80px; background:conic-gradient(from 180deg at 50% 50%, transparent, rgba(0,167,232,.13), transparent 35%); animation:spin 8s linear infinite; }
  @keyframes spin{to{transform:rotate(360deg)}}
  .panel > * { position:relative; z-index:2; }
  .cup-badge { display:inline-flex; align-items:center; gap:9px; padding:8px 14px; border-radius:99px; background:rgba(0,167,232,.12); border:1px solid rgba(127,233,255,.25); color:var(--cyan); font-size:12px; font-weight:900; letter-spacing:.16em; }
  .panel h1 { font-size:clamp(36px,8vw,66px); line-height:.92; margin:22px 0 14px; letter-spacing:-.04em; font-style:italic; }
  .panel h1 em { color:var(--lime); font-style:normal; text-shadow:0 0 22px rgba(185,245,47,.35); }
  .panel p { color:#bcd1e3; line-height:1.7; margin:0 auto 24px; max-width:430px; }
  .rules { display:grid; grid-template-columns:repeat(3,1fr); gap:8px; margin:20px 0 26px; }
  .rule { background:rgba(255,255,255,.045); border:1px solid rgba(255,255,255,.09); border-radius:14px; padding:12px 6px; }
  .rule strong { display:block; color:#fff; font-size:14px; } .rule span { color:#8fb0c8; font-size:11px; }
  .primary-btn, .secondary-btn {
    border:0; border-radius:16px; cursor:pointer; font-weight:1000; letter-spacing:.03em;
    padding:16px 24px; min-width:220px; transition:.2s ease;
  }
  .primary-btn { background:linear-gradient(135deg,var(--lime),#81d900); color:#153600; box-shadow:0 12px 32px rgba(185,245,47,.25); }
  .primary-btn:hover { transform:translateY(-2px); box-shadow:0 16px 42px rgba(185,245,47,.35); }
  .secondary-btn { background:rgba(255,255,255,.08); color:#fff; border:1px solid rgba(255,255,255,.14); margin-top:10px; }
  .name-box { margin: 0 auto 20px; max-width: 360px; text-align: left; }
  .name-box label { display:block; margin-bottom:8px; font-size:13px; color:#ddf8ff; font-weight:800; letter-spacing:.04em; }
  .name-input { width:100%; height:54px; border-radius:16px; border:1px solid rgba(255,255,255,.14); background:rgba(255,255,255,.06); color:#fff; padding:0 16px; font-size:16px; outline:none; }
  .name-input::placeholder { color:#7f9ab1; }
  .name-input:focus { border-color: rgba(127,233,255,.6); box-shadow:0 0 0 4px rgba(0,167,232,.12); }
  .name-help { margin-top:8px; font-size:12px; color:#83a3ba; }
  .start-overlay { padding:18px; }
  .start-panel {
    width:min(92vw,420px);
    padding:30px 26px 26px;
    border-radius:24px;
  }
  .start-panel::before { opacity:.55; }
  .start-logo-wrap {
    width:min(72vw,220px); height:58px; margin:0 auto 14px;
    display:flex; align-items:center; justify-content:center;
    border-radius:16px; background:rgba(255,255,255,.06);
    border:1px solid rgba(255,255,255,.08); padding:8px 12px;
  }
  .start-logo { max-width:100%; max-height:100%; object-fit:contain; display:block; }
  .start-kicker {
    color:var(--cyan); font-weight:900; font-size:12px;
    letter-spacing:.18em; margin-bottom:10px;
  }
  .panel .start-title {
    margin:0 0 12px; font-size:clamp(34px,9vw,48px);
    line-height:1; font-style:normal; letter-spacing:-.04em;
  }
  .start-guide {
    margin:0 auto 18px; max-width:280px; color:#c9dced;
    font-size:14px; line-height:1.5;
  }
  .start-guide b { color:#ef3340; font-weight:1000; }
  .simple-name-box { margin:0 auto 12px; max-width:none; }
  .simple-name-box label { margin-bottom:7px; font-size:13px; }
  .start-game-btn { width:100%; min-width:0; height:54px; padding:0 20px; }
  .final-score { font-size:68px; font-weight:1000; color:var(--lime); line-height:1; margin:18px 0 8px; }
  .mini { font-size:12px; color:#83a3ba; margin-top:14px; }

  .sound-btn {
    position:absolute; right:18px; bottom:18px; z-index:40;
    width:44px; height:44px; border-radius:50%; border:1px solid rgba(255,255,255,.16);
    background:rgba(3,18,34,.7); color:#fff; cursor:pointer;
  }

  #confetti { position:absolute; inset:0; width:100%; height:100%; pointer-events:none; z-index:45; }

  @media (max-width: 700px) {
    body { align-items: stretch; }
    .game-shell { min-height: 100svh; }
    .topbar { height:82px; padding:12px; }
    .brand-logo-wrap { width:150px; height:44px; border-radius:13px; padding:5px 9px; }
    .brand-meta strong { font-size:14px; }
    .brand-meta span { font-size:9px; letter-spacing:.18em; }
    .score-card { gap:8px; padding:8px 10px; }
    .score-label { display:none; }
    .shot-dot { width:20px; height:20px; font-size:11px; }
    .arena { height:calc(100svh - 82px); min-height:600px; }
    .banner { top:18px; font-size:12px; }
    .goal-wrap { top:96px; width:94vw; }
    .keeper { transform:translate(-50%,-50%) scale(.74) rotate(var(--rot)); }
    .ball { bottom:84px; }
    .penalty-spot { bottom:76px; }
    .instruction { bottom:132px; font-size:12px; line-height:1.45; width:90%; }
    .panel { padding:26px 18px 22px; border-radius:22px; }
    .start-overlay { align-items:center; padding:14px; }
    .start-panel { width:min(92vw,360px); padding:24px 18px 20px; }
    .start-logo-wrap { height:52px; margin-bottom:12px; border-radius:14px; }
    .panel .start-title { font-size:38px; margin-bottom:10px; }
    .start-kicker { font-size:11px; margin-bottom:8px; }
    .start-guide { font-size:13px; margin-bottom:16px; }
    .name-input { height:52px; font-size:16px; border-radius:14px; }
    .start-game-btn { height:52px; border-radius:14px; }
    .rules { grid-template-columns:1fr; }
    .rule { display:flex; justify-content:space-between; padding:10px 14px; }
  }

  @media (max-width: 430px) {
    .game-shell { width:100vw; min-height:100svh; }
    .topbar { height:70px; padding:9px 10px; gap:8px; }
    .brand { gap:8px; min-width:0; }
    .brand-logo-wrap { width:118px; height:38px; padding:4px 7px; border-radius:10px; }
    .brand-meta strong { font-size:12px; }
    .brand-meta span { font-size:8px; letter-spacing:.12em; }
    .score-card { padding:7px 8px; border-radius:13px; }
    .shot-dot { width:18px; height:18px; font-size:10px; }
    .shots { gap:5px; }
    .arena { height:calc(100svh - 70px); min-height:560px; }
    .banner { top:12px; height:38px; width:94%; font-size:10px; letter-spacing:.10em; }
    .goal-wrap { top:70px; width:96vw; }
    .keeper { transform:translate(-50%,-50%) scale(.66) rotate(var(--rot)); }
    .ball { width:64px; height:64px; bottom:70px; }
    .penalty-spot { bottom:64px; }
    .instruction { bottom:118px; font-size:11px; width:92%; }
    .sound-btn { right:10px; bottom:10px; width:40px; height:40px; }
    .start-overlay { padding:12px; }
    .start-panel { width:100%; max-width:340px; padding:22px 16px 18px; border-radius:20px; }
    .start-logo-wrap { width:min(76vw,200px); height:48px; margin-bottom:10px; }
    .panel .start-title { font-size:36px; }
    .start-guide { font-size:12px; margin-bottom:14px; }
  }
</style>
</head>
<body>
<div class="game-shell" id="gameShell">
  <header class="topbar">
    <div class="brand">
      <div class="brand-logo-wrap"><img class="brand-logo" src="data:image/png;base64,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" alt="GASTRON 로고"></div>
      <div class="brand-meta"><strong>FC</strong><span>GAS CUP 2026</span></div>
    </div>
    <div class="score-card">
      <span class="score-label">PENALTY</span>
      <div class="shots" id="shots"></div>
    </div>
  </header>

  <main class="arena" id="arena">
    <canvas id="confetti"></canvas>
    <div class="stadium-lights"><i class="beam b1"></i><i class="beam b2"></i></div>
    <div class="banner">GAS CUP 2026 · FINAL SHOOTOUT</div>

    <div class="goal-wrap" id="goalWrap">
      <div class="goal" id="goal">
        <div class="post-glow"></div>
        <div class="aim" id="aim"></div>
        <div class="keeper" id="keeper" aria-label="안전모를 착용한 골키퍼">
          <div class="shadow"></div>
          <div class="helmet"></div>
          <div class="head">
            <div class="eye-box left"></div>
            <div class="eye-box right"></div>
            <div class="mouth"></div>
          </div>
          <div class="neck"></div>
          <div class="torso"></div>
          <div class="vest-v"></div>
          <div class="arm left"><div class="upper-arm"></div><div class="hand"></div></div>
          <div class="arm right"><div class="upper-arm"></div><div class="hand"></div></div>
          <div class="hip"></div>
          <div class="leg left"></div>
          <div class="leg right"></div>
        </div>
      </div>
    </div>

    <div class="field-line"></div>
    <div class="penalty-spot"></div>
    <div class="ball" id="ball"><img src="data:image/jpeg;base64,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" alt="축구공"></div>
    <div class="instruction" id="instruction">골대 안 원하는 곳을 <b>터치</b>해 슛하세요. 3골 성공 시 우승!</div>
    <div class="result-toast" id="resultToast">GOAL!</div>

    <button class="sound-btn" id="soundBtn" aria-label="사운드 켜기/끄기">🔊</button>

    <section class="overlay start-overlay" id="startOverlay">
      <div class="panel start-panel">
        <div class="start-logo-wrap"><img class="start-logo" src="data:image/png;base64,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" alt="GASTRON 로고"></div>
        <div class="start-kicker">GAS CUP 2026</div>
        <h1 class="start-title">승부차기</h1>
        <p class="start-guide">이름을 입력하고 <b>3골을 성공</b>시켜 우승하세요.</p>
        <div class="name-box simple-name-box">
          <label for="playerNameInput">이름</label>
          <input class="name-input" id="playerNameInput" type="text" maxlength="12" placeholder="이름을 입력하세요" autocomplete="name" enterkeyhint="go">
        </div>
        <button class="primary-btn start-game-btn" id="startBtn">게임 시작</button>
      </div>
    </section>

    <section class="overlay hidden" id="endOverlay">
      <div class="panel">
        <div class="cup-badge" id="endBadge">MATCH RESULT</div>
        <h1 id="endTitle">도전 종료</h1>
        <div class="final-score" id="finalScore">0골 · 0실패</div>
        <p id="endMessage"></p>
        <button class="primary-btn" id="retryBtn">재도전하기</button>
      </div>
    </section>
  </main>
</div>

<script>
(() => {
  const TARGET_GOALS = 3;
  const MAX_MISSES = 3;
  const MAX_ATTEMPTS = 5;
  const goal = document.getElementById('goal');
  const goalWrap = document.getElementById('goalWrap');
  const keeper = document.getElementById('keeper');
  const ball = document.getElementById('ball');
  const aim = document.getElementById('aim');
  const shotsEl = document.getElementById('shots');
  const instruction = document.getElementById('instruction');
  const toast = document.getElementById('resultToast');
  const startOverlay = document.getElementById('startOverlay');
  const endOverlay = document.getElementById('endOverlay');
  const startBtn = document.getElementById('startBtn');
  const retryBtn = document.getElementById('retryBtn');
  const playerNameInput = document.getElementById('playerNameInput');
  const soundBtn = document.getElementById('soundBtn');
  const finalScore = document.getElementById('finalScore');
  const endTitle = document.getElementById('endTitle');
  const endMessage = document.getElementById('endMessage');
  const endBadge = document.getElementById('endBadge');
  const confettiCanvas = document.getElementById('confetti');
  const ctx = confettiCanvas.getContext('2d');

  let shotIndex = 0;
  let goals = 0;
  let misses = 0;
  let active = false;
  let aiming = false;
  let soundOn = true;
  let playerName = '';
  let target = { x: .5, y: .35 };
  let audioCtx;
  let confetti = [];
  let confettiFrame;

  function resizeCanvas() {
    const dpr = Math.min(window.devicePixelRatio || 1, 2);
    confettiCanvas.width = confettiCanvas.clientWidth * dpr;
    confettiCanvas.height = confettiCanvas.clientHeight * dpr;
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
  }
  window.addEventListener('resize', resizeCanvas);
  resizeCanvas();

  function initShots() {
    shotsEl.innerHTML = '';
    for (let i = 0; i < MAX_ATTEMPTS; i++) {
      const dot = document.createElement('div');
      dot.className = 'shot-dot';
      dot.textContent = i + 1;
      shotsEl.appendChild(dot);
    }
  }

  function updateAim(clientX, clientY) {
    if (!aiming) return;
    const r = goal.getBoundingClientRect();
    let x = Math.max(18, Math.min(r.width - 18, clientX - r.left));
    let y = Math.max(18, Math.min(r.height - 18, clientY - r.top));
    target = { x: x / r.width, y: y / r.height };
    aim.style.left = x + 'px';
    aim.style.top = y + 'px';
  }

  function onPointerMove(e) { updateAim(e.clientX, e.clientY); }
  goal.addEventListener('pointermove', onPointerMove);
  goal.addEventListener('pointerdown', e => {
    if (!aiming) return;
    updateAim(e.clientX, e.clientY);
    shoot();
  });

  function tone(freq, duration, type='sine', volume=.05, delay=0) {
    if (!soundOn) return;
    audioCtx ||= new (window.AudioContext || window.webkitAudioContext)();
    const o = audioCtx.createOscillator();
    const g = audioCtx.createGain();
    o.type = type; o.frequency.value = freq;
    g.gain.setValueAtTime(0, audioCtx.currentTime + delay);
    g.gain.linearRampToValueAtTime(volume, audioCtx.currentTime + delay + .01);
    g.gain.exponentialRampToValueAtTime(.0001, audioCtx.currentTime + delay + duration);
    o.connect(g).connect(audioCtx.destination);
    o.start(audioCtx.currentTime + delay); o.stop(audioCtx.currentTime + delay + duration + .03);
  }
  function kickSound(){ tone(115,.12,'square',.05); tone(75,.16,'sine',.08,.02); }
  function goalSound(){ [440,554,659,880].forEach((f,i)=>tone(f,.28,'triangle',.05,i*.07)); }
  function failSound(){ tone(180,.35,'sawtooth',.045); tone(130,.42,'sawtooth',.035,.08); }

  soundBtn.addEventListener('click', () => {
    soundOn = !soundOn;
    soundBtn.textContent = soundOn ? '🔊' : '🔇';
    if (soundOn) tone(620,.12,'sine',.04);
  });

  function resetKeeper() {
    keeper.style.setProperty('--x', '50%');
    keeper.style.setProperty('--y', '57%');
    keeper.style.setProperty('--rot', '0deg');
  }

  function beginRound() {
    active = true;
    aiming = true;
    resetKeeper();
    goal.classList.add('ready');
    instruction.innerHTML = `${playerName || "플레이어"} · 현재 ${goals}골 / ${misses}실패 · <b>3골 성공 시 우승</b>, 3번 실패 시 재도전!`;
    ball.classList.add('reset');
    ball.classList.remove('kick');
    ball.style.left = '50%';
    ball.style.top = '';
    ball.style.bottom = window.innerWidth <= 700 ? '84px' : '56px';
    void ball.offsetWidth;
    ball.classList.remove('reset');
  }

  function shoot() {
    if (!active || !aiming) return;
    aiming = false;
    goal.classList.remove('ready');
    kickSound();

    const keeperChoices = [
      {x:.16,y:.26,rot:-24}, {x:.84,y:.26,rot:24},
      {x:.20,y:.50,rot:-18}, {x:.80,y:.50,rot:18},
      {x:.24,y:.72,rot:-30}, {x:.76,y:.72,rot:30},
      {x:.50,y:.36,rot:0}, {x:.50,y:.62,rot:0}
    ];
    const anticipation = Math.random() < .50;
    let k;
    if (anticipation) {
      const clamp = (n, min, max) => Math.max(min, Math.min(max, n));
      k = {
        x: clamp(target.x + (Math.random() - .5) * .085, .11, .89),
        y: clamp(target.y + (Math.random() - .5) * .08, .16, .82),
        rot: target.x < .5 ? -24 : 24
      };
    } else {
      k = keeperChoices[Math.floor(Math.random() * keeperChoices.length)];
    }
    keeper.style.setProperty('--x', `${k.x*100}%`);
    keeper.style.setProperty('--y', `${k.y*100}%`);
    keeper.style.setProperty('--rot', `${k.rot}deg`);

    const goalRect = goal.getBoundingClientRect();
    const arenaRect = document.getElementById('arena').getBoundingClientRect();
    const targetX = goalRect.left - arenaRect.left + target.x * goalRect.width;
    const targetY = goalRect.top - arenaRect.top + target.y * goalRect.height;
    ball.style.bottom = 'auto';
    ball.style.left = `${targetX}px`;
    ball.style.top = `${targetY}px`;
    ball.classList.add('kick');

    const dx = target.x - k.x;
    const dy = target.y - k.y;
    const keeperDistance = Math.sqrt(dx*dx + dy*dy);
    const nearEdge = target.x < .055 || target.x > .945 || target.y < .055 || target.y > .94;
    const central = target.x > .39 && target.x < .61 && target.y > .28 && target.y < .68;
    const keeperReach = anticipation ? .29 : .27;
    const directSave = keeperDistance < keeperReach && Math.random() > .06;
    const centralSave = !directSave && central && Math.random() < .24;
    const isSave = directSave || centralSave;
    const isMiss = !isSave && nearEdge && Math.random() < .63;
    const isGoal = !isSave && !isMiss;

    setTimeout(() => resolveShot(isGoal, isSave), 450);
  }

  function resolveShot(isGoal, isSave) {
    const dot = shotsEl.children[shotIndex];
    toast.className = 'result-toast show';

    if (isGoal) {
      goals++;
      dot.classList.add('goal');
      dot.textContent = '✓';
      toast.textContent = 'GOAL!';
      toast.classList.add('goal-text');
      instruction.innerHTML = goals >= TARGET_GOALS
        ? `<b>${playerName || '플레이어'}님!</b> 3골 성공! 우승이 확정됩니다.`
        : `<b>득점 성공!</b> 현재 ${goals}골 / ${misses}실패. ${TARGET_GOALS - goals}골만 더 넣으면 우승!`;
      goalSound();
      burstConfetti(30);
    } else {
      misses++;
      dot.classList.add('miss');
      dot.textContent = '×';
      toast.textContent = isSave ? 'SAVE!' : 'MISS!';
      toast.classList.add(isSave ? 'save-text' : 'miss-text');
      instruction.innerHTML = misses >= MAX_MISSES
        ? `${playerName || '플레이어'}님, 3번 실패했습니다. 재도전합니다.`
        : `${isSave ? '골키퍼가 막았습니다.' : '아쉽게 골대를 벗어났습니다.'} 현재 ${goals}골 / ${misses}실패. 아직 기회가 있습니다!`;
      failSound();
    }

    shotIndex++;
    setTimeout(() => toast.classList.remove('show'), isGoal ? 680 : 720);
    setTimeout(() => {
      if (goals >= TARGET_GOALS) finishGame(true);
      else if (misses >= MAX_MISSES || shotIndex >= MAX_ATTEMPTS) finishGame(false);
      else beginRound();
    }, 1150);
  }

  function finishGame(cleared) {
    active = false;
    aiming = false;
    goal.classList.remove('ready');
    finalScore.textContent = `${goals}골 · ${misses}실패`;
    if (cleared) {
      endBadge.textContent = '🏆 GAS CUP 2026 CHAMPION';
      endTitle.innerHTML = `${playerName || '플레이어'}님!<br><em>우승!</em>`;
      endMessage.textContent = `총 3골 성공! ${playerName || '플레이어'}님이 가스트론 FC를 가스컵 2026 정상에 올렸습니다.`;
      burstConfetti(180);
      goalSound();
      setTimeout(goalSound, 420);
    } else {
      endBadge.textContent = 'RETRY MATCH';
      endTitle.textContent = '재도전';
      endMessage.textContent = `3번 실패했습니다. 최종 기록은 ${goals}골 / ${misses}실패입니다. 다시 도전해 총 3골을 성공시키세요.`;
    }
    setTimeout(() => endOverlay.classList.remove('hidden'), 350);
  }

  function startGame(fromStartOverlay = false) {
    if (fromStartOverlay) {
      const entered = (playerNameInput.value || '').trim();
      if (!entered) {
        playerNameInput.value = '';
        playerNameInput.placeholder = '이름을 입력해주세요';
        playerNameInput.focus();
        return;
      }
      playerName = entered;
    }

    shotIndex = 0;
    goals = 0;
    misses = 0;
    active = true;
    initShots();
    startOverlay.classList.add('hidden');
    endOverlay.classList.add('hidden');
    beginRound();
    tone(520,.08,'triangle',.04); tone(760,.12,'triangle',.035,.06);
  }

  startBtn.addEventListener('click', () => startGame(true));
  retryBtn.addEventListener('click', () => startGame(false));
  playerNameInput.addEventListener('keydown', e => {
    if (e.key === 'Enter') startGame(true);
  });

  function burstConfetti(count) {
    const w = confettiCanvas.clientWidth, h = confettiCanvas.clientHeight;
    const palette = ['#b9f52f','#00a7e8','#7fe9ff','#ff9f1c','#ffffff'];
    for (let i=0;i<count;i++) {
      confetti.push({
        x:w/2 + (Math.random()-.5)*220,
        y:h*.35 + (Math.random()-.5)*80,
        vx:(Math.random()-.5)*9,
        vy:-Math.random()*9-3,
        g:.16+Math.random()*.14,
        r:3+Math.random()*5,
        a:Math.random()*Math.PI,
        va:(Math.random()-.5)*.3,
        life:90+Math.random()*80,
        color:palette[Math.floor(Math.random()*palette.length)]
      });
    }
    if (!confettiFrame) animateConfetti();
  }
  function animateConfetti() {
    const w=confettiCanvas.clientWidth, h=confettiCanvas.clientHeight;
    ctx.clearRect(0,0,w,h);
    confetti = confetti.filter(p => p.life > 0 && p.y < h + 20);
    for (const p of confetti) {
      p.x += p.vx; p.y += p.vy; p.vy += p.g; p.a += p.va; p.life--;
      ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.a); ctx.globalAlpha=Math.min(1,p.life/30);
      ctx.fillStyle=p.color; ctx.fillRect(-p.r,-p.r*.55,p.r*2,p.r*1.1); ctx.restore();
    }
    if (confetti.length) confettiFrame=requestAnimationFrame(animateConfetti);
    else { cancelAnimationFrame(confettiFrame); confettiFrame=null; ctx.clearRect(0,0,w,h); }
  }

  initShots();
})();
</script>
</body>
</html>
