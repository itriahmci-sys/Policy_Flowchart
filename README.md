<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>整合醫療照護模式架構圖 ── 總覽</title>
<style>
  :root{
    --bg1:#fff7f0;
    --bg2:#f0f9ff;
    --bg3:#f5fbf2;
    --ink:#33344a;
    --sub:#7c7d94;
    --line:#eee1f5;
    --card-bg:#ffffff;
    --shadow:0 2px 6px rgba(120,90,180,.07),0 10px 26px rgba(120,90,180,.09);
    --shadow-hover:0 6px 14px rgba(120,90,180,.12),0 20px 40px rgba(120,90,180,.14);
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    font-family:"Noto Sans TC","Microsoft JhengHei","PingFang TC",-apple-system,BlinkMacSystemFont,sans-serif;
    background:
      radial-gradient(900px 480px at 6% -8%, #ffe3ef 0%, transparent 55%),
      radial-gradient(900px 480px at 96% 6%, #dcf3ff 0%, transparent 55%),
      radial-gradient(1000px 600px at 50% 105%, #e6fbe9 0%, transparent 55%),
      linear-gradient(180deg,#fffdf9, #fdfaf5 60%, #fbfaff);
    color:var(--ink);
    line-height:1.6;
    min-height:100vh;
  }
  header{
    max-width:1120px;
    margin:0 auto;
    padding:60px 24px 30px;
    text-align:center;
  }
  header .eyebrow{
    display:inline-block;
    font-size:12.5px;
    letter-spacing:.16em;
    font-weight:800;
    color:#ff6fa5;
    background:#ffe6f0;
    padding:6px 16px;
    border-radius:999px;
    margin-bottom:18px;
  }
  header h1{
    font-size:clamp(26px,4.2vw,36px);
    margin:0 0 12px;
    font-weight:800;
    letter-spacing:.01em;
    color:#1a1a1a;
  }
  header p{
    color:var(--sub);
    font-size:15.5px;
    max-width:660px;
    margin:0 auto;
  }
  main{
    max-width:1120px;
    margin:0 auto;
    padding:8px 24px 64px;
  }
  .section{
    margin-top:46px;
  }
  .section-head{
    display:flex;
    align-items:center;
    gap:12px;
    margin-bottom:20px;
  }
  .section-head .dot{
    width:11px;height:11px;border-radius:50%;
    background:linear-gradient(135deg,#ff9ac2,#7c9dff);
    flex:none;
  }
  .section-head.tw .dot{background:linear-gradient(135deg,#3ecf9a,#57d6c8);}
  .section-head h2{
    font-size:19px;
    margin:0;
    font-weight:800;
  }
  .section-head .count{
    font-size:12.5px;
    color:var(--sub);
    font-weight:700;
    background:#f3f0ff;
    padding:3px 11px;
    border-radius:999px;
  }
  .grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(255px,1fr));
    gap:18px;
  }
  a.card{
    display:flex;
    flex-direction:column;
    background:var(--card-bg);
    border:1px solid var(--line);
    border-radius:18px;
    padding:22px 22px 20px;
    text-decoration:none;
    color:inherit;
    box-shadow:var(--shadow);
    transition:transform .18s ease, box-shadow .18s ease, border-color .18s ease;
    position:relative;
    overflow:hidden;
    isolation:isolate;
  }
  a.card::before{
    content:"";
    position:absolute;
    inset:0;
    background:var(--card-tint);
    opacity:.55;
    z-index:-1;
  }
  a.card::after{
    content:"";
    position:absolute;
    top:-40px; right:-40px;
    width:120px; height:120px;
    border-radius:50%;
    background:var(--card-blob);
    opacity:.5;
    z-index:-1;
  }
  a.card:hover{
    transform:translateY(-4px) scale(1.01);
    box-shadow:var(--shadow-hover);
    border-color:var(--card-accent);
  }
  a.card .flag{
    font-size:28px;
    margin-bottom:12px;
    line-height:1;
  }
  a.card h3{
    font-size:15.5px;
    margin:0 0 6px;
    font-weight:800;
    color:var(--ink);
  }
  a.card p{
    font-size:13px;
    color:var(--sub);
    margin:0;
    flex-grow:1;
  }
  a.card .go{
    margin-top:16px;
    font-size:12.5px;
    font-weight:800;
    color:var(--card-accent);
    display:flex;
    align-items:center;
    gap:4px;
  }
  a.card .go svg{transition:transform .18s ease;}
  a.card:hover .go svg{transform:translateX(4px);}

  .c-jp{ --card-accent:#ff6f91; --card-tint:linear-gradient(160deg,#fff0f4,#ffffff 60%); --card-blob:#ffd3e0; }
  .c-fi{ --card-accent:#4fb0e8; --card-tint:linear-gradient(160deg,#eef8ff,#ffffff 60%); --card-blob:#c7e9ff; }
  .c-de1{--card-accent:#f0a941; --card-tint:linear-gradient(160deg,#fff7ea,#ffffff 60%); --card-blob:#ffe3b0; }
  .c-de2{--card-accent:#e08a2e; --card-tint:linear-gradient(160deg,#fff4e4,#ffffff 60%); --card-blob:#ffd79a; }
  .c-kr{ --card-accent:#a978e0; --card-tint:linear-gradient(160deg,#f6efff,#ffffff 60%); --card-blob:#e3cffb; }
  .c-uk{ --card-accent:#5a7de0; --card-tint:linear-gradient(160deg,#eef1ff,#ffffff 60%); --card-blob:#ccd6ff; }
  .c-tw{ --card-accent:#2bbd93; --card-tint:linear-gradient(160deg,#eafff6,#ffffff 60%); --card-blob:#bdf3dc; }

  .logo-bar{
    display:flex;
    justify-content:center;
    margin-bottom:22px;
  }
  .logo-bar img{
    height:56px;
    width:auto;
    display:block;
  }
  footer{
    max-width:1120px;
    margin:0 auto;
    padding:28px 24px 20px;
    color:var(--sub);
    font-size:12.5px;
    text-align:center;
    border-top:1px solid var(--line);
  }
  footer .copyright{
    margin-top:6px;
    font-size:12px;
    color:#9c9db0;
  }
</style>
</head>
<body>

<header>
  <div class="logo-bar">
    <img src="logo.png" alt="健康樂活與智慧醫療照護聯盟">
  </div>
  <span class="eyebrow">健康照護政策研究 ｜ 架構圖總覽</span>
  <h1>各國整合醫療照護模式架構圖</h1>
  <p>彙整日本、芬蘭、德國、韓國、英國之慢性病與整合照護制度架構，並對照台灣在宅醫療轉銜模式，點選卡片即可開啟各國詳細架構圖。</p>
</header>

<main>

  <div class="section">
    <div class="section-head">
      <span class="dot"></span>
      <h2>國際整合照護模式</h2>
      <span class="count">6 個架構圖</span>
    </div>
    <div class="grid">

      <a class="card c-jp" href="日本制度流程-flowchart.html">
        <div class="flag">🇯🇵</div>
        <h3>日本｜特定健診・保健指導制度</h3>
        <p>以醫療保險者為核心的代謝症候群預防管理機制，說明資金與服務流向。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

      <a class="card c-fi" href="芬蘭模式-flowchart.html">
        <div class="flag">🇫🇮</div>
        <h3>芬蘭｜慢性病管理模式</h3>
        <p>五層次健康生態系──全科醫師為核心、數位工具為橋梁、社區組織為後盾。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

      <a class="card c-de1" href="德國模式-flowchart.html">
        <div class="flag">🇩🇪</div>
        <h3>德國｜Kinzigtal 整合照護模式</h3>
        <p>以區域整合管理公司（GK GmbH）為樞紐的 Shared Savings 節餘分享機制。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

      <a class="card c-de2" href="德國模式-flowchart上位.html">
        <div class="flag">🇩🇪</div>
        <h3>德國｜政策治理架構（上位）</h3>
        <p>從聯邦立法到社區落地的完整制度鏈（SHI + Morbi-RSA + GK GmbH）。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

      <a class="card c-kr" href="韓國模式-flowchart.html">
        <div class="flag">🇰🇷</div>
        <h3>韓國｜慢性病整合管理模式</h3>
        <p>韓國 AX 計畫──以基層診所為核心的多方協作治理架構。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

      <a class="card c-uk" href="ics-framework-flowchart.html">
        <div class="flag">🇬🇧</div>
        <h3>英國｜ICS 整合醫療系統框架</h3>
        <p>英國整合醫療系統（Integrated Care System）治理架構圖。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

    </div>
  </div>

  <div class="section">
    <div class="section-head tw">
      <span class="dot"></span>
      <h2>台灣本土模式</h2>
      <span class="count">1 個架構圖</span>
    </div>
    <div class="grid">

      <a class="card c-tw" href="流程示意圖.html">
        <div class="flag">🇹🇼</div>
        <h3>台灣｜在宅醫療中繼轉銜與沙盒</h3>
        <p>台灣在宅醫療：醫院到居家的中繼轉銜與沙盒流程示意圖。</p>
        <span class="go">查看架構圖
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </span>
      </a>

    </div>
  </div>

</main>

<footer>
  各國模式架構圖 ｜ 點選卡片開啟個別頁面 ｜ 建議於桌面瀏覽器開啟以獲得最佳圖表顯示效果
  <div class="copyright">© 2026 健康樂活與智慧醫療照護聯盟 All Rights Reserved.</div>
</footer>

</body>
</html>
