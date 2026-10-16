# TEST
TEST
<!doctype html>
<html lang="zh-HK">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#f4f3ed">
  <title>現場圖記 | PlanPin</title>
  <style>
    :root {
      color-scheme: light;
      --paper: #f4f3ed;
      --panel: #fffefa;
      --ink: #252923;
      --muted: #7d8178;
      --line: #e4e5dc;
      --green: #2c5848;
      --green-soft: #e8eee8;
      --orange: #e16e4d;
      --shadow: 0 12px 32px rgba(39, 48, 39, .08);
    }
    * { box-sizing: border-box; }
    body { margin: 0; min-height: 100vh; background: var(--paper); color: var(--ink); font-family: "Bahnschrift", "Microsoft JhengHei", sans-serif; }
    button, input { font: inherit; }
    button { color: inherit; }
    .topbar { height: 72px; padding: 0 30px; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid var(--line); background: rgba(255,254,250,.88); }
    .brand { display: flex; align-items: center; gap: 12px; }
    .brand-mark { width: 34px; height: 34px; display: grid; place-items: center; border-radius: 10px; color: white; background: var(--green); }
    .brand-mark svg { width: 19px; height: 19px; }
    .brand-name { font-family: Georgia, "Noto Serif TC", serif; font-weight: 700; font-size: 19px; letter-spacing: 0; }
    .brand-caption { margin-left: 10px; padding-left: 13px; border-left: 1px solid var(--line); color: var(--muted); font-size: 12px; }
    .top-actions { display: flex; align-items: center; gap: 14px; }
    .save-state { color: var(--muted); display: flex; align-items: center; gap: 7px; font-size: 12px; }
    .save-dot { width: 7px; height: 7px; border-radius: 50%; background: #73a77d; }
    .avatar { width: 32px; height: 32px; display: grid; place-items: center; border-radius: 50%; background: #e9d8c9; color: #684d3a; font-size: 12px; font-weight: 700; }
    .app-shell { min-height: calc(100vh - 72px); display: grid; grid-template-columns: 310px minmax(0, 1fr); }
    .sidebar { padding: 28px 20px 24px 26px; background: #faf9f4; border-right: 1px solid var(--line); }
    .eyebrow { margin: 0 0 9px; color: var(--muted); font-size: 10px; font-weight: 700; letter-spacing: 1.25px; }
    .site-title { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 25px; }
    .site-title h1 { margin: 0; font-family: Georgia, "Noto Serif TC", serif; font-size: 23px; letter-spacing: 0; font-weight: 600; }
    .more-btn { width: 30px; height: 30px; display: grid; place-items: center; border: 1px solid var(--line); border-radius: 8px; background: white; cursor: pointer; }
    .more-btn svg { width: 17px; height: 17px; }
    .section-row { display: flex; justify-content: space-between; align-items: center; margin: 0 0 11px; }
    .section-title { margin: 0; font-size: 12px; font-weight: 700; }
    .count { color: var(--muted); font-size: 11px; }
    .entry-list { display: grid; gap: 8px; }
    .empty-state { padding: 24px 13px; border: 1px dashed #d5d8ce; border-radius: 8px; color: var(--muted); text-align: center; font-size: 12px; line-height: 1.7; }
    .entry { width: 100%; min-height: 68px; padding: 8px; display: grid; grid-template-columns: 52px minmax(0,1fr) 20px; align-items: center; gap: 11px; border: 1px solid transparent; border-radius: 8px; background: transparent; text-align: left; cursor: pointer; }
    .entry:hover { background: white; }
    .entry.active { border-color: #dce4da; background: white; box-shadow: 0 2px 8px rgba(30,50,34,.04); }
    .entry-thumb { width: 52px; height: 48px; border-radius: 5px; object-fit: cover; background: #e5e6df; }
    .entry-name { display: block; overflow: hidden; color: var(--ink); font-size: 12px; font-weight: 650; text-overflow: ellipsis; white-space: nowrap; }
    .entry-time { display: block; margin-top: 5px; color: var(--muted); font-size: 10px; }
    .entry-index { color: #92968b; font-size: 10px; text-align: right; }
    .sidebar-footer { position: sticky; top: calc(100vh - 76px); margin-top: 28px; padding-top: 16px; border-top: 1px solid var(--line); color: var(--muted); font-size: 10px; line-height: 1.6; }
    .main { min-width: 0; padding: 26px 32px 30px; }
    .main-heading { display: flex; align-items: center; justify-content: space-between; gap: 16px; margin-bottom: 18px; }
    .level-label { display: flex; align-items: center; gap: 10px; }
    .level-label h2 { margin: 0; font-family: Georgia, "Noto Serif TC", serif; font-size: 21px; letter-spacing: 0; font-weight: 600; }
    .floor-panel { min-width: 0; flex: 1; }
    .floor-title-row { display: flex; align-items: center; gap: 9px; }
    .floor-title-row .more-btn { width: 27px; height: 27px; }
    .floor-tabs { min-width: 0; margin-top: 11px; display: flex; align-items: center; gap: 6px; overflow-x: auto; scrollbar-width: thin; }
    .floor-tab { min-height: 31px; padding: 0 11px; border: 1px solid #dfe2d9; border-radius: 5px; background: #fffefa; color: #687066; cursor: pointer; font-size: 11px; white-space: nowrap; }
    .floor-tab[aria-selected="true"] { border-color: #a9b9a8; background: #e8eee8; color: var(--green); font-weight: 700; }
    .floor-add { width: 31px; height: 31px; flex: 0 0 auto; display: grid; place-items: center; border: 1px dashed #c9cec4; border-radius: 5px; background: transparent; color: #647066; cursor: pointer; }
    .floor-add svg { width: 15px; height: 15px; }
    .name-input { width: 100%; min-height: 42px; padding: 0 11px; border: 1px solid #dfe2d9; border-radius: 5px; outline-color: var(--green); background: white; color: var(--ink); font-size: 13px; }
    .level-tag { padding: 5px 8px; border-radius: 4px; background: #e9eee8; color: var(--green); font-size: 10px; font-weight: 700; }
      .pdf-controls { display: flex; align-items: center; gap: 5px; margin-left: 2px; }
      .pdf-controls .tool-btn { min-width: 30px; min-height: 30px; padding: 0 7px; }
      .pdf-page { min-width: 38px; color: var(--muted); font-size: 10px; text-align: center; }
    .main-tools { display: flex; gap: 8px; }
    .tool-btn, .primary-btn { min-height: 38px; padding: 0 12px; display: inline-flex; align-items: center; justify-content: center; gap: 8px; border: 1px solid #dfe2d9; border-radius: 6px; background: var(--panel); color: #42483f; cursor: pointer; font-size: 11px; font-weight: 650; }
    .tool-btn:hover { background: #f8f8f3; }
    .tool-btn svg, .primary-btn svg { width: 16px; height: 16px; }
    .primary-btn { border-color: var(--green); background: var(--green); color: white; }
    .primary-btn:hover { background: #234b3b; }
    .map-surface { min-height: 500px; height: calc(100vh - 190px); max-height: 920px; position: relative; overflow: hidden; display: grid; place-items: center; border: 1px solid #e6e6dd; border-radius: 8px; background-color: #eeeee7; background-image: radial-gradient(#d7d9d0 0.75px, transparent .75px); background-size: 18px 18px; box-shadow: var(--shadow); }
    .plan-empty { width: 100%; height: 100%; padding: 24px; display: grid; place-content: center; justify-items: center; gap: 12px; color: var(--muted); text-align: center; }
    .plan-empty svg { width: 40px; height: 40px; color: #9aa295; }
    .plan-empty strong { color: #434940; font-family: Georgia, "Noto Serif TC", serif; font-size: 19px; font-weight: 600; }
    .plan-empty span { max-width: 270px; font-size: 12px; line-height: 1.7; }
    .plan-stage { position: relative; max-width: 100%; max-height: 100%; display: flex; align-items: center; justify-content: center; }
    .plan-image { display: block; width: auto; height: auto; max-width: 100%; max-height: calc(100vh - 220px); object-fit: contain; user-select: none; -webkit-user-drag: none; }
    .map-surface.placing { cursor: crosshair; }
    .map-surface.placing .plan-image { cursor: crosshair; }
    .pin-layer { position: absolute; inset: 0; pointer-events: none; }
    .pin { position: absolute; width: 32px; height: 38px; transform: translate(-50%, -90%); padding: 0; border: 0; background: none; pointer-events: auto; cursor: pointer; }
    .pin svg { width: 100%; height: 100%; overflow: visible; filter: drop-shadow(0 3px 3px rgba(35,47,38,.22)); }
    .pin .pin-number { fill: white; font-size: 9px; font-family: sans-serif; font-weight: 700; text-anchor: middle; }
    .pin.selected { z-index: 2; transform: translate(-50%, -90%) scale(1.2); }
    .map-toolbar { position: absolute; right: 14px; bottom: 14px; display: flex; gap: 6px; padding: 5px; border: 1px solid rgba(224,225,216,.9); border-radius: 7px; background: rgba(255,254,250,.94); box-shadow: 0 3px 12px rgba(34,39,31,.08); }
    .zoom-btn { width: 30px; height: 30px; display: grid; place-items: center; border: 0; border-radius: 4px; background: transparent; color: #52584f; cursor: pointer; }
    .zoom-btn:hover { background: var(--green-soft); }
    .zoom-btn svg { width: 16px; height: 16px; }
    .map-caption { position: absolute; left: 14px; bottom: 16px; padding: 7px 9px; display: flex; align-items: center; gap: 8px; border: 1px solid rgba(224,225,216,.8); border-radius: 5px; background: rgba(255,254,250,.88); color: #73786f; font-size: 10px; }
    .map-floor-label { color: var(--green); font-weight: 750; white-space: nowrap; }
    .placement-bar { position: absolute; z-index: 5; top: 14px; left: 50%; transform: translateX(-50%); min-height: 46px; padding: 6px 8px 6px 13px; display: flex; align-items: center; gap: 12px; border: 1px solid #dce2d9; border-radius: 7px; background: #fffefa; box-shadow: var(--shadow); white-space: nowrap; }
    .placement-bar span { font-size: 11px; font-weight: 650; }
    .placement-bar img { width: 32px; height: 32px; border-radius: 4px; object-fit: cover; }
    .placement-bar button { min-height: 32px; padding: 0 10px; border: 0; border-radius: 5px; background: var(--green); color: white; cursor: pointer; font-size: 11px; font-weight: 700; }
    .placement-bar button.cancel { background: #f0f0ea; color: #555b51; }
    .toast { position: fixed; z-index: 20; left: 50%; bottom: 24px; transform: translate(-50%, 12px); padding: 10px 15px; border-radius: 6px; background: #273c30; color: white; box-shadow: var(--shadow); font-size: 12px; opacity: 0; pointer-events: none; transition: opacity .18s, transform .18s; }
    .toast.show { transform: translate(-50%, 0); opacity: 1; }
    dialog { width: min(460px, calc(100% - 28px)); padding: 0; border: 1px solid #e2e3db; border-radius: 10px; background: var(--panel); color: var(--ink); box-shadow: 0 24px 80px rgba(21,30,23,.24); }
    dialog::backdrop { background: rgba(28,34,29,.42); backdrop-filter: blur(2px); }
    .dialog-head { padding: 20px 22px 13px; display: flex; justify-content: space-between; align-items: flex-start; }
    .dialog-head h3 { margin: 0; font-family: Georgia, "Noto Serif TC", serif; font-size: 20px; font-weight: 600; }
    .dialog-head p { margin: 6px 0 0; color: var(--muted); font-size: 11px; }
    .close-btn { width: 30px; height: 30px; display: grid; place-items: center; border: 0; border-radius: 5px; background: transparent; color: #6f756b; cursor: pointer; }
    .close-btn:hover { background: #f0f0ea; }
    .close-btn svg { width: 17px; height: 17px; }
    .dialog-body { padding: 8px 22px 22px; }
    .camera-view { width: 100%; aspect-ratio: 4 / 3; display: grid; place-items: center; overflow: hidden; border-radius: 7px; background: #252a25; color: #c7cec5; }
    .camera-view video { width: 100%; height: 100%; object-fit: cover; }
    .camera-placeholder { display: grid; justify-items: center; gap: 10px; font-size: 12px; }
    .camera-placeholder svg { width: 30px; height: 30px; color: #89958a; }
    .dialog-actions { margin-top: 13px; display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
    .dialog-actions button { min-height: 42px; }
    .dialog-actions .wide { grid-column: 1 / -1; }
    .photo-preview { display: none; width: 100%; max-height: 360px; border-radius: 7px; background: #ecece5; object-fit: contain; }
    .filename { min-height: 15px; margin: 8px 0 0; overflow: hidden; color: var(--muted); font-size: 10px; text-overflow: ellipsis; white-space: nowrap; }
    .photo-viewer { width: min(1100px, calc(100% - 24px)); height: min(88vh, 820px); padding: 0; overflow: hidden; border: 1px solid #424840; border-radius: 9px; background: #171b17; color: #f7f6f0; }
    .photo-viewer::backdrop { background: rgba(17, 20, 17, .82); backdrop-filter: blur(3px); }
    .viewer-head { height: 64px; padding: 0 18px 0 22px; display: flex; align-items: center; justify-content: space-between; gap: 14px; border-bottom: 1px solid #343a33; }
    .viewer-title { min-width: 0; overflow: hidden; font-size: 13px; font-weight: 650; text-overflow: ellipsis; white-space: nowrap; }
    .viewer-tools { display: flex; align-items: center; gap: 7px; }
    .viewer-tools .tool-btn { min-height: 34px; border-color: #495047; background: #252b25; color: #f7f6f0; }
    .viewer-zoom-controls { display: flex; flex: 0 0 auto; align-items: center; gap: 4px; }
    #viewerLatest { flex: 0 0 auto; white-space: nowrap; }
    .viewer-tools .tool-btn[aria-pressed="true"] { border-color: #96b19a; background: #324a38; }
    .viewer-tools .tool-btn svg { width: 15px; height: 15px; }
    .viewer-tools .tool-btn.danger { color: #f2a390; }
    .viewer-tools .tool-btn.zoom-value { min-width: 48px; font-variant-numeric: tabular-nums; }
    .viewer-close { width: 34px; height: 34px; display: grid; place-items: center; border: 0; border-radius: 5px; background: transparent; color: #e7e9e3; cursor: pointer; }
    .viewer-close:hover { background: #303630; }
    .viewer-close svg { width: 18px; height: 18px; }
    .viewer-stage { position: relative; width: 100%; height: calc(100% - 64px); display: grid; place-items: center; overflow: hidden; background: #111411; }
    .viewer-image { display: block; max-width: 100%; max-height: 100%; object-fit: contain; transform-origin: center; transition: transform .12s ease-out; }
    .panorama-host { width: 100%; height: 100%; cursor: grab; touch-action: none; }
    .panorama-host:active { cursor: grabbing; }
    .panorama-host canvas { display: block; width: 100%; height: 100%; }
    .viewer-hint { position: absolute; bottom: 14px; left: 50%; transform: translateX(-50%); padding: 7px 10px; border: 1px solid #414840; border-radius: 5px; background: rgba(25,29,25,.82); color: #e1e5de; font-size: 10px; pointer-events: none; }
    .history-list { max-height: min(55vh, 440px); display: grid; gap: 7px; overflow: auto; }
    .history-item { width: 100%; min-height: 64px; padding: 7px; display: grid; grid-template-columns: 58px minmax(0, 1fr) auto; align-items: center; gap: 10px; border: 1px solid var(--line); border-radius: 6px; background: white; text-align: left; cursor: pointer; }
    .history-item:hover { border-color: #b6c4b5; background: #f8faf6; }
    .history-item img { width: 58px; height: 48px; border-radius: 4px; object-fit: cover; }
    .history-item strong { display: block; overflow: hidden; font-size: 11px; text-overflow: ellipsis; white-space: nowrap; }
    .history-item small { display: block; margin-top: 5px; color: var(--muted); font-size: 10px; }
    .history-empty { padding: 24px 12px; color: var(--muted); font-size: 12px; text-align: center; }
    .confirm-copy { margin: 0; color: #62685e; font-size: 12px; line-height: 1.7; }
    .hidden { display: none !important; }
    @media (max-width: 800px) {
      .topbar { height: 62px; padding: 0 16px; }
      .brand-caption, .save-state { display: none; }
      .app-shell { min-height: calc(100vh - 62px); grid-template-columns: 1fr; }
      .main { grid-row: 1; padding: 18px 14px 14px; }
      .main-heading { align-items: flex-start; }
      .level-label { flex-wrap: wrap; }
      .level-label h2 { font-size: 19px; }
      .main-tools { gap: 6px; }
      .tool-btn { width: 38px; padding: 0; font-size: 0; }
      .tool-btn svg { width: 17px; height: 17px; }
      .primary-btn { min-height: 38px; padding: 0 10px; font-size: 11px; }
      .map-surface { min-height: 50vh; height: 58vh; max-height: 700px; }
      .plan-image { max-height: 58vh; }
      .sidebar { padding: 17px 14px 22px; border-top: 1px solid var(--line); border-right: 0; }
      .site-title { margin-bottom: 17px; }
      .site-title h1 { font-size: 20px; }
      .sidebar-footer { position: static; }
      .placement-bar { top: 8px; max-width: calc(100% - 16px); gap: 7px; padding-left: 8px; }
      .placement-bar span { font-size: 10px; }
      .placement-bar button { padding: 0 8px; font-size: 10px; }
      .map-caption { left: 8px; bottom: 8px; }
      .map-toolbar { right: 8px; bottom: 8px; }
      .photo-viewer { width: calc(100% - 16px); height: 84vh; }
      .viewer-head { height: 56px; padding: 0 10px 0 14px; }
      .viewer-stage { height: calc(100% - 56px); }
      .viewer-head { height: auto; min-height: 56px; padding: 8px 10px; align-items: flex-start; flex-direction: column; gap: 6px; }
      .viewer-title { max-width: 100%; }
      .viewer-tools { max-width: 100%; overflow-x: auto; }
      .viewer-tools .tool-btn { width: auto; min-width: 34px; padding: 0 8px; }
      .viewer-stage { height: calc(100% - 98px); }
    }
    @media (max-width: 390px) {
      .main { padding-right: 10px; padding-left: 10px; }
      .level-label { gap: 7px; }
      .level-label h2 { font-size: 17px; }
      .main-tools { gap: 4px; }
      .tool-btn { width: 34px; }
      .primary-btn { padding: 0 8px; }
      .placement-bar img { display: none; }
    }
  </style>
</head>
<body>
  <header class="topbar">
    <div class="brand">
      <div class="brand-mark" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M4 6.5 9 4l6 2.5L20 4v13.5L15 20l-6-2.5L4 20z"/><path d="M9 4v13.5M15 6.5V20"/><circle cx="12" cy="11" r="1.4" fill="currentColor"/></svg></div>
      <span class="brand-name">現場圖記</span><span class="brand-caption">PLANPIN / SITE NOTES</span>
    </div>
    <div class="top-actions"><span class="save-state"><i class="save-dot"></i>已儲存喺此裝置</span><span class="avatar" aria-label="使用者">現</span></div>
  </header>
  <div class="app-shell">
    <aside class="sidebar">
      <p class="eyebrow">工地記錄　/　SITE 01</p>
      <div class="site-title"><div><h1>中環 · 展示空間</h1></div><button class="more-btn" id="renameSite" title="更改項目名稱" aria-label="更改項目名稱"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="5" cy="12" r="1"/><circle cx="12" cy="12" r="1"/><circle cx="19" cy="12" r="1"/></svg></button></div>
      <div class="section-row"><h2 class="section-title">現場相片</h2><span class="count" id="entryCount">0 張</span></div>
      <div class="entry-list" id="entryList"></div>
      <div class="sidebar-footer">位置以平面圖比例記錄<br>相片只會儲存喺此裝置</div>
    </aside>
    <main class="main">
      <div class="main-heading">
        <div class="floor-panel"><div class="level-label floor-title-row"><p class="eyebrow" style="margin:0">樓層</p><h2 id="activeFloorName">地下</h2><button class="more-btn" id="editFloorName" title="編輯樓層名稱" aria-label="編輯樓層名稱"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m14 5 5 5M4 20l4.5-1 11-11a2.1 2.1 0 0 0-3-3l-11 11z"/></svg></button><span class="level-tag" id="floorIndex">1 / 01</span><div class="pdf-controls hidden" id="pdfControls"><button class="tool-btn" id="pagePrev" title="上一頁" aria-label="上一頁">‹</button><span class="pdf-page" id="pageIndicator">1 / 1</span><button class="tool-btn" id="pageNext" title="下一頁" aria-label="下一頁">›</button></div></div><div class="floor-tabs" id="floorTabs" role="tablist" aria-label="樓層分頁"></div></div>
        <div class="main-tools">
          <button class="tool-btn" id="uploadPlan" title="上載平面圖"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7"><path d="M12 16V4m0 0L7.5 8.5M12 4l4.5 4.5"/><path d="M5 14v5h14v-5"/></svg>上載平面圖</button>
          <button class="primary-btn" id="addPhoto"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M4 8h3l1.5-2h7L17 8h3v11H4z"/><circle cx="12" cy="13" r="3.5"/><path d="M18 4v4m-2-2h4"/></svg>新增相片</button>
        </div>
      </div>
      <section class="map-surface" id="mapSurface" aria-label="平面圖位置標記區">
        <div class="plan-empty" id="planEmpty"><svg viewBox="0 0 40 40" fill="none" stroke="currentColor" stroke-width="1.5"><path d="m5 10 10-5 10 5 10-5v25l-10 5-10-5-10 5z"/><path d="M15 5v25m10-20v25"/><circle cx="20" cy="19" r="3"/></svg><strong>上載平面圖開始記錄</strong><span>加入樓層平面圖，然後將現場相片標記到相應位置。</span><button class="tool-btn" id="uploadPlanEmpty">選擇平面圖</button></div>
        <div class="plan-stage hidden" id="planStage"><img class="plan-image" id="planImage" alt="樓層平面圖"><div class="pin-layer" id="pinLayer"></div></div>
        <div class="placement-bar hidden" id="placementBar"><img id="pendingThumb" alt="待標記相片"><span id="placementMessage">喺平面圖點選位置</span><button id="confirmPlacement" disabled>儲存位置</button><button class="cancel" id="cancelPlacement">取消</button></div>
        <div class="map-caption" id="mapCaption"><strong class="map-floor-label" id="mapFloorLabel">地下</strong><span id="mapCaptionDetail">第 1 / 1 頁</span></div>
        <div class="map-toolbar"><button class="zoom-btn" id="zoomOut" title="縮小" aria-label="縮小"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="10.8" cy="10.8" r="6.6"/><path d="M16 16l4.5 4.5M7.8 10.8h6"/></svg></button><button class="zoom-btn" id="zoomReset" title="重設縮放" aria-label="重設縮放"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M4 9V4h5M20 9V4h-5M4 15v5h5m11-5v5h-5"/><path d="M9 9h6v6H9z"/></svg></button><button class="zoom-btn" id="zoomIn" title="放大" aria-label="放大"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="10.8" cy="10.8" r="6.6"/><path d="M16 16l4.5 4.5M10.8 7.8v6m-3-3h6"/></svg></button></div>
      </section>
    </main>
  </div>
  <input class="hidden" type="file" id="planInput" accept="image/*,application/pdf,.pdf">
  <input class="hidden" type="file" id="photoInput" accept="image/*" capture="environment">
  <input class="hidden" type="file" id="updatePhotoInput" accept="image/*">
  <dialog id="photoDialog">
    <div class="dialog-head"><div><h3>新增現場相片</h3><p>拍攝或從裝置選擇相片</p></div><button class="close-btn" id="closeDialog" aria-label="關閉"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m6 6 12 12M18 6 6 18"/></svg></button></div>
    <div class="dialog-body"><div class="camera-view" id="cameraView"><div class="camera-placeholder" id="cameraPlaceholder"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M3 8h4l1.5-2h7L17 8h4v12H3z"/><circle cx="12" cy="14" r="3.5"/></svg><span>相機未啟動</span></div><video id="cameraVideo" autoplay playsinline class="hidden"></video></div><img class="photo-preview" id="photoPreview" alt="相片預覽"><p class="filename" id="photoFilename"></p><div class="dialog-actions"><button class="tool-btn" id="startCamera"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7"><path d="M3 8h4l1.5-2h7L17 8h4v12H3z"/><circle cx="12" cy="14" r="3.5"/></svg>開啟相機</button><button class="tool-btn" id="choosePhoto"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7"><rect x="3" y="4" width="18" height="16" rx="2"/><circle cx="8.5" cy="9" r="1.5"/><path d="m4 17 5-5 3 3 3-4 5 6"/></svg>選擇相片</button><button class="primary-btn wide hidden" id="usePhoto">標記相片位置</button><button class="primary-btn wide hidden" id="takePhoto">拍攝相片</button></div></div>
  </dialog>
  <dialog id="floorNameDialog">
    <div class="dialog-head"><div><h3 id="nameDialogTitle">編輯樓層名稱</h3><p id="nameDialogHint">輸入容易辨認嘅樓層名稱</p></div><button class="close-btn" id="closeFloorName" aria-label="關閉"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m6 6 12 12M18 6 6 18"/></svg></button></div>
    <div class="dialog-body"><input class="name-input" id="floorNameInput" maxlength="40" aria-label="樓層名稱"><div class="dialog-actions"><button class="tool-btn" id="cancelFloorName">取消</button><button class="primary-btn" id="saveFloorName">儲存名稱</button></div></div>
  </dialog>
  <dialog class="photo-viewer" id="photoViewer" aria-label="相片檢視器">
    <div class="viewer-head">
      <strong class="viewer-title" id="viewerTitle"></strong>
      <div class="viewer-tools">
        <button class="tool-btn" id="viewerLatest" title="回到最新照片" aria-label="回到最新照片"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M4 12h15m-6-6 6 6-6 6"/></svg><span>最新照片</span></button>
        <button class="tool-btn" id="viewerRename" title="編輯相片名稱" aria-label="編輯相片名稱"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m14 5 5 5M4 20l4.5-1 11-11a2.1 2.1 0 0 0-3-3l-11 11z"/></svg></button>
        <button class="tool-btn" id="viewerMove" title="更改相片位置" aria-label="更改相片位置"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M20 10c0 5-8 11-8 11S4 15 4 10a8 8 0 1 1 16 0Z"/><circle cx="12" cy="10" r="2.5"/></svg></button>
        <button class="tool-btn" id="viewerUpdate" title="更新相片" aria-label="更新相片"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M12 15V4m0 0L7.5 8.5M12 4l4.5 4.5"/><path d="M5 14v5h14v-5"/></svg></button>
        <button class="tool-btn" id="viewerHistory" title="查看舊相片" aria-label="查看相片歷史"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M3 12a9 9 0 1 0 3-6.7L3 8"/><path d="M3 3v5h5m4-1v5l3 2"/></svg><span id="historyCount">0</span></button>
        <button class="tool-btn danger" id="viewerDelete" title="刪除相片" aria-label="刪除相片"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M4 7h16m-10 4v7m4-7v7M6 7l1 14h10l1-14M9 7V4h6v3"/></svg></button>
        <div class="viewer-zoom-controls" id="viewerZoomControls">
          <button class="tool-btn" id="photoZoomOut" title="縮小相片" aria-label="縮小相片"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="10.8" cy="10.8" r="6.6"/><path d="M16 16l4.5 4.5M7.8 10.8h6"/></svg></button>
          <button class="tool-btn zoom-value" id="photoZoomReset" title="重設相片縮放" aria-label="重設相片縮放">100%</button>
          <button class="tool-btn" id="photoZoomIn" title="放大相片" aria-label="放大相片"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="10.8" cy="10.8" r="6.6"/><path d="M16 16l4.5 4.5M10.8 7.8v6m-3-3h6"/></svg></button>
        </div>
        <button class="tool-btn" id="viewerMode" aria-label="切換 360 度檢視" aria-pressed="false">360°</button>
        <button class="viewer-close" id="viewerClose" aria-label="關閉相片"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m6 6 12 12M18 6 6 18"/></svg></button>
      </div>
    </div>
    <div class="viewer-stage"><img class="viewer-image" id="viewerImage" alt="現場相片"><div class="panorama-host hidden" id="panoramaHost"></div><span class="viewer-hint hidden" id="viewerHint">拖動畫面環視　·　滾輪縮放</span></div>
  </dialog>
  <dialog id="historyDialog"><div class="dialog-head"><div><h3>相片歷史紀錄</h3><p id="historySubtitle">可開啟舊版本查閱</p></div><button class="close-btn" id="closeHistory" aria-label="關閉"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m6 6 12 12M18 6 6 18"/></svg></button></div><div class="dialog-body"><div class="history-list" id="historyList"></div></div></dialog>
  <dialog id="deleteDialog"><div class="dialog-head"><div><h3>刪除相片？</h3><p>相片同佢嘅歷史版本會一併刪除。</p></div><button class="close-btn" id="closeDelete" aria-label="關閉"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="m6 6 12 12M18 6 6 18"/></svg></button></div><div class="dialog-body"><p class="confirm-copy" id="deleteMessage"></p><div class="dialog-actions"><button class="tool-btn" id="cancelDelete">取消</button><button class="primary-btn wide" id="confirmDelete" style="border-color:#a84436;background:#a84436">刪除相片</button></div></div></dialog>
  <div class="toast" id="toast" role="status"></div>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
  <script>
    (() => {
      const $ = (selector) => document.querySelector(selector);
      const planSvg = `<svg xmlns="http://www.w3.org/2000/svg" width="1100" height="720" viewBox="0 0 1100 720"><rect width="1100" height="720" fill="#f8f7f0"/><g fill="#e9eee8"><path d="M105 95h340v205H105zM465 95h270v205H465zM755 95h250v205H755zM105 320h195v285H105zM320 320h415v285H320zM755 320h250v285H755z"/></g><g fill="none" stroke="#687568" stroke-width="9" stroke-linecap="square"><path d="M105 95h900v510H105zM455 95v205M745 95v205M310 310v295M745 310v295M105 310h900M455 310v115M455 495v110M745 310v120M745 500v105M310 455h145M560 310v115M600 425h145M745 500h115"/></g><g fill="none" stroke="#aab1a7" stroke-width="3"><path d="M129 120h292v155H129zM488 120h225v155H488zM779 120h202v155H779zM129 345h156v235H129zM344 345h382v235H344zM779 345h202v235H779z"/><path d="M175 298v25m26-25v25m26-25v25m26-25v25m96-25v25m26-25v25m26-25v25m26-25v25m96-25v25m26-25v25m26-25v25m26-25v25m96-25v25m26-25v25m26-25v25m26-25v25"/></g><g fill="#777f74" font-family="sans-serif" font-size="16" letter-spacing="2"><text x="190" y="200">入口大堂</text><text x="530" y="200">展示廳</text><text x="835" y="200">會議室</text><text x="152" y="478">接待處</text><text x="485" y="470">中庭</text><text x="835" y="478">工作室</text></g><g fill="none" stroke="#c6c9be" stroke-width="2"><path d="M105 55h900M105 47v16m900-16v16M55 95v510M47 95h16m-16 510h16"/></g><g fill="#92988d" font-family="sans-serif" font-size="12"><text x="530" y="45">18.0 m</text><text x="22" y="356" transform="rotate(-90 22 356)">10.2 m</text></g></svg>`;
      const demoPlan = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(planSvg);
      const dbPromise = new Promise((resolve, reject) => {
        const request = indexedDB.open('planpin-local', 2);
        request.onupgradeneeded = (event) => {
          const db = request.result;
          if (event.oldVersion < 1) {
            db.createObjectStore('settings', { keyPath: 'key' });
            db.createObjectStore('entries', { keyPath: 'id' });
          }
          if (event.oldVersion < 2) db.createObjectStore('floors', { keyPath: 'id' });
        };
        request.onsuccess = () => resolve(request.result);
        request.onerror = () => reject(request.error);
      });
      const tx = async (store, mode, action) => {
        const db = await dbPromise;
        return new Promise((resolve, reject) => {
          const request = action(db.transaction(store, mode).objectStore(store));
          request.onsuccess = () => resolve(request.result);
          request.onerror = () => reject(request.error);
        });
      };
      const state = { plan: demoPlan, planName: '地下', planType: 'image', pdfBlob: null, pdfDocument: null, page: 1, pageCount: 1, floors: [], activeFloorId: null, entries: [], pendingBlob: null, pendingName: '', point: null, repositionId: null, stream: null, zoom: 1, activeId: null, viewerEntry: null, viewerVersion: null, viewerUrl: null, viewer360: false, photoZoom: 1, panorama: null, panoramaFrame: 0, nameTargetType: null, nameTargetId: null, pendingDeleteId: null, historyUrls: [] };
      const mapSurface = $('#mapSurface');
      const planImage = $('#planImage');
      const planStage = $('#planStage');
      const photoDialog = $('#photoDialog');
      const toast = (text) => { const node = $('#toast'); node.textContent = text; node.classList.add('show'); setTimeout(() => node.classList.remove('show'), 2300); };
      const save = async (store, value) => tx(store, 'readwrite', (objectStore) => objectStore.put(value));
      const readAll = async (store) => tx(store, 'readonly', (objectStore) => objectStore.getAll());
      const formatDate = (date) => new Intl.DateTimeFormat('zh-HK', { month: 'numeric', day: 'numeric', hour: '2-digit', minute: '2-digit', hour12: false }).format(date);
      const planData = async (file) => new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = () => reject(reader.error);
        reader.readAsDataURL(file);
      });
      const activeFloor = () => state.floors.find((floor) => floor.id === state.activeFloorId);
      const renderFloorTabs = () => {
        const tabs = $('#floorTabs');
        tabs.replaceChildren();
        state.floors.forEach((floor, index) => {
          const tab = document.createElement('button');
          tab.type = 'button';
          tab.className = 'floor-tab';
          tab.setAttribute('role', 'tab');
          tab.setAttribute('aria-selected', String(floor.id === state.activeFloorId));
          tab.textContent = floor.name;
          tab.addEventListener('click', () => activateFloor(floor.id));
          tabs.append(tab);
          if (floor.id === state.activeFloorId) {
            $('#activeFloorName').textContent = floor.name;
            $('#floorIndex').textContent = `${index + 1} / ${String(state.floors.length).padStart(2, '0')}`;
            $('#mapFloorLabel').textContent = floor.name;
          }
        });
        const add = document.createElement('button');
        add.type = 'button';
        add.className = 'floor-add';
        add.title = '新增樓層';
        add.setAttribute('aria-label', '新增樓層');
        add.innerHTML = '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M12 5v14M5 12h14"/></svg>';
        add.addEventListener('click', addFloor);
        tabs.append(add);
      };
      const setPlan = async (src, name, persist = true) => {
        state.plan = src;
        state.planName = activeFloor()?.name || name;
        state.planType = 'image';
        state.pdfBlob = null;
        state.pdfDocument = null;
        state.page = 1;
        state.pageCount = 1;
        if (activeFloor()) {
          Object.assign(activeFloor(), { type: 'image', src, planFileName: name, page: 1 });
          if (persist) await save('floors', activeFloor());
        }
        planImage.src = src;
        $('#planEmpty').classList.add('hidden');
        planStage.classList.remove('hidden');
        $('#pdfControls').classList.add('hidden');
        $('#mapCaptionDetail').textContent = `第 ${state.page} / ${state.pageCount} 頁`;
        renderPins();
      };
      const renderPdfPage = async (pageNumber, persist = true) => {
        const page = await state.pdfDocument.getPage(pageNumber);
        state.page = pageNumber;
        const baseViewport = page.getViewport({ scale: 1 });
        const viewport = page.getViewport({ scale: Math.min(1.6, 1600 / baseViewport.width) });
        const canvas = document.createElement('canvas');
        canvas.width = Math.ceil(viewport.width);
        canvas.height = Math.ceil(viewport.height);
        await page.render({ canvasContext: canvas.getContext('2d'), viewport }).promise;
        planImage.src = canvas.toDataURL('image/png');
        await planImage.decode();
        $('#planEmpty').classList.add('hidden');
        planStage.classList.remove('hidden');
        $('#pdfControls').classList.remove('hidden');
        $('#pageIndicator').textContent = `${pageNumber} / ${state.pageCount}`;
        $('#pagePrev').disabled = pageNumber <= 1;
        $('#pageNext').disabled = pageNumber >= state.pageCount;
        $('#mapCaptionDetail').textContent = `第 ${pageNumber} / ${state.pageCount} 頁`;
        renderPins();
        if (activeFloor()) {
          activeFloor().page = pageNumber;
          if (persist) await save('floors', activeFloor());
        }
      };
      const setPdfPlan = async (file) => {
        if (!window.pdfjsLib) throw new Error('PDF renderer unavailable');
        window.pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
        state.pdfBlob = file;
        state.planName = activeFloor()?.name || file.name;
        state.planType = 'pdf';
        state.pdfDocument = await window.pdfjsLib.getDocument({ data: new Uint8Array(await file.arrayBuffer()) }).promise;
        state.pageCount = state.pdfDocument.numPages;
        if (activeFloor()) Object.assign(activeFloor(), { type: 'pdf', blob: file, planFileName: file.name, page: 1 });
        await renderPdfPage(1, false);
        if (activeFloor()) await save('floors', activeFloor());
      };
      const activateFloor = async (floorId) => {
        const floor = state.floors.find((item) => item.id === floorId);
        if (!floor) return;
        state.activeFloorId = floorId;
        state.activeId = null;
        state.planName = floor.name;
        state.zoom = 1;
        planImage.style.transform = '';
        renderFloorTabs();
        if (floor.type === 'pdf' && floor.blob && window.pdfjsLib) {
          window.pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
          state.pdfBlob = floor.blob;
          state.planType = 'pdf';
          state.pdfDocument = await window.pdfjsLib.getDocument({ data: new Uint8Array(await floor.blob.arrayBuffer()) }).promise;
          state.pageCount = state.pdfDocument.numPages;
          await renderPdfPage(Math.min(floor.page || 1, state.pageCount), false);
        } else if (floor.type === 'image') {
          await setPlan(floor.src || demoPlan, floor.planFileName || floor.name, false);
        } else {
          state.planType = 'empty';
          state.pdfBlob = null;
          state.pdfDocument = null;
          state.page = 1;
          state.pageCount = 1;
          planStage.classList.add('hidden');
          $('#planEmpty').classList.remove('hidden');
          $('#pdfControls').classList.add('hidden');
          $('#mapCaptionDetail').textContent = '第 1 / 1 頁';
          renderPins();
        }
        renderList();
        renderPins();
      };
      const addFloor = async () => {
        const floor = { id: crypto.randomUUID(), order: state.floors.length, name: `樓層 ${state.floors.length + 1}`, floorCode: `${state.floors.length}F`, type: 'empty', page: 1 };
        state.floors.push(floor);
        await save('floors', floor);
        await activateFloor(floor.id);
      };
      const entryPage = (entry) => Math.min(Math.max(entry.pageNumber || 1, 1), state.pageCount);
      const renderPins = () => {
        const layer = $('#pinLayer');
        layer.replaceChildren();
        state.entries.filter((entry) => entry.floorId === state.activeFloorId && entryPage(entry) === state.page).forEach((entry, index) => {
          const pin = document.createElement('button');
          pin.className = `pin${entry.id === state.activeId ? ' selected' : ''}`;
          pin.style.left = `${entry.x * 100}%`;
          pin.style.top = `${entry.y * 100}%`;
          pin.title = entry.name;
          pin.setAttribute('aria-label', `相片 ${index + 1}: ${entry.name}`);
          pin.innerHTML = `<svg viewBox="0 0 32 38" aria-hidden="true"><path d="M16 1C7.9 1 1.5 7.3 1.5 15.1c0 9.6 14.5 22 14.5 22s14.5-12.4 14.5-22C30.5 7.3 24.1 1 16 1Z" fill="${entry.id === state.activeId ? '#2c5848' : '#e16e4d'}" stroke="white" stroke-width="1.5"/><circle cx="16" cy="15" r="9" fill="white"/><text class="pin-number" x="16" y="18">${index + 1}</text></svg>`;
          pin.addEventListener('click', (event) => { event.stopPropagation(); state.activeId = entry.id; renderList(); renderPins(); openPhoto(entry); });
          layer.append(pin);
        });
      };
      const renderList = () => {
        const list = $('#entryList');
        list.replaceChildren();
        const visibleEntries = state.entries.filter((entry) => entry.floorId === state.activeFloorId);
        $('#entryCount').textContent = `${visibleEntries.length} 張`;
        if (!visibleEntries.length) {
          const empty = document.createElement('div');
          empty.className = 'empty-state';
          empty.textContent = '未有現場相片';
          list.append(empty);
          return;
        }
        visibleEntries.forEach((entry, index) => {
          const button = document.createElement('button');
          button.className = `entry${entry.id === state.activeId ? ' active' : ''}`;
          button.innerHTML = `<img class="entry-thumb" alt="" src="${URL.createObjectURL(entry.blob)}"><span><span class="entry-name"></span><span class="entry-time">${formatDate(new Date(entry.createdAt))}</span></span><span class="entry-index">${String(index + 1).padStart(2, '0')}</span>`;
          button.querySelector('.entry-name').textContent = entry.name;
          button.querySelector('.entry-thumb').addEventListener('click', (event) => { event.stopPropagation(); openPhoto(entry); });
          button.addEventListener('click', async () => { state.activeId = entry.id; if (state.planType === 'pdf' && entryPage(entry) !== state.page) await renderPdfPage(entryPage(entry)); renderList(); renderPins(); });
          list.append(button);
        });
      };
      const disposePanorama = () => {
        if (!state.panorama) return;
        cancelAnimationFrame(state.panoramaFrame);
        window.removeEventListener('resize', state.panorama.resize);
        state.panorama.controls.dispose();
        state.panorama.geometry.dispose();
        state.panorama.material.map?.dispose();
        state.panorama.material.dispose();
        state.panorama.renderer.dispose();
        state.panorama.renderer.domElement.remove();
        state.panorama = null;
      };
      const renderPanorama = () => {
        if (!window.THREE?.OrbitControls) throw new Error('360 viewer unavailable');
        disposePanorama();
        const host = $('#panoramaHost');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, host.clientWidth / host.clientHeight, .1, 1100);
        camera.position.set(0, 0, .1);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
        renderer.setSize(host.clientWidth, host.clientHeight);
        host.replaceChildren(renderer.domElement);
        const texture = new THREE.TextureLoader().load(state.viewerUrl);
        const geometry = new THREE.SphereGeometry(500, 64, 48);
        geometry.scale(-1, 1, 1);
        const material = new THREE.MeshBasicMaterial({ map: texture });
        scene.add(new THREE.Mesh(geometry, material));
        const controls = new THREE.OrbitControls(camera, renderer.domElement);
        controls.enablePan = false;
        controls.enableZoom = true;
        controls.minDistance = .1;
        controls.maxDistance = 2;
        controls.rotateSpeed = -.25;
        controls.enableDamping = true;
        const resize = () => {
          if (!state.panorama) return;
          camera.aspect = host.clientWidth / host.clientHeight;
          camera.updateProjectionMatrix();
          renderer.setSize(host.clientWidth, host.clientHeight);
        };
        state.panorama = { camera, controls, geometry, material, renderer, resize };
        window.addEventListener('resize', resize);
        const animate = () => {
          if (!state.panorama) return;
          state.panoramaFrame = requestAnimationFrame(animate);
          controls.update();
          renderer.render(scene, camera);
        };
        animate();
      };
      const setPhotoViewerMode = async (is360, persist = false) => {
        state.viewer360 = is360;
        $('#viewerMode').setAttribute('aria-pressed', String(is360));
        $('#viewerImage').classList.toggle('hidden', is360);
        $('#panoramaHost').classList.toggle('hidden', !is360);
        $('#viewerHint').classList.toggle('hidden', !is360);
        $('#viewerZoomControls').classList.toggle('hidden', is360);
        if (is360) {
          try { renderPanorama(); }
          catch { state.viewer360 = false; $('#viewerMode').setAttribute('aria-pressed', 'false'); $('#viewerImage').classList.remove('hidden'); $('#panoramaHost').classList.add('hidden'); $('#viewerHint').classList.add('hidden'); toast('無法啟動 360 檢視'); return; }
        } else disposePanorama();
        if (persist && state.viewerEntry && !state.viewerVersion) {
          state.viewerEntry.is360 = is360;
          await save('entries', state.viewerEntry);
        }
      };
      const setPhotoZoom = (zoom) => {
        state.photoZoom = Math.max(1, Math.min(4, zoom));
        $('#viewerImage').style.transform = `scale(${state.photoZoom})`;
        $('#photoZoomReset').textContent = `${Math.round(state.photoZoom * 100)}%`;
      };
      const openPhoto = async (entry, version = null) => {
        disposePanorama();
        if (state.viewerUrl) URL.revokeObjectURL(state.viewerUrl);
        state.viewerEntry = entry;
        state.viewerVersion = version;
        setPhotoZoom(1);
        state.viewerUrl = URL.createObjectURL(version?.blob || entry.blob);
        $('#viewerTitle').textContent = version ? `${entry.name}　·　舊相片 ${formatDate(new Date(version.savedAt))}` : entry.name;
        $('#viewerLatest').classList.toggle('hidden', !version);
        $('#historyCount').textContent = String(entry.history?.length || 0);
        $('#viewerImage').src = state.viewerUrl;
        $('#photoViewer').showModal();
        await setPhotoViewerMode(Boolean(version?.is360 ?? entry.is360));
      };
      const closePhoto = () => {
        disposePanorama();
        if (state.viewerUrl) URL.revokeObjectURL(state.viewerUrl);
        state.viewerUrl = null;
        state.viewerEntry = null;
        state.viewerVersion = null;
        $('#viewerImage').removeAttribute('src');
      };
      const openPhotoNameEditor = (entry) => {
        state.nameTargetType = 'photo';
        state.nameTargetId = entry.id;
        $('#nameDialogTitle').textContent = '編輯相片名稱';
        $('#nameDialogHint').textContent = '輸入容易辨認嘅相片名稱';
        $('#floorNameInput').value = entry.name;
        $('#floorNameDialog').showModal();
        $('#floorNameInput').focus();
        $('#floorNameInput').select();
      };
      const renderHistory = (entry) => {
        const list = $('#historyList');
        list.replaceChildren();
        state.historyUrls.forEach((url) => URL.revokeObjectURL(url));
        state.historyUrls = [];
        $('#historySubtitle').textContent = entry.name;
        if (!entry.history?.length) {
          const empty = document.createElement('div');
          empty.className = 'history-empty';
          empty.textContent = '更新照片後，舊版本會喺呢度保留。';
          list.append(empty);
          return;
        }
        entry.history.forEach((version, index) => {
          const button = document.createElement('button');
          button.type = 'button';
          button.className = 'history-item';
          const image = document.createElement('img');
          image.alt = '';
          image.src = URL.createObjectURL(version.blob);
          state.historyUrls.push(image.src);
          const details = document.createElement('span');
          details.innerHTML = `<strong></strong><small>${formatDate(new Date(version.savedAt))}</small>`;
          details.querySelector('strong').textContent = index === 0 ? '更新前版本' : `舊版本 ${index + 1}`;
          const view = document.createElement('span');
          view.className = 'entry-index';
          view.textContent = '查閱';
          button.append(image, details, view);
          button.addEventListener('click', () => { $('#historyDialog').close(); openPhoto(entry, version); });
          list.append(button);
        });
        $('#historyDialog').showModal();
      };
      const stopCamera = () => {
        if (state.stream) state.stream.getTracks().forEach((track) => track.stop());
        state.stream = null;
        $('#cameraVideo').srcObject = null;
      };
      const setPendingPhoto = (blob, name) => {
        state.pendingBlob = blob;
        state.pendingName = name || '現場相片';
        $('#photoPreview').src = URL.createObjectURL(blob);
        $('#photoPreview').style.display = 'block';
        $('#cameraView').classList.add('hidden');
        $('#photoFilename').textContent = state.pendingName;
        $('#usePhoto').classList.remove('hidden');
        $('#takePhoto').classList.add('hidden');
        $('#startCamera').classList.remove('hidden');
      };
      const beginPlacement = () => {
        if (!state.pendingBlob) return;
        state.repositionId = null;
        stopCamera();
        photoDialog.close();
        $('#placementBar').classList.remove('hidden');
        $('#pendingThumb').src = URL.createObjectURL(state.pendingBlob);
        $('#confirmPlacement').disabled = true;
        state.point = null;
        mapSurface.classList.add('placing');
      };
      const beginReposition = (entry) => {
        state.repositionId = entry.id;
        state.pendingBlob = null;
        state.pendingName = entry.name;
        state.point = null;
        $('#pendingThumb').src = URL.createObjectURL(entry.blob);
        $('#placementMessage').textContent = `選擇「${entry.name}」嘅新位置`;
        $('#confirmPlacement').disabled = true;
        $('#placementBar').classList.remove('hidden');
        mapSurface.classList.add('placing');
        $('#photoViewer').close();
      };
      $('#uploadPlan').addEventListener('click', () => $('#planInput').click());
      $('#uploadPlanEmpty').addEventListener('click', () => $('#planInput').click());
      $('#planInput').addEventListener('change', async (event) => {
        const file = event.target.files[0];
        if (!file) return;
        try {
          if (file.type === 'application/pdf' || /\.pdf$/i.test(file.name)) await setPdfPlan(file);
          else if (file.type.startsWith('image/')) await setPlan(await planData(file), file.name);
          else return toast('請選擇圖片或 PDF 格式嘅平面圖');
          toast('平面圖已更新');
        } catch { toast('無法讀取檔案，請確認 PDF 格式正確'); }
        event.target.value = '';
      });
      $('#addPhoto').addEventListener('click', () => {
        state.pendingBlob = null;
        $('#photoPreview').style.display = 'none';
        $('#cameraView').classList.remove('hidden');
        $('#cameraPlaceholder').classList.remove('hidden');
        $('#cameraVideo').classList.add('hidden');
        $('#photoFilename').textContent = '';
        $('#usePhoto').classList.add('hidden');
        $('#takePhoto').classList.add('hidden');
        photoDialog.showModal();
      });
      $('#closeDialog').addEventListener('click', () => { stopCamera(); photoDialog.close(); });
      photoDialog.addEventListener('click', (event) => { if (event.target === photoDialog) { stopCamera(); photoDialog.close(); } });
      $('#viewerClose').addEventListener('click', () => $('#photoViewer').close());
      $('#photoViewer').addEventListener('close', closePhoto);
      $('#photoViewer').addEventListener('click', (event) => { if (event.target === $('#photoViewer')) $('#photoViewer').close(); });
      $('#viewerMode').addEventListener('click', () => setPhotoViewerMode(!state.viewer360, true));
      $('#viewerLatest').addEventListener('click', () => { if (state.viewerEntry) openPhoto(state.viewerEntry); });
      $('#photoZoomIn').addEventListener('click', () => setPhotoZoom(state.photoZoom + .25));
      $('#photoZoomOut').addEventListener('click', () => setPhotoZoom(state.photoZoom - .25));
      $('#photoZoomReset').addEventListener('click', () => setPhotoZoom(1));
      $('#viewerImage').addEventListener('wheel', (event) => {
        event.preventDefault();
        setPhotoZoom(state.photoZoom + (event.deltaY < 0 ? .2 : -.2));
      }, { passive: false });
      $('#viewerRename').addEventListener('click', () => { if (state.viewerEntry) openPhotoNameEditor(state.viewerEntry); });
      $('#viewerMove').addEventListener('click', () => { if (state.viewerEntry) beginReposition(state.viewerEntry); });
      $('#viewerUpdate').addEventListener('click', () => { if (state.viewerEntry) $('#updatePhotoInput').click(); });
      $('#viewerHistory').addEventListener('click', () => { if (state.viewerEntry) renderHistory(state.viewerEntry); });
      const closeHistory = () => {
        $('#historyDialog').close();
        state.historyUrls.forEach((url) => URL.revokeObjectURL(url));
        state.historyUrls = [];
      };
      $('#closeHistory').addEventListener('click', closeHistory);
      $('#historyDialog').addEventListener('click', (event) => { if (event.target === $('#historyDialog')) closeHistory(); });
      const closeDelete = () => { $('#deleteDialog').close(); state.pendingDeleteId = null; };
      $('#closeDelete').addEventListener('click', closeDelete);
      $('#cancelDelete').addEventListener('click', closeDelete);
      $('#viewerDelete').addEventListener('click', () => {
        if (!state.viewerEntry) return;
        state.pendingDeleteId = state.viewerEntry.id;
        $('#deleteMessage').textContent = `確定刪除「${state.viewerEntry.name}」？此操作無法復原。`;
        $('#deleteDialog').showModal();
      });
      $('#confirmDelete').addEventListener('click', async () => {
        const id = state.pendingDeleteId;
        if (!id) return;
        try {
          await tx('entries', 'readwrite', (store) => store.delete(id));
          state.entries = state.entries.filter((entry) => entry.id !== id);
          closeDelete();
          $('#photoViewer').close();
          renderList();
          renderPins();
          toast('相片同歷史紀錄已刪除');
        } catch { toast('刪除失敗，請重試'); }
      });
      $('#startCamera').addEventListener('click', async () => {
        if (!navigator.mediaDevices?.getUserMedia) { $('#photoInput').click(); return; }
        try {
          stopCamera();
          state.stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: { ideal: 'environment' } }, audio: false });
          const video = $('#cameraVideo');
          video.srcObject = state.stream;
          video.classList.remove('hidden');
          $('#cameraPlaceholder').classList.add('hidden');
          $('#cameraView').classList.remove('hidden');
          $('#photoPreview').style.display = 'none';
          $('#takePhoto').classList.remove('hidden');
          $('#usePhoto').classList.add('hidden');
        } catch { toast('無法開啟相機，請改為選擇相片'); }
      });
      $('#choosePhoto').addEventListener('click', () => $('#photoInput').click());
      $('#photoInput').addEventListener('change', (event) => {
        const file = event.target.files[0];
        if (file) setPendingPhoto(file, file.name);
        event.target.value = '';
      });
      $('#updatePhotoInput').addEventListener('change', async (event) => {
        const file = event.target.files[0];
        const entry = state.viewerEntry;
        if (file && entry) {
          entry.history = [{ blob: entry.blob, savedAt: entry.updatedAt || entry.createdAt, is360: entry.is360 }, ...(entry.history || [])];
          entry.blob = file;
          entry.is360 = false;
          entry.updatedAt = Date.now();
          try {
            await save('entries', entry);
            renderList();
            renderPins();
            await openPhoto(entry);
            toast('新相片已更新，舊版本已保留');
          } catch { toast('更新失敗，舊相片仍然保留'); }
        }
        event.target.value = '';
      });
      $('#takePhoto').addEventListener('click', () => {
        const video = $('#cameraVideo');
        if (!video.videoWidth) return toast('相機準備中，請稍候');
        const canvas = document.createElement('canvas');
        canvas.width = video.videoWidth;
        canvas.height = video.videoHeight;
        canvas.getContext('2d').drawImage(video, 0, 0);
        canvas.toBlob((blob) => { if (blob) setPendingPhoto(blob, `現場相片 ${formatDate(new Date())}.jpg`); }, 'image/jpeg', .9);
      });
      $('#usePhoto').addEventListener('click', beginPlacement);
      mapSurface.addEventListener('click', (event) => {
        if (!mapSurface.classList.contains('placing') || !event.target.closest('#planImage')) return;
        const rect = planImage.getBoundingClientRect();
        const x = Math.max(0, Math.min(1, (event.clientX - rect.left) / rect.width));
        const y = Math.max(0, Math.min(1, (event.clientY - rect.top) / rect.height));
        state.point = { x, y };
        $('#confirmPlacement').disabled = false;
        $('#pendingThumb').style.outline = '2px solid #73a77d';
        const previewPin = document.createElement('div');
        previewPin.className = 'pin';
        previewPin.style.left = `${x * 100}%`;
        previewPin.style.top = `${y * 100}%`;
        previewPin.innerHTML = '<svg viewBox="0 0 32 38" aria-hidden="true"><path d="M16 1C7.9 1 1.5 7.3 1.5 15.1c0 9.6 14.5 22 14.5 22s14.5-12.4 14.5-22C30.5 7.3 24.1 1 16 1Z" fill="#e16e4d" stroke="white" stroke-width="1.5"/></svg>';
        $('#pinLayer').replaceChildren(previewPin);
      });
      $('#confirmPlacement').addEventListener('click', async () => {
        if (!state.point) return;
        try {
          if (state.repositionId) {
            const entry = state.entries.find((item) => item.id === state.repositionId);
            if (!entry) return;
            Object.assign(entry, { floorId: state.activeFloorId, x: state.point.x, y: state.point.y, pageNumber: state.page });
            await save('entries', entry);
            state.activeId = entry.id;
            toast('相片位置已更新');
          } else {
            if (!state.pendingBlob) return;
            const entry = { id: crypto.randomUUID(), floorId: state.activeFloorId, x: state.point.x, y: state.point.y, pageNumber: state.page, name: state.pendingName, blob: state.pendingBlob, is360: false, createdAt: Date.now() };
            await save('entries', entry);
            state.entries.unshift(entry);
            state.activeId = entry.id;
            toast('相片位置已儲存');
          }
          state.pendingBlob = null;
          state.point = null;
          state.repositionId = null;
          $('#placementBar').classList.add('hidden');
          mapSurface.classList.remove('placing');
          renderList();
          renderPins();
        } catch { toast('儲存失敗，請檢查裝置空間'); }
      });
      $('#cancelPlacement').addEventListener('click', () => {
        state.pendingBlob = null;
        state.point = null;
        state.repositionId = null;
        $('#placementBar').classList.add('hidden');
        mapSurface.classList.remove('placing');
        renderPins();
      });
      $('#renameSite').addEventListener('click', () => {
        const title = prompt('項目名稱', $('.site-title h1').textContent);
        if (title?.trim()) $('.site-title h1').textContent = title.trim();
      });
      $('#zoomIn').addEventListener('click', () => { state.zoom = Math.min(1.7, state.zoom + .1); planImage.style.transform = `scale(${state.zoom})`; });
      $('#zoomOut').addEventListener('click', () => { state.zoom = Math.max(.7, state.zoom - .1); planImage.style.transform = `scale(${state.zoom})`; });
      $('#zoomReset').addEventListener('click', () => { state.zoom = 1; planImage.style.transform = ''; });
      $('#editFloorName').addEventListener('click', () => {
        const floor = activeFloor();
        if (!floor) return;
        state.nameTargetType = 'floor';
        state.nameTargetId = floor.id;
        $('#nameDialogTitle').textContent = '編輯樓層名稱';
        $('#nameDialogHint').textContent = '輸入容易辨認嘅樓層名稱';
        $('#floorNameInput').value = floor.name;
        $('#floorNameDialog').showModal();
        $('#floorNameInput').focus();
        $('#floorNameInput').select();
      });
      const closeFloorName = () => {
        $('#floorNameDialog').close();
        state.nameTargetType = null;
        state.nameTargetId = null;
      };
      $('#closeFloorName').addEventListener('click', closeFloorName);
      $('#cancelFloorName').addEventListener('click', closeFloorName);
      $('#saveFloorName').addEventListener('click', async () => {
        const name = $('#floorNameInput').value.trim();
        if (!name) return toast('請輸入樓層名稱');
        if (state.nameTargetType === 'floor') {
          const floor = state.floors.find((item) => item.id === state.nameTargetId);
          if (!floor) return closeFloorName();
          floor.name = name;
          if (floor.id === state.activeFloorId) {
            state.planName = name;
            $('#mapCaptionDetail').textContent = `第 ${state.page} / ${state.pageCount} 頁`;
          }
          await save('floors', floor);
          renderFloorTabs();
        } else if (state.nameTargetType === 'photo') {
          const entry = state.entries.find((item) => item.id === state.nameTargetId);
          if (!entry) return closeFloorName();
          entry.name = name;
          await save('entries', entry);
          if (state.viewerEntry?.id === entry.id) $('#viewerTitle').textContent = name;
          renderList();
          renderPins();
        }
        closeFloorName();
      });
      $('#floorNameInput').addEventListener('keydown', (event) => { if (event.key === 'Enter') $('#saveFloorName').click(); });
        $('#pagePrev').addEventListener('click', () => { if (state.page > 1) renderPdfPage(state.page - 1); });
        $('#pageNext').addEventListener('click', () => { if (state.page < state.pageCount) renderPdfPage(state.page + 1); });
      const init = async () => {
        try {
          const [legacyPlan, floors, entries] = await Promise.all([tx('settings', 'readonly', (store) => store.get('plan')), readAll('floors'), readAll('entries')]);
          state.floors = floors.sort((left, right) => {
            const leftOrder = Number.isInteger(left.order) ? left.order : left.name === '地下' ? 0 : Number.MAX_SAFE_INTEGER;
            const rightOrder = Number.isInteger(right.order) ? right.order : right.name === '地下' ? 0 : Number.MAX_SAFE_INTEGER;
            return leftOrder - rightOrder;
          });
          if (!state.floors.length) {
            const floor = legacyPlan
              ? { id: crypto.randomUUID(), order: 0, name: '地下', type: legacyPlan.type || 'image', src: legacyPlan.src, blob: legacyPlan.blob, planFileName: legacyPlan.name, page: legacyPlan.page || 1 }
              : { id: crypto.randomUUID(), order: 0, name: '地下', type: 'image', src: demoPlan, planFileName: '示範平面圖', page: 1 };
            state.floors = [floor];
            await save('floors', floor);
          }
          state.entries = entries.sort((a, b) => b.createdAt - a.createdAt);
          for (let index = 0; index < state.floors.length; index++) {
            if (!Number.isInteger(state.floors[index].order)) {
              state.floors[index].order = index;
              await save('floors', state.floors[index]);
            }
          }
          for (const entry of state.entries) {
            if (!entry.floorId) {
              entry.floorId = state.floors[0].id;
              await save('entries', entry);
            }
          }
          state.activeFloorId = state.floors[0].id;
          renderFloorTabs();
          await activateFloor(state.activeFloorId);
          renderList();
          renderPins();
        } catch {
          if (!state.floors.length) {
            const floor = { id: crypto.randomUUID(), name: '地下', type: 'image', src: demoPlan, planFileName: '示範平面圖', page: 1 };
            state.floors = [floor];
            state.activeFloorId = floor.id;
          }
          renderFloorTabs();
          await activateFloor(state.activeFloorId);
          toast('本機儲存未能啟用，重新整理後記錄可能消失');
        }
      };
      init();
    })();
  </script>
</body>
</html>

