<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>【15日締め切り】休み希望申請フォーム</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg:#F5F4F0;--surface:#FFFFFF;--border:#E2E0DA;--border-strong:#C8C5BC;
  --text:#1A1917;--text-muted:#7A7872;--text-hint:#B0AEA8;
  --shift-○-bg:#EBF3FF;--shift-○-text:#1A5FA8;--shift-○-border:#AACBF0;
  --shift-●-bg:#FFF4E6;--shift-●-text:#8B4F00;--shift-●-border:#F0C88A;
  --shift-☆-bg:#EDFAF3;--shift-☆-text:#0D6B45;--shift-☆-border:#8ED4B4;
  --shift-★-bg:#FFF0EE;--shift-★-text:#8B2500;--shift-★-border:#F0A898;
  --off-bg:#F5EEFF;--off-text:#4A1D8B;--off-border:#C4A8F0;
  --success-bg:#EDFAF3;--radius:12px;--radius-sm:8px;
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:'Noto Sans JP',sans-serif;background:var(--bg);min-height:100vh;color:var(--text);font-size:15px}
.app{max-width:480px;margin:0 auto;min-height:100vh;background:var(--bg)}
.header{background:var(--surface);border-bottom:1px solid var(--border);padding:16px 20px 14px;position:sticky;top:0;z-index:10}
.header-title{font-size:16px;font-weight:700;letter-spacing:.02em}
.header-sub{font-size:12px;color:var(--text-muted);margin-top:2px;font-family:'DM Mono',monospace}
.progress-wrap{display:flex;gap:4px;margin-top:12px}
.prog-seg{height:3px;flex:1;background:var(--border);border-radius:2px;transition:background .3s}
.prog-seg.done{background:var(--text)}.prog-seg.active{background:var(--text-muted)}
.content{padding:24px 20px 100px}
.step{display:none;animation:fadeUp .2s ease}.step.active{display:block}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.step-label{font-family:'DM Mono',monospace;font-size:11px;color:var(--text-hint);letter-spacing:.1em;text-transform:uppercase;margin-bottom:6px}
.step-title{font-size:20px;font-weight:700;line-height:1.3;margin-bottom:6px}
.step-desc{font-size:13px;color:var(--text-muted);margin-bottom:24px;line-height:1.6}
.emp-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:24px}
.emp-btn{padding:14px 10px;border:1px solid var(--border);border-radius:var(--radius-sm);text-align:center;cursor:pointer;font-size:14px;font-weight:500;background:var(--surface);color:var(--text);transition:border-color .15s,background .15s;user-select:none}
.emp-btn:active{background:var(--bg)}
.emp-btn.selected{border:2px solid var(--text);background:var(--text);color:var(--surface)}

