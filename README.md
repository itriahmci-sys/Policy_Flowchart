<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>台灣在宅醫療：醫院到居家的中繼轉銜與沙盒</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700&display=swap');
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --coral-50: #FAECE7; --coral-600: #993C1D; --coral-800: #712B13;
    --amber-50: #FAEEDA; --amber-600: #854F0B; --amber-800: #633806;
    --teal-50: #E1F5EE; --teal-600: #0F6E56; --teal-800: #085041;
    --blue-50: #E6F1FB; --blue-600: #185FA5; --blue-800: #0C447C;
    --gray-50: #F1EFE8; --gray-600: #5F5E5A; --gray-800: #444441;
    --purple-50: #EEEDFE; --purple-600: #534AB7; --purple-800: #3C3489;
    --red-50: #FCEBEB; --red-600: #A32D2D; --red-800: #791F1F;
    --text: #1a1a18;
    --text-muted: #6b6b66;
    --bg: #f7f7f4;
    --border: rgba(0,0,0,0.1);
    --arrow-color: #8a8a84;
  }

  body {
    font-family: 'Noto Sans TC', sans-serif;
    background: var(--bg);
    color: var(--text);
    padding: 48px 24px 72px;
  }

  .page-title {
    text-align: center;
    font-size: 24px;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 10px;
    letter-spacing: 0.02em;
  }
  .page-sub {
    text-align: center;
    font-size: 15px;
    color: var(--text-muted);
    margin-bottom: 48px;
  }

  .diagram {
    max-width: 960px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }

  /* ── 節點卡片 ── */
  .node {
    border-radius: 12px;
    padding: 18px 22px;
  }
  .node-title {
    font-size: 17px;
    font-weight: 700;
    line-height: 1.35;
    margin-bottom: 6px;
  }
  .node-sub {
    font-size: 13px;
    font-weight: 400;
    line-height: 1.55;
    opacity: 0.85;
  }

  /* ── 色彩 ── */
  .coral  { background: var(--coral-50);  border: 1.5px solid rgba(153,60,29,0.28); }
  .coral  .node-title { color: var(--coral-800); }
  .coral  .node-sub   { color: var(--coral-600); }

  .amber  { background: var(--amber-50);  border: 1.5px solid rgba(133,79,11,0.28); }
  .amber  .node-title { color: var(--amber-800); }
  .amber  .node-sub   { color: var(--amber-600); }

  .teal   { background: var(--teal-50);   border: 1.5px solid rgba(15,110,86,0.28); }
  .teal   .node-title { color: var(--teal-800); }
  .teal   .node-sub   { color: var(--teal-600); }

  .blue   { background: var(--blue-50);   border: 1.5px solid rgba(24,95,165,0.28); }
  .blue   .node-title { color: var(--blue-800); }
  .blue   .node-sub   { color: var(--blue-600); }

  .gray   { background: var(--gray-50);   border: 1.5px solid rgba(95,94,90,0.28); }
  .gray   .node-title { color: var(--gray-800); }
  .gray   .node-sub   { color: var(--gray-600); }

  /* ── 橫向箭頭 ── */
  .arrow-h {
    display: flex;
    align-items: center;
    flex-shrink: 0;
    width: 52px;
    padding: 0 4px;
  }
  .arr-line { flex: 1; height: 2px; background: var(--arrow-color); }
  .arr-head {
    width: 0; height: 0;
    border-top: 7px solid transparent;
    border-bottom: 7px solid transparent;
    border-left: 11px solid var(--arrow-color);
    flex-shrink: 0;
  }

  /* ── 向下箭頭 ── */
  .arrow-down-wrap {
    display: flex;
    justify-content: center;
    padding: 10px 0;
  }
  .arrow-down {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .arr-vline { width: 2px; background: var(--arrow-color); }
  .arr-vhead {
    width: 0; height: 0;
    border-left: 7px solid transparent;
    border-right: 7px solid transparent;
    border-top: 11px solid var(--arrow-color);
  }

  /* ── 沙盒ブロック ── */
  .sandbox-box {
    background: var(--purple-50);
    border: 2px dashed var(--purple-600);
    border-radius: 14px;
    padding: 20px 28px;
  }
  .sandbox-label {
    font-size: 13px;
    font-weight: 700;
    color: var(--purple-600);
    letter-spacing: 0.05em;
    margin-bottom: 6px;
  }
  .sandbox-title {
    font-size: 17px;
    font-weight: 700;
    color: var(--purple-800);
    margin-bottom: 6px;
  }
  .sandbox-desc {
    font-size: 13px;
    color: var(--purple-600);
    line-height: 1.6;
  }

  /* ── 法規缺口 ── */
  .gap-box {
    background: var(--red-50);
    border: 2px dashed var(--red-600);
    border-radius: 12px;
    padding: 18px 20px;
  }
  .gap-label {
    font-size: 12px;
    font-weight: 700;
    color: var(--red-600);
    margin-bottom: 5px;
  }
  .gap-box .node-title { color: var(--red-800); font-size: 17px; }
  .gap-box .node-sub   { color: var(--red-600); font-size: 13px; }

  /* ── 段落標題 ── */
  .section-label {
    font-size: 14px;
    font-weight: 700;
    color: var(--text-muted);
    text-align: center;
    letter-spacing: 0.06em;
    margin: 4px 0 16px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-label::before, .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── 三欄格線 ── */
  .three-col {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
  }

  /* ── 欄標題 ── */
  .col-header {
    font-size: 13px;
    font-weight: 700;
    text-align: center;
    margin-bottom: 10px;
  }
  .col-header.teal  { color: var(--teal-600); }
  .col-header.blue  { color: var(--blue-600); }
  .col-header.gray  { color: var(--gray-600); }

  /* ── 子節點 ── */
  .sub-col { display: flex; flex-direction: column; gap: 0; }
  .sub-node {
    border-radius: 10px;
    padding: 14px 16px;
  }
  .sub-node .node-title { font-size: 15px; }
  .sub-node .node-sub   { font-size: 12px; }

  /* ── 欄內小箭頭 ── */
  .col-arrow {
    display: flex;
    justify-content: center;
    padding: 6px 0;
  }

  /* ── 問題欄 ── */
  .problem-box {
    background: var(--red-50);
    border: 1.5px dashed var(--red-600);
    border-radius: 12px;
    padding: 18px 20px;
  }
  .problem-box .node-title { color: var(--red-800); font-size: 16px; }
  .problem-box .node-sub   { color: var(--red-600); font-size: 13px; line-height: 1.55; }

  /* ── 圖例 ── */
  .legend {
    display: flex;
    gap: 20px;
    justify-content: center;
    margin-top: 44px;
    flex-wrap: wrap;
  }
  .legend-item {
    display: flex;
    align-items: center;
    gap: 7px;
    font-size: 13px;
    color: var(--text-muted);
  }
  .legend-dot {
    width: 14px; height: 14px;
    border-radius: 4px;
    flex-shrink: 0;
  }
  .legend-dash {
    width: 22px; height: 0;
    border-top: 2.5px dashed;
    flex-shrink: 0;
  }

  @media (max-width: 680px) {
    .three-col { grid-template-columns: 1fr; }
    .page-title { font-size: 19px; }
    .node-title { font-size: 15px; }
  }
</style>
</head>
<body>

<div class="page-title">台灣在宅醫療：醫院到居家的中繼轉銜與沙盒</div>
<div class="page-sub">從急性住院到穩定居家的照護路徑、法規缺口與沙盒試驗介入點</div>

<div class="diagram">

  <!-- ══ 第一排：主流程橫向 ══ -->
  <div style="display:flex;align-items:center;gap:0;">

    <!-- 急性住院 -->
    <div class="node coral" style="flex:0 0 220px;">
      <div class="node-title">急性住院</div>
      <div class="node-sub">醫學中心 / 區域醫院<br>急性治療期</div>
    </div>

    <!-- → -->
    <div class="arrow-h">
      <div class="arr-line"></div>
      <div class="arr-head"></div>
    </div>

    <!-- PAC -->
    <div class="node amber" style="flex:1;">
      <div class="node-title">急性後期照護（PAC）</div>
      <div class="node-sub">住院復健 3–12 週｜腦中風、骨折、衰弱高齡、創傷性神經損傷<br>87.6% 功能進步，88% 成功返家，30日再住院率降至 15.2%</div>
    </div>

    <!-- → -->
    <div class="arrow-h">
      <div class="arr-line"></div>
      <div class="arr-head"></div>
    </div>

    <!-- 法規缺口 -->
    <div class="gap-box" style="flex:0 0 215px;">
      <div class="gap-label">⚠ 法規缺口</div>
      <div class="node-title">中繼照護（亞急性）</div>
      <div class="node-sub">PAC 後、穩定居家前<br>給付機制尚未完整覆蓋</div>
    </div>

  </div>

  <!-- ↓ 箭頭 -->
  <div class="arrow-down-wrap">
    <div class="arrow-down">
      <div class="arr-vline" style="height:28px;"></div>
      <div class="arr-vhead"></div>
    </div>
  </div>

  <!-- ══ 沙盒介入層 ══ -->
  <div class="sandbox-box">
    <div class="sandbox-label">🔬 監理沙盒介入層（受控實驗空間）</div>
    <div class="sandbox-title">《智慧醫療創新實驗條例》草案研議中</div>
    <div class="sandbox-desc">在受控環境中試行——遠距 IoT 生理監測、跨域健保給付包裹式設計、AI 輔助照護判斷、跨機構照護協定彈性化、FHIR 資料互通標準導入</div>
  </div>

  <!-- ↓ 箭頭 -->
  <div class="arrow-down-wrap">
    <div class="arrow-down">
      <div class="arr-vline" style="height:28px;"></div>
      <div class="arr-vhead"></div>
    </div>
  </div>

  <!-- ══ PAC 結案後三路分流標題 ══ -->
  <div class="section-label">PAC 結案後的三條轉銜路徑</div>

  <!-- 三路主節點 -->
  <div class="three-col">
    <div class="node teal" style="text-align:center;">
      <div class="node-title">返家 + 居家醫療</div>
      <div class="node-sub">健保居家醫療照護整合計畫<br>到宅醫師訪視 + 護理照護</div>
    </div>
    <div class="node blue" style="text-align:center;">
      <div class="node-title">在宅急症照護（HaH）</div>
      <div class="node-sub">113 年 7 月試辦<br>肺炎、尿路感染、軟組織感染</div>
    </div>
    <div class="node gray" style="text-align:center;">
      <div class="node-title">長照機構安置</div>
      <div class="node-sub">護理之家 / 日照中心<br>重度失能、需密集照護</div>
    </div>
  </div>

  <!-- ↓ 三欄各自向下箭頭 -->
  <div class="three-col" style="margin-top:0;">
    <div class="arrow-down-wrap">
      <div class="arrow-down">
        <div class="arr-vline" style="height:22px;"></div>
        <div class="arr-vhead"></div>
      </div>
    </div>
    <div class="arrow-down-wrap">
      <div class="arrow-down">
        <div class="arr-vline" style="height:22px;"></div>
        <div class="arr-vhead"></div>
      </div>
    </div>
    <div class="arrow-down-wrap">
      <div class="arrow-down">
        <div class="arr-vline" style="height:22px;"></div>
        <div class="arr-vhead"></div>
      </div>
    </div>
  </div>

  <!-- 三路細節 -->
  <div class="three-col" style="align-items:start;">

    <!-- 欄一：居家醫療三階段 -->
    <div class="sub-col">
      <div class="col-header teal">居家醫療三階段（健保給付）</div>
      <div class="sub-node teal node">
        <div class="node-title">一般居家照護</div>
        <div class="node-sub">輕度需求、到宅訪視<br>醫師 + 護理 + 藥師到宅</div>
      </div>
      <div class="col-arrow">
        <div class="arrow-down">
          <div class="arr-vline" style="height:14px;"></div>
          <div class="arr-vhead"></div>
        </div>
      </div>
      <div class="sub-node teal node">
        <div class="node-title">重度居家醫療</div>
        <div class="node-sub">呼吸器依賴 / 重度失能<br>清醒時 50%+ 時間臥床</div>
      </div>
      <div class="col-arrow">
        <div class="arrow-down">
          <div class="arr-vline" style="height:14px;"></div>
          <div class="arr-vhead"></div>
        </div>
      </div>
      <div class="sub-node teal node">
        <div class="node-title">居家安寧療護</div>
        <div class="node-sub">末期病人、癌症末期<br>八大疾病末期、善終照護</div>
      </div>
    </div>

    <!-- 欄二：HaH 核心機制 -->
    <div class="sub-col">
      <div class="col-header blue">HaH 核心機制</div>
      <div class="sub-node blue node">
        <div class="node-title">垂直轉銜合作</div>
        <div class="node-sub">強化各級醫療體系協作<br>急症延伸到居家 / 機構</div>
      </div>
      <div class="col-arrow">
        <div class="arrow-down">
          <div class="arr-vline" style="height:14px;"></div>
          <div class="arr-vhead"></div>
        </div>
      </div>
      <div class="sub-node blue node">
        <div class="node-title">包裹式給付 + IoT</div>
        <div class="node-sub">遠距生理監測設備<br>避免不必要住院往返</div>
      </div>
      <div class="col-arrow">
        <div class="arrow-down">
          <div class="arr-vline" style="height:14px;"></div>
          <div class="arr-vhead"></div>
        </div>
      </div>
      <div class="sub-node blue node">
        <div class="node-title">費用負擔</div>
        <div class="node-sub">自負額 5%（居家照護規定）<br>重大傷病 / 偏鄉可減免</div>
      </div>
    </div>

    <!-- 欄三：長照3.0 -->
    <div class="sub-col">
      <div class="col-header gray">長照 3.0（2025–2026）</div>
      <div class="sub-node gray node">
        <div class="node-title">大家醫計畫整合</div>
        <div class="node-sub">在宅 + 遠距 + 安寧<br>統一資訊管理平台</div>
      </div>
      <div class="col-arrow">
        <div class="arrow-down">
          <div class="arr-vline" style="height:14px;"></div>
          <div class="arr-vhead"></div>
        </div>
      </div>
      <div class="sub-node gray node">
        <div class="node-title">出院前啟動銜接</div>
        <div class="node-sub">住院中即評估失能等級<br>出院前完成返家計畫</div>
      </div>
      <div class="col-arrow">
        <div class="arrow-down">
          <div class="arr-vline" style="height:14px;"></div>
          <div class="arr-vhead"></div>
        </div>
      </div>
      <div class="sub-node gray node">
        <div class="node-title">復能不中斷</div>
        <div class="node-sub">PAC 接長照確保連續性<br>個案管理師全程追蹤</div>
      </div>
    </div>

  </div>

  <!-- ↓ 箭頭 -->
  <div class="arrow-down-wrap" style="margin-top:8px;">
    <div class="arrow-down">
      <div class="arr-vline" style="height:28px;"></div>
      <div class="arr-vhead"></div>
    </div>
  </div>

  <!-- ══ 三大轉銜斷層 ══ -->
  <div class="section-label">三大轉銜斷層（沙盒最需解決的問題）</div>

  <div class="three-col">
    <div class="problem-box">
      <div class="node-title">給付空白</div>
      <div class="node-sub" style="margin-top:6px;">PAC 結案後到穩定居家醫療之間，健保給付銜接尚無明確機制。論日給付修訂中，可能改為包裹式給付模式。</div>
    </div>
    <div class="problem-box">
      <div class="node-title">跨域資料斷點</div>
      <div class="node-sub" style="margin-top:6px;">醫院、長照、社福三體系資訊尚未互通。FHIR 標準導入中，智慧雲端病歷平台仍在推進階段。</div>
    </div>
    <div class="problem-box">
      <div class="node-title">責任歸屬不清</div>
      <div class="node-sub" style="margin-top:6px;">衛福部醫事司、健保署、社家署各管一塊，跨機關協調成本高。沙盒機制是突破主管機關分立的關鍵工具。</div>
    </div>
  </div>

  <!-- ── 圖例 ── -->
  <div class="legend">
    <div class="legend-item">
      <div class="legend-dot" style="background:var(--coral-50);border:1.5px solid rgba(153,60,29,0.3);"></div>急性醫療
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background:var(--amber-50);border:1.5px solid rgba(133,79,11,0.3);"></div>中繼復健（PAC）
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background:var(--teal-50);border:1.5px solid rgba(15,110,86,0.3);"></div>居家醫療
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background:var(--blue-50);border:1.5px solid rgba(24,95,165,0.3);"></div>在宅急症（HaH）
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background:var(--gray-50);border:1.5px solid rgba(95,94,90,0.3);"></div>長照體系
    </div>
    <div class="legend-item">
      <div class="legend-dash" style="border-color:var(--purple-600);"></div>沙盒 / 實驗機制
    </div>
    <div class="legend-item">
      <div class="legend-dash" style="border-color:var(--red-600);"></div>法規缺口
    </div>
  </div>

</div>
</body>
</html>