/* カレンダー共通 */
.cal-nav{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.cal-nav-btn{width:36px;height:36px;border:1px solid var(--border);border-radius:var(--radius-sm);background:var(--surface);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:16px;color:var(--text);transition:background .15s}
.cal-nav-btn:active{background:var(--bg)}
.cal-month-label{font-size:15px;font-weight:700}
.cal-head{display:grid;grid-template-columns:repeat(7,1fr);margin-bottom:4px}
.cal-hd{text-align:center;font-size:11px;font-weight:500;padding:4px 0;font-family:'DM Mono',monospace;color:var(--text-muted)}
.cal-hd.sun{color:#C0392B}.cal-hd.sat{color:#1A5FA8}
.cal-days{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;margin-bottom:16px}
.cal-d{aspect-ratio:1;display:flex;flex-direction:column;align-items:center;justify-content:center;border-radius:50%;font-size:14px;cursor:pointer;position:relative;transition:background .12s;user-select:none}
.cal-d:active{background:var(--border)}
.cal-d.empty{cursor:default}
.cal-d.past{color:var(--text-hint);cursor:default}
.cal-d.sun{color:#C0392B}.cal-d.sat{color:#1A5FA8}
.cal-d.selected{background:var(--text);color:var(--surface);font-weight:700}
.cal-d.selected.sun,.cal-d.selected.sat{color:var(--surface)}
/* 申請済み（セッション内・今回入力中） */
.cal-d.submitted{background:#E8E8E8;border-radius:6px;cursor:not-allowed;color:#999;font-size:12px}
/* 過去申請（localStorage履歴） */
.cal-d.history-day{border-radius:6px}

/* チップ */
.chip-wrap{display:flex;flex-wrap:wrap;gap:6px;min-height:32px;margin-bottom:4px}
.chip{display:inline-flex;align-items:center;gap:5px;padding:5px 10px 5px 12px;background:var(--surface);border:1px solid var(--border-strong);border-radius:20px;font-size:13px;font-weight:500;font-family:'DM Mono',monospace}
.chip-x{cursor:pointer;color:var(--text-muted);font-size:15px;line-height:1;padding:0 2px}
.chip-hint{font-size:12px;color:var(--text-hint);padding:6px 0}

/* 種別 */
.type-section-label{font-size:12px;font-weight:700;color:var(--text-muted);letter-spacing:.08em;text-transform:uppercase;margin:20px 0 10px}
.off-card{border:1.5px dashed var(--off-border);border-radius:var(--radius);padding:16px;cursor:pointer;background:var(--surface);display:flex;align-items:center;gap:14px;margin-bottom:10px;transition:all .15s;user-select:none}
.off-card:active{background:var(--off-bg)}
.off-card.selected{border:2px solid var(--off-text);background:var(--off-bg)}
.off-icon{width:44px;height:44px;border-radius:10px;background:var(--off-bg);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0}
.off-card.selected .off-icon{background:rgba(74,29,139,.15)}
.off-text-main{font-size:15px;font-weight:700;color:var(--off-text)}
.off-text-sub{font-size:12px;color:var(--text-muted);margin-top:2px}
.time-range-wrap{display:none;margin-top:14px;padding-top:14px;border-top:1px solid var(--off-border)}
.off-card.selected .time-range-wrap{display:block}
.time-range-row{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;gap:8px;margin-bottom:10px}
.time-range-row select{width:100%;padding:9px 10px;border:1px solid var(--border-strong);border-radius:var(--radius-sm);font-size:14px;font-family:'DM Mono',monospace;background:var(--surface);color:var(--text);appearance:none;-webkit-appearance:none;text-align:center}
.time-sep{font-size:14px;color:var(--text-muted);text-align:center}
.time-hint{font-size:11px;color:var(--off-text);text-align:center;font-weight:500}
.shift-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.shift-card{border:1px solid var(--border);border-radius:var(--radius);padding:14px 10px;cursor:pointer;background:var(--surface);text-align:center;transition:all .15s;user-select:none}
.shift-card:active{opacity:.8}
.shift-sym{font-size:28px;margin-bottom:4px}
.shift-name{font-size:13px;font-weight:700;margin-bottom:2px}
.shift-time{font-size:11px;font-family:'DM Mono',monospace}
.shift-h{font-size:11px;font-weight:700;margin-top:4px}
.shift-card[data-shift="○"]{border-color:var(--shift-○-border)}
.shift-card[data-shift="○"].selected{background:var(--shift-○-bg);border:2px solid var(--shift-○-text)}
.shift-card[data-shift="○"] .shift-sym,.shift-card[data-shift="○"] .shift-name,.shift-card[data-shift="○"] .shift-time,.shift-card[data-shift="○"] .shift-h{color:var(--shift-○-text)}
.shift-card[data-shift="●"]{border-color:var(--shift-●-border)}
.shift-card[data-shift="●"].selected{background:var(--shift-●-bg);border:2px solid var(--shift-●-text)}
.shift-card[data-shift="●"] .shift-sym,.shift-card[data-shift="●"] .shift-name,.shift-card[data-shift="●"] .shift-time,.shift-card[data-shift="●"] .shift-h{color:var(--shift-●-text)}
.shift-card[data-shift="☆"]{border-color:var(--shift-☆-border)}
.shift-card[data-shift="☆"].selected{background:var(--shift-☆-bg);border:2px solid var(--shift-☆-text)}
.shift-card[data-shift="☆"] .shift-sym,.shift-card[data-shift="☆"] .shift-name,.shift-card[data-shift="☆"] .shift-time,.shift-card[data-shift="☆"] .shift-h{color:var(--shift-☆-text)}
.shift-card[data-shift="★"]{border-color:var(--shift-★-border)}
.shift-card[data-shift="★"].selected{background:var(--shift-★-bg);border:2px solid var(--shift-★-text)}
.shift-card[data-shift="★"] .shift-sym,.shift-card[data-shift="★"] .shift-name,.shift-card[data-shift="★"] .shift-time,.shift-card[data-shift="★"] .shift-h{color:var(--shift-★-text)}

/* 備考 */
.note-area{width:100%;padding:14px;border:1px solid var(--border-strong);border-radius:var(--radius);font-size:15px;font-family:'Noto Sans JP',sans-serif;background:var(--surface);color:var(--text);resize:none;min-height:88px;outline:none;transition:border-color .15s}
.note-area:focus{border-color:var(--text)}

/* 確認カード */
.confirm-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;margin-bottom:20px}
.confirm-row{display:flex;justify-content:space-between;align-items:center;padding:14px 16px;border-bottom:1px solid var(--border);gap:12px}
.confirm-row:last-child{border-bottom:none}
.c-label{font-size:13px;color:var(--text-muted);flex-shrink:0}
.c-val{font-size:14px;font-weight:700;text-align:right;line-height:1.5;flex:1}
.edit-btn{font-size:12px;color:var(--text-muted);background:var(--bg);border:1px solid var(--border-strong);border-radius:6px;padding:3px 8px;cursor:pointer;flex-shrink:0;transition:background .15s}
.edit-btn:active{background:var(--border)}

/* 確認カレンダー（提出前）*/
.confirm-cal-wrap{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:16px;margin-bottom:16px}
.confirm-cal-title{font-size:12px;font-weight:700;color:var(--text-muted);letter-spacing:.08em;margin-bottom:12px}
.confirm-cal-hint{font-size:12px;color:var(--text-hint);margin-top:4px;text-align:center}

/* 成功画面 */
.success-wrap{text-align:center;padding:16px 0 8px}
.success-circle{width:72px;height:72px;border-radius:50%;background:var(--success-bg);display:flex;align-items:center;justify-content:center;margin:0 auto 20px;font-size:34px}
.success-title{font-size:22px;font-weight:700;margin-bottom:8px}
.success-sub{font-size:14px;color:var(--text-muted);line-height:1.7}

/* 底部ボタン */
.bottom-actions{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:480px;background:rgba(245,244,240,.92);backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);padding:14px 20px 28px;border-top:1px solid var(--border);display:flex;gap:10px}
.btn-back{flex:0 0 auto;padding:0 18px;height:52px;border:1px solid var(--border-strong);border-radius:var(--radius);background:var(--surface);cursor:pointer;font-size:14px;color:var(--text-muted);font-family:'Noto Sans JP',sans-serif;transition:background .15s}
.btn-back:active{background:var(--bg)}
.btn-next{flex:1;height:52px;border:none;border-radius:var(--radius);background:var(--text);color:var(--surface);cursor:pointer;font-size:16px;font-weight:700;font-family:'Noto Sans JP',sans-serif;transition:opacity .15s;letter-spacing:.02em}
.btn-next:disabled{opacity:.3;cursor:not-allowed}
.btn-next:not(:disabled):active{opacity:.8}

.deadline-banner{background:#FFF8E6;border:1px solid #F0D48A;border-radius:var(--radius);padding:12px 14px;margin-bottom:16px;display:flex;gap:10px;align-items:flex-start}
.deadline-icon{font-size:18px;flex-shrink:0}
.deadline-text{font-size:13px;color:#7A4F00;line-height:1.6;font-weight:500}

/* 凡例 */
.legend-wrap{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px;margin-bottom:4px}
.legend-item{display:inline-flex;align-items:center;gap:4px;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:500}

/* 締め切り後 */
.closed-screen{text-align:center;padding:48px 0 24px}
.closed-icon{width:80px;height:80px;border-radius:50%;background:#FFF0EE;display:flex;align-items:center;justify-content:center;margin:0 auto 20px;font-size:38px}
.closed-title{font-size:20px;font-weight:700;margin-bottom:12px}
.closed-msg{font-size:14px;color:var(--text-muted);line-height:1.8;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:16px;margin-top:8px;text-align:left}

/* 履歴カレンダー（締め切り後） */
.history-cal-section{margin-top:24px;padding:0 20px 40px}
.history-cal-title{font-size:13px;font-weight:700;color:var(--text-muted);margin-bottom:12px}
</style>
</head>
<body>
<div class="app">

  <!-- 締め切り後 -->
  <div id="closedScreen" style="display:none;padding:24px 20px">
    <div class="closed-screen">
      <div class="closed-icon">🔒</div>
      <p class="closed-title">申請期間が終了しました</p>
      <div class="closed-msg">休み希望申請は<strong>15日まで</strong>です。<br><br>変更や追加は<strong>管理者に直接</strong>お願い致します。</div>
    </div>
    <!-- 締め切り後も履歴をカレンダーで確認 -->
    <div class="history-cal-section" style="padding:0">
      <p class="history-cal-title">📅 申請済みカレンダー</p>
      <div class="cal-nav">
        <button class="cal-nav-btn" onclick="prevHistoryCal()">‹</button>
        <span class="cal-month-label" id="historyCalLabel"></span>
        <button class="cal-nav-btn" onclick="nextHistoryCal()">›</button>
      </div>
      <div class="cal-head">
        <div class="cal-hd sun">日</div><div class="cal-hd">月</div><div class="cal-hd">火</div>
        <div class="cal-hd">水</div><div class="cal-hd">木</div><div class="cal-hd">金</div>
        <div class="cal-hd sat">土</div>
      </div>
      <div class="cal-days" id="historyCalDays"></div>
      <div class="legend-wrap" id="historyCalLegend"></div>
    </div>
  </div>

  <div id="mainApp">
  <div class="header">
    <div class="header-title">希望申請フォーム</div>
    <div class="header-sub" id="headerSub">2026年 シフト</div>
    <div class="progress-wrap" id="progressWrap">
      <div class="prog-seg" id="ps0"></div><div class="prog-seg" id="ps1"></div>
      <div class="prog-seg" id="ps2"></div><div class="prog-seg" id="ps3"></div>
    </div>
  </div>

  <div class="content">

    <!-- Step 0: 名前 -->
    <div class="step active" id="step0">
      <p class="step-label">step 1 / 4</p>
      <h1 class="step-title">お名前を<br>選んでください</h1>
      <p class="step-desc">あなたの名前をタップしてください</p>
      <div class="emp-grid" id="empGrid"></div>
    </div>

    <!-- Step 1: 日付（名前選択後 → カレンダーに履歴表示） -->
    <div class="step" id="step1">
      <p class="step-label">step 2 / 4</p>
      <h1 class="step-title">希望日を<br>選んでください</h1>
      <p class="step-desc">希望日をタップして選択してください</p>
      <div class="deadline-banner">
        <span class="deadline-icon">⚠️</span>
        <span class="deadline-text">申請期間は毎月<strong>1日〜15日</strong>です。<br>16日以降の変更・追加は管理者に直接お願い致します。</span>
      </div>
      <div class="cal-nav">
        <button class="cal-nav-btn" onclick="prevCalMonth()" style="opacity:.2;cursor:default">‹</button>
        <span class="cal-month-label" id="calMonthLabel"></span>
        <button class="cal-nav-btn" onclick="nextCalMonth()" style="opacity:.2;cursor:default">›</button>
      </div>
      <div class="cal-head">
        <div class="cal-hd sun">日</div><div class="cal-hd">月</div><div class="cal-hd">火</div>
        <div class="cal-hd">水</div><div class="cal-hd">木</div><div class="cal-hd">金</div>
        <div class="cal-hd sat">土</div>
      </div>
      <div class="cal-days" id="calDays"></div>
      <div class="chip-wrap" id="chipWrap"></div>
      <p class="chip-hint" id="chipHint">日付をタップして選択</p>
      <!-- 履歴の凡例 -->
      <div class="legend-wrap" id="calLegend"></div>
    </div>

    <!-- Step 2: 種別 -->
    <div class="step" id="step2">
      <p class="step-label">step 3 / 4</p>
      <h1 class="step-title">申請の種類を<br>選んでください</h1>
      <p class="step-desc">休み希望、またはご希望のシフトを選んでください</p>
      <p class="type-section-label">休み希望</p>
      <div class="off-card" id="offCard1" onclick="selOff(1)">
        <div class="off-icon">🌙</div>
        <div style="flex:1">
          <div class="off-text-main">休み希望</div>
          <div class="off-text-sub">この日は休みたい</div>
          <div class="time-range-wrap" id="timeRangeWrap1" onclick="event.stopPropagation()">
            <p style="font-size:12px;font-weight:700;color:var(--off-text);margin-bottom:8px">⏰ 時間帯を指定する場合（任意）</p>
            <div class="time-range-row">
              <select id="offStart1" onchange="updateOffLabel(1)"><option>終日</option><option>8:00</option><option>8:30</option><option>9:00</option><option>9:30</option><option>10:00</option><option>10:30</option><option>11:00</option><option>11:30</option><option>12:00</option><option>12:30</option><option>13:00</option><option>13:30</option><option>14:00</option><option>14:30</option><option>15:00</option><option>15:30</option></select>
              <div class="time-sep">〜</div>
              <select id="offEnd1" onchange="updateOffLabel(1)"><option>終日</option><option>12:00</option><option>12:30</option><option>13:00</option><option>13:30</option><option>14:00</option><option>14:30</option><option>15:00</option><option>15:30</option><option>16:00</option><option>16:30</option><option>17:00</option><option>17:30</option><option>18:00</option><option>18:30</option><option>19:00</option></select>
            </div>
            <p class="time-hint" id="offTimeHint1">終日お休み</p>
          </div>
        </div>
      </div>
      <div class="off-card" id="offCard2" onclick="selOff(2)" style="--off-bg:#FFF8E6;--off-text:#7A4F00;--off-border:#F0D48A;border-color:#F0D48A;">
        <div class="off-icon" style="background:#FFF8E6">🌤️</div>
        <div style="flex:1">
          <div class="off-text-main" style="color:#7A4F00">できれば休み希望</div>
          <div class="off-text-sub">可能なら休みにしてほしい</div>
          <div class="time-range-wrap" id="timeRangeWrap2" onclick="event.stopPropagation()" style="border-top-color:#F0D48A">
            <p style="font-size:12px;font-weight:700;color:#7A4F00;margin-bottom:8px">⏰ 時間帯を指定する場合（任意）</p>
            <div class="time-range-row">
              <select id="offStart2" onchange="updateOffLabel(2)"><option>終日</option><option>8:00</option><option>8:30</option><option>9:00</option><option>9:30</option><option>10:00</option><option>10:30</option><option>11:00</option><option>11:30</option><option>12:00</option><option>12:30</option><option>13:00</option><option>13:30</option><option>14:00</option><option>14:30</option><option>15:00</option><option>15:30</option></select>
              <div class="time-sep">〜</div>
              <select id="offEnd2" onchange="updateOffLabel(2)"><option>終日</option><option>12:00</option><option>12:30</option><option>13:00</option><option>13:30</option><option>14:00</option><option>14:30</option><option>15:00</option><option>15:30</option><option>16:00</option><option>16:30</option><option>17:00</option><option>17:30</option><option>18:00</option><option>18:30</option><option>19:00</option></select>
            </div>
            <p class="time-hint" id="offTimeHint2" style="color:#7A4F00">終日（できれば）</p>
          </div>
        </div>
      </div>
      <p class="type-section-label">シフト希望</p>
      <div class="shift-grid">
        <div class="shift-card" data-shift="○" onclick="selShift(this,'○','早番','9:30〜17:30','7.5h')"><div class="shift-sym">○</div><div class="shift-name">早番</div><div class="shift-time">9:30 – 17:30</div><div class="shift-h">7.5h</div></div>
        <div class="shift-card" data-shift="●" onclick="selShift(this,'●','遅番','12:00〜19:00','7.5h')"><div class="shift-sym">●</div><div class="shift-name">遅番</div><div class="shift-time">12:00 – 19:00</div><div class="shift-h">7.5h</div></div>
        <div class="shift-card" data-shift="☆" onclick="selShift(this,'☆','午前のみ','9:30〜14:00','4.5h')"><div class="shift-sym">☆</div><div class="shift-name">午前のみ</div><div class="shift-time">9:30 – 14:00</div><div class="shift-h">4.5h</div></div>
        <div class="shift-card" data-shift="★" onclick="selShift(this,'★','午後のみ','14:00〜19:00','5.0h')"><div class="shift-sym">★</div><div class="shift-name">午後のみ</div><div class="shift-time">14:00 – 19:00</div><div class="shift-h">5.0h</div></div>
      </div>
    </div>

    <!-- Step 3: 確認（カレンダー付き・日付タップで変更可） -->
    <div class="step" id="step3">
      <p class="step-label">step 4 / 4</p>
      <h1 class="step-title">内容を確認して<br>申請してください</h1>

      <!-- 確認カレンダー：日付タップで日付ステップへ -->
      <div class="confirm-cal-wrap">
        <p class="confirm-cal-title">📅 希望日（タップで変更）</p>
        <div class="cal-head">
          <div class="cal-hd sun">日</div><div class="cal-hd">月</div><div class="cal-hd">火</div>
          <div class="cal-hd">水</div><div class="cal-hd">木</div><div class="cal-hd">金</div>
          <div class="cal-hd sat">土</div>
        </div>
        <div class="cal-days" id="confirmCalDays"></div>
        <p class="confirm-cal-hint">選択中の日付をタップして外す、または空白をタップして追加できます</p>
      </div>

      <div class="confirm-card">
        <div class="confirm-row">
          <span class="c-label">名前</span>
          <span class="c-val" id="cfName">—</span>
        </div>
        <div class="confirm-row">
          <span class="c-label">希望日</span>
          <span class="c-val" id="cfDates" style="font-size:13px;font-family:'DM Mono',monospace">—</span>
          <button class="edit-btn" onclick="editDates()">変更</button>
        </div>
        <div class="confirm-row" style="border-bottom:none">
          <span class="c-label">種別</span>
          <span class="c-val" id="cfType">—</span>
          <button class="edit-btn" onclick="editType()">変更</button>
        </div>
      </div>
      <p style="font-size:13px;font-weight:700;margin-bottom:8px;color:var(--text-muted)">備考（任意）</p>
      <textarea class="note-area" id="noteField" placeholder="例：午前中は通院のため、午後から出勤希望　など"></textarea>
    </div>

    <!-- Step 4: 申請完了 -->
    <div class="step" id="step4">
      <div class="success-wrap">
        <div class="success-circle">✓</div>
        <p class="success-title">申請完了！</p>
        <p class="success-sub">管理者が確認後、<br>シフトに反映されます。</p>
      </div>
      <div class="confirm-card" style="margin-top:20px">
        <div class="confirm-row"><span class="c-label">名前</span><span class="c-val" id="cfName2">—</span></div>
        <div class="confirm-row"><span class="c-label">希望日</span><span class="c-val" id="cfDates2" style="font-size:13px;font-family:'DM Mono',monospace">—</span></div>
        <div class="confirm-row" style="border-bottom:none"><span class="c-label">種別</span><span class="c-val" id="cfType2">—</span></div>
      </div>
      <p style="font-size:13px;font-weight:700;text-align:center;margin:24px 0 12px;color:var(--text-muted)">次はどうしますか？</p>
      <button class="btn-next" style="margin-bottom:10px" onclick="continueInput()">続けて入力する</button>
      <button class="btn-next" style="background:var(--surface);color:var(--text);border:1.5px solid var(--border-strong)" onclick="showReview()">申請を確認する</button>
    </div>

    <!-- Step 5: 申請確認カレンダー -->
    <div class="step" id="step5">
      <p class="step-label">申請確認</p>
      <h1 class="step-title">申請内容の確認</h1>
      <p class="step-desc">今回の申請をカレンダーで確認できます</p>
      <div class="cal-nav">
        <button class="cal-nav-btn" onclick="prevReviewMonth()">‹</button>
        <span class="cal-month-label" id="reviewMonthLabel"></span>
        <button class="cal-nav-btn" onclick="nextReviewMonth()">›</button>
      </div>
      <div class="cal-head">
        <div class="cal-hd sun">日</div><div class="cal-hd">月</div><div class="cal-hd">火</div>
        <div class="cal-hd">水</div><div class="cal-hd">木</div><div class="cal-hd">金</div>
        <div class="cal-hd sat">土</div>
      </div>
      <div class="cal-days" id="reviewCalDays"></div>
      <div class="legend-wrap" id="reviewLegend"></div>
      <p style="font-size:13px;font-weight:700;text-align:center;margin:24px 0 12px;color:var(--text-muted)">次はどうしますか？</p>
      <button class="btn-next" style="margin-bottom:10px" onclick="continueInput()">続けて入力する</button>
      <button class="btn-next" style="background:var(--surface);color:var(--text);border:1.5px solid var(--border-strong)" onclick="finishAll()">申請を終了する</button>
    </div>

    <!-- Step 6: 終了 -->
    <div class="step" id="step6">
      <div class="success-wrap" style="padding:40px 0">
        <div class="success-circle">🎉</div>
        <p class="success-title">お疲れさまでした！</p>
        <p class="success-sub">すべての申請が完了しました。<br>管理者が確認後、<br>シフトに反映されます。</p>
      </div>
    </div>

  </div>

  <div class="bottom-actions" id="bottomActions">
    <button class="btn-back" id="btnBack" onclick="goBack()" style="display:none">← 戻る</button>
    <button class="btn-next" id="btnNext" onclick="goNext()" disabled>名前を選んでください</button>
  </div>
  </div><!-- /mainApp -->
</div>

<script>
// ── 締め切りチェック ──
(function(){
  const d = new Date().getDate();
  if(d >= 16){
    document.getElementById('closedScreen').style.display='block';
    document.getElementById('mainApp').style.display='none';
    initHistoryCal();
  }
})();

const EMPLOYEES   = ['佐藤','鈴木','田中','高橋'];
const WEEKDAYS    = ['日','月','火','水','木','金','土'];
const STORAGE_KEY = 'shiftAppHistory_v2';

// 申請種別ごとの色定義
const SYM_COLORS = {
  '○':{ bg:'#EBF3FF', fg:'#1A5FA8' },
  '●':{ bg:'#FFF4E6', fg:'#8B4F00' },
  '☆':{ bg:'#EDFAF3', fg:'#0D6B45' },
  '★':{ bg:'#FFF0EE', fg:'#8B2500' },
  '休':{ bg:'#F5EEFF', fg:'#4A1D8B' },
  '△':{ bg:'#FFF8E6', fg:'#7A4F00' },
};
const SYM_NAMES = { '○':'早番','●':'遅番','☆':'午前','★':'午後','休':'休み希望','△':'できれば休み' };

let currentStep  = 0;
let selEmpName   = '';
let selDates     = [];   // 現在入力中の選択日付
let selType      = '';
let selTypeLabel = '';

const _today = new Date();
let calYear  = _today.getMonth()===11 ? _today.getFullYear()+1 : _today.getFullYear();
let calMonth = _today.getMonth()===11 ? 1 : _today.getMonth()+2;
const NEXT_YEAR=calYear, NEXT_MONTH=calMonth;
let reviewYear=calYear, reviewMonth=calMonth;
let historyCalYear=calYear, historyCalMonth=calMonth;

// セッション内申請済みエントリ
let submittedEntries = [];

// ── localStorage ──
function loadHistory(){ try{ return JSON.parse(localStorage.getItem(STORAGE_KEY)||'[]'); }catch(e){ return []; } }
function saveToHistory(entry){
  const h=loadHistory(); h.unshift(entry);
  if(h.length>100) h.splice(100);
  localStorage.setItem(STORAGE_KEY,JSON.stringify(h));
}

// 名前でフィルタした履歴をキー(YYYY-MM-DD)→シンボルのマップで返す
function getHistoryMapForName(name){
  const map={};
  loadHistory().filter(function(item){ return item.name===name; }).forEach(function(item){
    (item.keys||[]).forEach(function(key){
      if(!map[key]) map[key]={ sym: item.sym, label: item.type };
    });
  });
  return map;
}

function typeToSym(type){
  if(!type) return '';
  if(type.includes('○')) return '○';
  if(type.includes('●')) return '●';
  if(type.includes('☆')) return '☆';
  if(type.includes('★')) return '★';
  if(type.includes('できれば')) return '△';
  if(type.includes('休')) return '休';
  return '済';
}

// ── 従業員ボタン ──
const empGrid=document.getElementById('empGrid');
EMPLOYEES.forEach(function(name){
  const btn=document.createElement('div');
  btn.className='emp-btn'; btn.textContent=name;
  btn.onclick=function(){
    document.querySelectorAll('.emp-btn').forEach(function(b){ b.classList.remove('selected'); });
    btn.classList.add('selected');
    selEmpName=name;
    updateNextBtn();
  };
  empGrid.appendChild(btn);
});

// ── Progress ──
function updateProgress(){
  for(let i=0;i<4;i++){
    const s=document.getElementById('ps'+i);
    s.className='prog-seg';
    if(i<currentStep) s.classList.add('done');
    else if(i===currentStep) s.classList.add('active');
  }
}
function updateNextBtn(){
  const btn=document.getElementById('btnNext');
  const back=document.getElementById('btnBack');
  const bottom=document.getElementById('bottomActions');
  if(currentStep>=4){ bottom.style.display='none'; return; }
  bottom.style.display='flex';
  back.style.display=currentStep>0?'block':'none';
  const labels=['名前を選んでください','日付を選んでください','種類を選んでください','申請する →'];
  btn.textContent=labels[currentStep];
  if(currentStep===0)      btn.disabled=!selEmpName;
  else if(currentStep===1) btn.disabled=selDates.length===0;
  else if(currentStep===2) btn.disabled=!selType;
  else                     btn.disabled=false;
}
function goNext(){ if(currentStep===3){ submit(); return; } currentStep++; showStep(); }
function goBack(){ if(currentStep>0&&currentStep<4){ currentStep--; showStep(); } }
function editDates(){ currentStep=1; showStep(); }
function editType(){  currentStep=2; showStep(); }

function showStep(){
  document.querySelectorAll('.step').forEach(function(s,i){ s.classList.toggle('active',i===currentStep); });
  updateProgress(); updateNextBtn();
  if(currentStep===1) renderCal();
  if(currentStep===3) fillConfirm();
  if(currentStep===5) renderReviewCal();
  window.scrollTo(0,0);
}

// ── Step1 カレンダー(履歴を色付き表示) ──
function renderCal(){
  document.getElementById('calMonthLabel').textContent=calYear+'年'+calMonth+'月';
  const firstDay=new Date(calYear,calMonth-1,1).getDay();
  const dim=new Date(calYear,calMonth,0).getDate();
  const today=new Date();
  const histMap=getHistoryMapForName(selEmpName); // 履歴マップ
  let html='';
  for(let i=0;i<firstDay;i++) html+='<div class="cal-d empty"></div>';
  for(let d=1;d<=dim;d++){
    const date=new Date(calYear,calMonth-1,d);
    const dow=date.getDay();
    const key=calYear+'-'+pad(calMonth)+'-'+pad(d);
    const isPast=date<new Date(today.getFullYear(),today.getMonth(),today.getDate());
    const isSel=selDates.includes(key);
    const sessionSubmitted=submittedEntries.find(function(e){ return e.key===key; });
    const histEntry=histMap[key];

    let cls='cal-d';
    if(dow===0) cls+=' sun';
    if(dow===6) cls+=' sat';
    let style='', inner=''+d, onclick='';

    if(sessionSubmitted && !isSel){
      // セッション内提出済み(変更不可)
      cls+=' submitted';
      inner=d+'<span style="font-size:9px;display:block;line-height:1">'+sessionSubmitted.sym+'</span>';
    } else if(histEntry && !isSel && !sessionSubmitted){
      // 履歴あり(タップして新規選択可能)
      const c=SYM_COLORS[histEntry.sym]||{bg:'#eee',fg:'#555'};
      style='background:'+c.bg+';border-radius:6px;';
      inner='<span style="font-size:12px;font-weight:700;color:'+c.fg+';display:block;line-height:1.3">'+d+'</span>'
           +'<span style="font-size:9px;color:'+c.fg+';display:block;line-height:1">'+histEntry.sym+'</span>';
      onclick=isPast ? '' : 'onclick="toggleDate(\''+key+'\')"';
    } else if(isSel){
      cls+=' selected';
      if(isPast) cls+=' past';
      onclick='onclick="toggleDate(\''+key+'\')"';
    } else if(isPast){
      cls+=' past';
    } else {
      onclick='onclick="toggleDate(\''+key+'\')"';
    }

    html+='<div class="'+cls+'" '+onclick+' style="'+style+'">'+inner+'</div>';
  }
  document.getElementById('calDays').innerHTML=html;
  renderChips();
  renderCalLegend(histMap);
}

function renderCalLegend(histMap){
  const syms=[...new Set(Object.values(histMap).map(function(e){ return e.sym; }))];
  const leg=document.getElementById('calLegend');
  if(!leg) return;
  if(syms.length===0){ leg.innerHTML=''; return; }
  leg.innerHTML='<span style="font-size:11px;color:var(--text-hint);width:100%">過去の申請：</span>'
    +syms.map(function(sym){
      const c=SYM_COLORS[sym]||{bg:'#eee',fg:'#555'};
      return '<span class="legend-item" style="background:'+c.bg+';color:'+c.fg+'">'+sym+' '+(SYM_NAMES[sym]||'')+'</span>';
    }).join('');
}

function toggleDate(key){
  const idx=selDates.indexOf(key);
  if(idx>=0) selDates.splice(idx,1); else selDates.push(key);
  selDates.sort();
  renderCal();
  // 確認画面にいる場合も更新
  if(currentStep===3) updateConfirmCal();
  updateNextBtn();
}

function renderChips(){
  const wrap=document.getElementById('chipWrap');
  const hint=document.getElementById('chipHint');
  if(selDates.length===0){ wrap.innerHTML=''; hint.style.display='block'; return; }
  hint.style.display='none';
  wrap.innerHTML=selDates.map(function(k){
    const p=k.split('-');
    const dow=new Date(+p[0],+p[1]-1,+p[2]).getDay();
    return '<div class="chip">'+(+p[1])+'/'+(+p[2])+'('+WEEKDAYS[dow]+')<span class="chip-x" onclick="removeDate(\''+k+'\')">×</span></div>';
  }).join('');
}

function removeDate(key){
  selDates=selDates.filter(function(d){ return d!==key; });
  renderCal();
  if(currentStep===3) updateConfirmCal();
  updateNextBtn();
}

function pad(n){ return String(n).padStart(2,'0'); }
function prevCalMonth(){} function nextCalMonth(){}

// ── Step3 確認カレンダー(タップで日付変更) ──
function updateConfirmCal(){
  const firstDay=new Date(calYear,calMonth-1,1).getDay();
  const dim=new Date(calYear,calMonth,0).getDate();
  const today=new Date();
  let html='';
  for(let i=0;i<firstDay;i++) html+='<div class="cal-d empty"></div>';
  for(let d=1;d<=dim;d++){
    const date=new Date(calYear,calMonth-1,d);
    const dow=date.getDay();
    const key=calYear+'-'+pad(calMonth)+'-'+pad(d);
    const isPast=date<new Date(today.getFullYear(),today.getMonth(),today.getDate());
    const isSel=selDates.includes(key);
    const sessionSubmitted=submittedEntries.find(function(e){ return e.key===key; });
    let cls='cal-d', style='', inner=''+d, onclick='';
    if(dow===0) cls+=' sun';
    if(dow===6) cls+=' sat';
    if(sessionSubmitted && !isSel){
      cls+=' submitted';
      inner=d+'<span style="font-size:9px;display:block;line-height:1">'+sessionSubmitted.sym+'</span>';
    } else if(isSel){
      cls+=' selected';
      onclick='onclick="toggleDate(\''+key+'\')"';
    } else if(isPast){
      cls+=' past';
    } else {
      onclick='onclick="toggleDate(\''+key+'\')"';
    }
    html+='<div class="'+cls+'" '+onclick+' style="'+style+'">'+inner+'</div>';
  }
  document.getElementById('confirmCalDays').innerHTML=html;
  // cfDatesも更新
  document.getElementById('cfDates').textContent=selDates.map(function(k){
    const p=k.split('-');
    return (+p[1])+'/'+(+p[2])+'('+WEEKDAYS[new Date(+p[0],+p[1]-1,+p[2]).getDay()]+')';
  }).join('  ')||'—';
  updateNextBtn();
}

// ── Off cards ──
function selOff(n){
  document.querySelectorAll('.shift-card').forEach(function(c){ c.classList.remove('selected'); });
  document.getElementById('offCard'+n).classList.toggle('selected');
  updateOffLabel(n);
  syncType();
  updateNextBtn();
}
function syncType(){
  const s1=document.getElementById('offCard1').classList.contains('selected');
  const s2=document.getElementById('offCard2').classList.contains('selected');
  if(s1&&s2){ selType='休+希望'; selTypeLabel=_offLabel(1)+' ／ '+_offLabel(2); }
  else if(s1){ selType='休'; selTypeLabel=_offLabel(1); }
  else if(s2){ selType='希望休'; selTypeLabel=_offLabel(2); }
  else { selType=''; selTypeLabel=''; }
}
function _offLabel(n){
  const s=document.getElementById('offStart'+n).value;
  const e=document.getElementById('offEnd'+n).value;
  const pre=n===1?'休み希望':'できれば休み希望';
  return (s==='終日'||e==='終日') ? pre+'(終日)' : pre+'('+s+'〜'+e+')';
}
function updateOffLabel(n){
  const hint=document.getElementById('offTimeHint'+n);
  const s=document.getElementById('offStart'+n).value;
  const e=document.getElementById('offEnd'+n).value;
  const suf=n===2?'(できれば)':'';
  hint.textContent=(s==='終日'||e==='終日')?'終日お休み'+suf:s+' 〜 '+e+suf;
  syncType();
}
function selShift(el,val,name,time,hours){
  document.getElementById('offCard1').classList.remove('selected');
  document.getElementById('offCard2').classList.remove('selected');
  document.querySelectorAll('.shift-card').forEach(function(c){ c.classList.remove('selected'); });
  el.classList.add('selected');
  selType=val;
  selTypeLabel=val+' '+name+'('+time+' / '+hours+')';
  updateNextBtn();
}

// ── Confirm ──
function fillConfirm(){
  document.getElementById('cfName').textContent=selEmpName;
  document.getElementById('cfType').textContent=selTypeLabel;
  updateConfirmCal();
}

// ── Submit ──
function submit(){
  const fmt=selDates.map(function(k){
    const p=k.split('-');
    return (+p[1])+'/'+(+p[2])+'('+WEEKDAYS[new Date(+p[0],+p[1]-1,+p[2]).getDay()]+')';
  }).join('  ');

  document.getElementById('cfName2').textContent=selEmpName;
  document.getElementById('cfDates2').textContent=fmt;
  document.getElementById('cfType2').textContent=selTypeLabel;

  const sym=typeToSym(selTypeLabel);
  selDates.forEach(function(key){
    if(!submittedEntries.find(function(e){ return e.key===key; }))
      submittedEntries.push({ key:key, label:selTypeLabel, sym:sym });
  });

  // localStorage保存(keysも一緒に保存)
  saveToHistory({
    name: selEmpName, dates: fmt, type: selTypeLabel,
    sym: sym, keys: selDates.slice(),
    note: document.getElementById('noteField').value||'',
    submittedAt: new Date().toISOString(),
  });

  currentStep=4; showStep();

  // GAS送信 — datesはISO形式カンマ区切り(例: 2026-07-06,2026-07-07)
  const datesISO = selDates.join(',');
  const s1=document.getElementById('offCard1').classList.contains('selected');
  const s2=document.getElementById('offCard2').classList.contains('selected');
  const os1=document.getElementById('offStart1').value, oe1=document.getElementById('offEnd1').value;
  const os2=document.getElementById('offStart2').value, oe2=document.getElementById('offEnd2').value;
  let timeRange='---';
  if(s1||s2){
    const t1=(os1==='終日'||oe1==='終日')?'終日':os1+'-'+oe1;
    const t2=(os2==='終日'||oe2==='終日')?'終日':os2+'-'+oe2;
    if(s1&&s2) timeRange=t1+' / '+t2+'(できれば)';
    else if(s1) timeRange=t1;
    else timeRange=t2+'(できれば)';
  }
  fetch('https://script.google.com/macros/s/AKfycbx3dSEA83QIAIH-WM-qSgC56kbHadQzBbjGoiuzTL50Pol-nPVGtA8IS3Cr09X4QM_1/exec',{
    method:'POST', mode:'no-cors', headers:{'Content-Type':'application/json'},
    body:JSON.stringify({ name:selEmpName, dates:datesISO, type:selTypeLabel, timeRange:timeRange, note:document.getElementById('noteField').value||'' }),
  }).catch(function(){});
}

// ── 続けて入力 ──
function continueInput(){
  selDates=[]; selType=''; selTypeLabel='';
  document.querySelectorAll('.shift-card').forEach(function(c){ c.classList.remove('selected'); });
  document.getElementById('offCard1').classList.remove('selected');
  document.getElementById('offCard2').classList.remove('selected');
  document.getElementById('noteField').value='';
  ['offStart1','offEnd1','offStart2','offEnd2'].forEach(function(id){ document.getElementById(id).value='終日'; });
  updateOffLabel(1); updateOffLabel(2);
  currentStep=1; showStep();
}
function showReview(){ currentStep=5; showStep(); }

// ── Review Calendar ──
function renderReviewCal(){
  document.getElementById('reviewMonthLabel').textContent=reviewYear+'年'+reviewMonth+'月';
  const firstDay=new Date(reviewYear,reviewMonth-1,1).getDay();
  const dim=new Date(reviewYear,reviewMonth,0).getDate();
  let html='';
  for(let i=0;i<firstDay;i++) html+='<div class="cal-d empty"></div>';
  for(let d=1;d<=dim;d++){
    const dow=new Date(reviewYear,reviewMonth-1,d).getDay();
    const key=reviewYear+'-'+pad(reviewMonth)+'-'+pad(d);
    const entry=submittedEntries.find(function(e){ return e.key===key; });
    let cls='cal-d', style='', inner=''+d;
    if(dow===0) cls+=' sun'; if(dow===6) cls+=' sat';
    if(entry){
      const c=SYM_COLORS[entry.sym]||{bg:'#F0F0F0',fg:'#555'};
      style='background:'+c.bg+';border-radius:6px;';
      inner='<span style="font-size:12px;font-weight:700;color:'+c.fg+';display:block;line-height:1.2">'+d+'</span>'
           +'<span style="font-size:9px;color:'+c.fg+';display:block;line-height:1">'+entry.sym+'</span>';
    }
    html+='<div class="'+cls+'" style="'+style+'">'+inner+'</div>';
  }
  document.getElementById('reviewCalDays').innerHTML=html;
  const used=[...new Set(submittedEntries.filter(function(e){
    const p=e.key.split('-'); return +p[0]===reviewYear&&+p[1]===reviewMonth;
  }).map(function(e){ return e.sym; }))];
  document.getElementById('reviewLegend').innerHTML=used.map(function(sym){
    const c=SYM_COLORS[sym]||{bg:'#eee',fg:'#555'};
    return '<span class="legend-item" style="background:'+c.bg+';color:'+c.fg+'">'+sym+' '+(SYM_NAMES[sym]||'')+'</span>';
  }).join('');
}
function prevReviewMonth(){ if(reviewMonth>1) reviewMonth--; else{ reviewYear--; reviewMonth=12; } renderReviewCal(); }
function nextReviewMonth(){ if(reviewMonth<12) reviewMonth++; else{ reviewYear++; reviewMonth=1; } renderReviewCal(); }

// ── 終了 ──
function finishAll(){
  submittedEntries=[];
  selEmpName=''; selDates=[]; selType=''; selTypeLabel='';
  calYear=NEXT_YEAR; calMonth=NEXT_MONTH;
  document.querySelectorAll('.emp-btn').forEach(function(b){ b.classList.remove('selected'); });
  document.querySelectorAll('.shift-card').forEach(function(c){ c.classList.remove('selected'); });
  document.getElementById('offCard1').classList.remove('selected');
  document.getElementById('offCard2').classList.remove('selected');
  document.getElementById('noteField').value='';
  ['offStart1','offEnd1','offStart2','offEnd2'].forEach(function(id){ document.getElementById(id).value='終日'; });
  updateOffLabel(1); updateOffLabel(2);
  currentStep=6; showStep();
}

// ── 締め切り後の履歴カレンダー ──
function initHistoryCal(){
  renderHistoryCal();
}
function renderHistoryCal(){
  document.getElementById('historyCalLabel').textContent=historyCalYear+'年'+historyCalMonth+'月';
  const history=loadHistory();
  // 全員の履歴をマップ化
  const map={};
  history.forEach(function(item){
    (item.keys||[]).forEach(function(key){
      const p=key.split('-');
      if(+p[0]===historyCalYear&&+p[1]===historyCalMonth){
        if(!map[key]) map[key]=[];
        map[key].push({ name:item.name, sym:item.sym||typeToSym(item.type) });
      }
    });
  });
  const firstDay=new Date(historyCalYear,historyCalMonth-1,1).getDay();
  const dim=new Date(historyCalYear,historyCalMonth,0).getDate();
  let html='';
  for(let i=0;i<firstDay;i++) html+='<div class="cal-d empty"></div>';
  for(let d=1;d<=dim;d++){
    const dow=new Date(historyCalYear,historyCalMonth-1,d).getDay();
    const key=historyCalYear+'-'+pad(historyCalMonth)+'-'+pad(d);
    const entries=map[key];
    let cls='cal-d', style='', inner=''+d;
    if(dow===0) cls+=' sun'; if(dow===6) cls+=' sat';
    if(entries&&entries.length>0){
      const sym=entries[0].sym;
      const c=SYM_COLORS[sym]||{bg:'#eee',fg:'#555'};
      style='background:'+c.bg+';border-radius:6px;';
      const names=entries.map(function(e){ return e.name; }).join(',');
      inner='<span style="font-size:11px;font-weight:700;color:'+c.fg+';display:block;line-height:1.3">'+d+'</span>'
           +'<span style="font-size:8px;color:'+c.fg+';display:block;line-height:1.1;overflow:hidden;max-width:100%">'+names+'</span>';
    }
    html+='<div class="'+cls+'" style="'+style+'">'+inner+'</div>';
  }
  document.getElementById('historyCalDays').innerHTML=html;
  // 凡例
  const usedSyms=[...new Set(Object.values(map).flat().map(function(e){ return e.sym; }))];
  document.getElementById('historyCalLegend').innerHTML=usedSyms.map(function(sym){
    const c=SYM_COLORS[sym]||{bg:'#eee',fg:'#555'};
    return '<span class="legend-item" style="background:'+c.bg+';color:'+c.fg+'">'+sym+' '+(SYM_NAMES[sym]||'')+'</span>';
  }).join('');
}
function prevHistoryCal(){ if(historyCalMonth>1) historyCalMonth--; else{ historyCalYear--; historyCalMonth=12; } renderHistoryCal(); }
function nextHistoryCal(){ if(historyCalMonth<12) historyCalMonth++; else{ historyCalYear++; historyCalMonth=1; } renderHistoryCal(); }

updateProgress();
updateNextBtn();
</script>
</body>
</html>
