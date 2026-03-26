<!DOCTYPE html><html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Aviation App</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Rajdhani:wght@600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0a0e1a;--bg2:#0d1520;--bg3:#121e30;
  --border:#1a2d45;--border2:#243d5c;
  --text:#b8ccd8;--text2:#5a7f9a;--text3:#2e4a5f;
  --accent:#00b4d8;--green:#2dc653;--red:#e63946;--yellow:#f0b429;
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;overflow:hidden;}
body{background:var(--bg);color:var(--text);font-family:'Share Tech Mono',monospace;height:100vh;display:flex;flex-direction:column;}
body::before{content:'';position:fixed;inset:0;pointer-events:none;z-index:9999;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.04) 2px,rgba(0,0,0,0.04) 4px);}
::-webkit-scrollbar{width:4px}::-webkit-scrollbar-track{background:var(--bg)}::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
/* HEADER */
#header{background:linear-gradient(90deg,#05080f 0%,#0d1b2e 50%,#05080f 100%);border-bottom:1px solid var(--border2);padding:0 14px;height:54px;flex-shrink:0;display:flex;align-items:center;justify-content:space-between;gap:8px;z-index:100;}
#header-left{display:flex;align-items:center;gap:8px;flex:1;min-width:0;}
#back-btn{background:none;border:none;color:var(--text2);cursor:pointer;font-size:20px;padding:4px 8px;display:none;transition:color .2s;flex-shrink:0;}
#back-btn:hover{color:var(--accent);}
.h-logo{font-family:'Rajdhani',sans-serif;font-weight:700;font-size:15px;color:var(--accent);letter-spacing:3px;flex-shrink:0;}
.h-sep{color:var(--border2);font-size:16px;flex-shrink:0;}
#header-sub{font-size:10px;letter-spacing:2px;color:var(--text2);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
#header-right{display:flex;gap:5px;flex-shrink:0;}
.hbtn{background:rgba(0,180,216,0.08);border:1px solid rgba(0,180,216,0.3);color:var(--accent);cursor:pointer;padding:5px 10px;border-radius:5px;font-family:'Share Tech Mono',monospace;font-size:11px;letter-spacing:1px;transition:all .2s;white-space:nowrap;}
.hbtn:hover{background:rgba(0,180,216,0.2);}
.hbtn.green{background:rgba(45,198,83,0.08);border-color:rgba(45,198,83,0.3);color:var(--green);}
.hbtn.green:hover{background:rgba(45,198,83,0.2);}
.hbtn.red{background:rgba(230,57,70,0.08);border-color:rgba(230,57,70,0.3);color:var(--red);}
.hbtn-plus{font-size:22px;padding:1px 10px;line-height:1;}
/* SCROLL AREA */
#main-scroll{flex:1;overflow-y:auto;overflow-x:hidden;}
/* BREADCRUMB */
#breadcrumb{max-width:700px;margin:0 auto;padding:10px 14px 0;font-size:9px;letter-spacing:2px;color:var(--text3);display:none;}
.bc-link{cursor:pointer;transition:color .2s;}.bc-link:hover{color:var(--text2);}
/* PAGES */
.page{display:none;}.page.active{display:block;}
/* SAVE BANNER */
#save-banner{background:linear-gradient(135deg,#071520,#0d2030);border-top:1px solid var(--border2);padding:8px 14px;flex-shrink:0;}
.save-row{display:flex;gap:6px;margin-bottom:6px;}.save-row .hbtn{flex:1;text-align:center;}
.save-status-row{display:flex;align-items:center;gap:8px;}
.sdot{width:7px;height:7px;border-radius:50%;background:var(--text3);flex-shrink:0;transition:background .4s;}
.sdot.active{background:var(--green);box-shadow:0 0 5px var(--green);}.sdot.saving{background:var(--yellow);animation:blink .7s infinite alternate;}
.slabel{font-size:9px;color:var(--text3);letter-spacing:1px;flex:1;}.slabel.on{color:var(--green);}
@keyframes blink{from{opacity:.4}to{opacity:1}}
/* TAB BAR */
#tab-bar{flex-shrink:0;background:linear-gradient(0deg,#05080f,#0d1b2e);border-top:1px solid var(--border2);display:flex;height:62px;padding-bottom:env(safe-area-inset-bottom,0px);}
.tab-btn{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;cursor:pointer;border:none;background:none;color:var(--text3);font-family:'Share Tech Mono',monospace;font-size:8px;letter-spacing:2px;transition:color .2s;padding:8px 4px;border-top:2px solid transparent;}
.tab-btn:hover{color:var(--text2);}.tab-btn.active{color:var(--accent);border-top-color:var(--accent);}
.tab-icon{font-size:20px;line-height:1;}
/* CHECKLIST STYLES */
#app{max-width:700px;margin:0 auto;padding:16px 14px 20px;}
.view-label{font-size:9px;letter-spacing:3px;color:var(--text3);margin-bottom:18px;}
.ac-card,.cl-card{border-radius:8px;padding:14px 14px 14px 20px;margin-bottom:9px;display:flex;align-items:center;justify-content:space-between;position:relative;overflow:hidden;cursor:pointer;transition:background .2s;}
.ac-card{background:var(--bg2);border:1px solid var(--border);}
.ac-card::before,.cl-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:4px;background:var(--clr,var(--accent));border-radius:8px 0 0 8px;}
.ac-card:hover,.cl-card:hover{background:var(--bg3);}
.cl-card{background:var(--bg2);border:1px solid var(--border);}
.card-info{flex:1;min-width:0;pointer-events:none;}
.card-name{font-family:'Rajdhani',sans-serif;font-weight:700;letter-spacing:2px;color:var(--text);margin-bottom:4px;}
.ac-card .card-name{font-size:17px;}.cl-card .card-name{font-size:14px;}
.card-meta{font-size:9px;color:var(--text2);letter-spacing:1px;}
.card-bar-row{display:flex;align-items:center;gap:8px;margin-top:5px;}
.card-bar{width:100px;height:3px;background:var(--border2);border-radius:2px;overflow:hidden;}
.card-fill{height:100%;border-radius:2px;transition:width .4s;}
.card-count{font-size:9px;color:var(--text2);letter-spacing:1px;}
.card-done{font-size:8px;color:var(--green);letter-spacing:2px;border:1px solid var(--green);padding:1px 6px;border-radius:3px;}
.card-actions{display:flex;gap:5px;flex-shrink:0;pointer-events:auto;}
.icon-btn{background:none;border:1px solid var(--border);color:var(--text2);cursor:pointer;border-radius:4px;padding:4px 8px;font-size:11px;font-family:inherit;transition:all .2s;}
.icon-btn:hover{color:var(--text);border-color:var(--border2);}.icon-btn.del:hover{color:var(--red);border-color:rgba(230,57,70,.5);}
.prog-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;}
.prog-label-text{font-size:9px;letter-spacing:3px;color:var(--text2);}
.prog-bar-wide{width:160px;height:3px;background:var(--border2);border-radius:2px;overflow:hidden;margin-top:5px;}
.prog-fill{height:100%;border-radius:2px;transition:width .4s;}
.item-row{background:var(--bg2);border:1px solid var(--border);border-radius:7px;padding:10px 12px;display:flex;align-items:center;gap:11px;margin-bottom:5px;position:relative;transition:all .2s;}
.item-row.ischecked{background:rgba(45,198,83,0.04);border-color:rgba(45,198,83,0.2);}
.chk-btn{width:26px;height:26px;border-radius:6px;flex-shrink:0;border:2px solid var(--item-clr,var(--accent));background:transparent;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:14px;color:var(--bg);transition:all .15s;}
.chk-btn.on{background:var(--green);border-color:var(--green);}
.item-text{flex:1;font-size:12px;letter-spacing:.5px;color:var(--text);transition:color .2s,opacity .2s;line-height:1.4;}
.item-text.done{color:var(--text3);text-decoration:line-through;opacity:.55;}
.item-actions{display:flex;gap:3px;flex-shrink:0;}
.item-actions button{background:none;border:none;color:var(--text3);cursor:pointer;font-size:12px;padding:2px 5px;transition:color .2s;font-family:inherit;}
.item-actions .edit-item:hover{color:var(--text2);}.item-actions .del-item:hover{color:var(--red);}
.uncheck-overlay{position:absolute;inset:0;border-radius:7px;background:rgba(230,57,70,0.1);border:1px solid rgba(230,57,70,0.45);display:flex;align-items:center;justify-content:center;cursor:pointer;z-index:10;animation:fadeIn .15s ease;}
.uncheck-label{font-size:11px;letter-spacing:2px;color:var(--red);background:var(--bg);padding:4px 16px;border-radius:4px;border:1px solid var(--red);font-family:'Rajdhani',sans-serif;font-weight:700;}
.inline-input{background:var(--bg);border:1px solid var(--accent);color:var(--text);border-radius:4px;padding:3px 8px;font-family:'Share Tech Mono',monospace;font-size:12px;outline:none;width:100%;}
.empty-hint{text-align:center;color:var(--text3);font-size:10px;letter-spacing:2px;margin-top:50px;line-height:2.2;}

/* ═══ ATIS PAGE ═══ */
#page-atis{padding:0;}
.atis-page-inner{max-width:700px;margin:0 auto;}
.atis-hdr{padding:14px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--border);gap:8px;flex-wrap:wrap;}
.atis-hdr-info .title{font-family:'Rajdhani',sans-serif;font-weight:700;font-size:16px;letter-spacing:3px;color:var(--accent);}
.atis-hdr-info .sub{font-size:9px;color:var(--text3);letter-spacing:2px;margin-top:2px;}
.atis-actions{display:flex;gap:6px;flex-wrap:wrap;}

/* Edit mode toggle */
.edit-mode-bar{display:flex;align-items:center;justify-content:space-between;padding:8px 14px;background:rgba(0,180,216,0.05);border-bottom:1px solid var(--border);}
.edit-mode-label{font-size:9px;letter-spacing:2px;color:var(--text2);}
.edit-mode-btn{background:rgba(0,180,216,0.1);border:1px solid rgba(0,180,216,0.3);color:var(--accent);cursor:pointer;padding:5px 12px;border-radius:5px;font-family:'Share Tech Mono',monospace;font-size:10px;letter-spacing:1px;transition:all .2s;}
.edit-mode-btn.active{background:rgba(240,180,41,0.15);border-color:rgba(240,180,41,0.4);color:var(--yellow);}
.add-field-btn{background:rgba(45,198,83,0.08);border:1px solid rgba(45,198,83,0.3);color:var(--green);cursor:pointer;padding:5px 12px;border-radius:5px;font-family:'Share Tech Mono',monospace;font-size:11px;letter-spacing:1px;transition:all .2s;}
.add-field-btn:hover{background:rgba(45,198,83,0.2);}

/* Field wrapper in edit mode */
.atis-fields{padding:14px;display:flex;flex-direction:column;gap:10px;}
.atis-field-wrap{position:relative;}
.atis-field-wrap.edit-active .atis-field{border-color:rgba(240,180,41,0.4);box-shadow:0 0 0 1px rgba(240,180,41,0.15);}
.field-del-btn{position:absolute;top:50%;right:-14px;transform:translateY(-50%);width:26px;height:26px;border-radius:50%;background:rgba(230,57,70,0.15);border:1px solid rgba(230,57,70,0.5);color:var(--red);cursor:pointer;font-size:14px;display:none;align-items:center;justify-content:center;z-index:10;transition:all .2s;line-height:1;}
.field-del-btn:hover{background:rgba(230,57,70,0.3);}
.edit-active .field-del-btn{display:flex;}
.atis-field{background:var(--bg2);border:1px solid var(--border);border-radius:8px;overflow:hidden;transition:border-color .2s,box-shadow .2s;}
.atis-field-hdr{display:flex;align-items:center;justify-content:space-between;padding:8px 12px;border-bottom:1px solid var(--border);background:rgba(0,0,0,0.2);}
.atis-field-label-wrap{display:flex;align-items:center;gap:8px;flex:1;}
.atis-field-label{font-size:9px;letter-spacing:3px;color:var(--text2);}
.label-edit-inp{background:var(--bg);border:1px solid var(--accent);color:var(--text);border-radius:4px;padding:2px 8px;font-family:'Share Tech Mono',monospace;font-size:9px;letter-spacing:2px;outline:none;width:180px;}
.atis-clear-btn{background:none;border:none;color:var(--text3);cursor:pointer;font-size:10px;padding:2px 6px;font-family:inherit;transition:color .2s;letter-spacing:1px;}
.atis-clear-btn:hover{color:var(--red);}
.ai-status{font-size:8px;letter-spacing:1px;padding:2px 8px;border-radius:3px;border:1px solid transparent;transition:all .3s;display:inline-block;}
.ai-status.ok{color:var(--green);border-color:rgba(45,198,83,0.4);background:rgba(45,198,83,0.08);}
.ai-status.warn{color:var(--yellow);border-color:rgba(240,180,41,0.4);background:rgba(240,180,41,0.08);}
.ai-status.err{color:var(--red);border-color:rgba(230,57,70,0.4);background:rgba(230,57,70,0.08);}
.atis-inp{width:100%;background:transparent;border:none;color:var(--text);font-family:'Share Tech Mono',monospace;font-size:13px;padding:10px 12px;outline:none;resize:none;line-height:1.6;min-height:44px;}
.atis-inp::placeholder{color:var(--text3);}

/* ═══ CANVAS ═══ */
.canvas-field-container{position:relative;}
.canvas-expand-btn{position:absolute;top:8px;right:8px;z-index:20;background:rgba(0,180,216,0.15);border:1px solid rgba(0,180,216,0.4);color:var(--accent);cursor:pointer;padding:4px 10px;border-radius:4px;font-family:'Share Tech Mono',monospace;font-size:9px;letter-spacing:1px;transition:all .2s;}
.canvas-expand-btn:hover{background:rgba(0,180,216,0.3);}
.canvas-wrap{position:relative;background:#070d18;}
.canvas-wrap canvas{display:block;width:100%;touch-action:none;cursor:crosshair;}
.canvas-toolbar{display:flex;align-items:center;gap:6px;padding:8px 10px;background:rgba(0,0,0,0.35);border-top:1px solid var(--border);flex-wrap:wrap;}
.c-swatch{width:22px;height:22px;border-radius:50%;cursor:pointer;border:2px solid transparent;transition:all .15s;flex-shrink:0;}
.c-swatch:hover{transform:scale(1.1);}.c-swatch.sel{border-color:#fff;transform:scale(1.15);}
.c-sep{color:var(--border2);margin:0 3px;flex-shrink:0;}
.c-sz-btn{background:rgba(0,180,216,0.06);border:1px solid var(--border2);color:var(--text2);cursor:pointer;padding:3px 8px;border-radius:4px;font-family:'Share Tech Mono',monospace;font-size:9px;transition:all .2s;}
.c-sz-btn.active{background:rgba(0,180,216,0.18);color:var(--accent);border-color:rgba(0,180,216,0.4);}
.c-tool-btn{background:rgba(0,180,216,0.06);border:1px solid var(--border2);color:var(--text2);cursor:pointer;padding:4px 9px;border-radius:4px;font-family:'Share Tech Mono',monospace;font-size:9px;letter-spacing:1px;transition:all .2s;}
.c-tool-btn:hover,.c-tool-btn.active{background:rgba(0,180,216,0.18);color:var(--accent);border-color:rgba(0,180,216,0.4);}
.c-tool-btn.eraser.active{background:rgba(240,180,41,0.15);color:var(--yellow);border-color:rgba(240,180,41,0.4);}
.c-tool-btn.danger:hover{background:rgba(230,57,70,0.15);color:var(--red);border-color:rgba(230,57,70,0.4);}
.c-tool-btn.ai-btn{background:rgba(116,76,241,0.1);border-color:rgba(116,76,241,0.4);color:#a78bfa;}
.c-tool-btn.ai-btn:hover,.c-tool-btn.ai-btn.active{background:rgba(116,76,241,0.25);border-color:rgba(116,76,241,0.7);color:#c4b5fd;}

/* Fullscreen canvas overlay */
#canvas-fullscreen{position:fixed;inset:0;z-index:500;background:var(--bg);display:none;flex-direction:column;}
#canvas-fullscreen.open{display:flex;}
#canvas-fs-header{background:linear-gradient(90deg,#05080f,#0d1b2e);border-bottom:1px solid var(--border2);padding:0 14px;height:50px;flex-shrink:0;display:flex;align-items:center;justify-content:space-between;}
#canvas-fs-title{font-family:'Rajdhani',sans-serif;font-weight:700;font-size:14px;letter-spacing:3px;color:var(--accent);}
#canvas-fs-close{background:rgba(230,57,70,0.1);border:1px solid rgba(230,57,70,0.4);color:var(--red);cursor:pointer;padding:6px 14px;border-radius:5px;font-family:'Share Tech Mono',monospace;font-size:10px;letter-spacing:1px;transition:all .2s;}
#canvas-fs-close:hover{background:rgba(230,57,70,0.25);}
#canvas-fs-body{flex:1;overflow:hidden;display:flex;flex-direction:column;}
#canvas-fs-wrap{flex:1;position:relative;background:#070d18;overflow:hidden;}
#canvas-fs-wrap canvas{position:absolute;top:0;left:0;touch-action:none;cursor:crosshair;}
#canvas-fs-toolbar{background:rgba(0,0,0,0.5);border-top:1px solid var(--border);padding:8px 12px;display:flex;align-items:center;gap:6px;flex-wrap:wrap;flex-shrink:0;}

/* AI Spinner */
.ai-spinner{display:inline-block;width:10px;height:10px;border:2px solid rgba(167,139,250,0.3);border-top-color:#a78bfa;border-radius:50%;animation:spin .6s linear infinite;vertical-align:middle;margin-right:4px;}
@keyframes spin{to{transform:rotate(360deg)}}

/* TOAST */
#toast{position:fixed;bottom:80px;left:50%;transform:translateX(-50%);background:#0d2a1a;border:1px solid var(--green);color:var(--green);padding:9px 20px;border-radius:8px;font-size:11px;letter-spacing:2px;z-index:9000;pointer-events:none;opacity:0;transition:opacity .35s;white-space:nowrap;}
#toast.show{opacity:1;}#toast.warn{background:#1a1205;border-color:var(--yellow);color:var(--yellow);}

/* MODALS */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.82);display:none;align-items:center;justify-content:center;z-index:800;padding:20px;}
.modal-overlay.open{display:flex;}
.modal{background:var(--bg2);border:1px solid var(--border2);border-radius:12px;padding:22px;width:100%;max-width:390px;animation:slideUp .2s ease;max-height:90vh;overflow-y:auto;}
.modal-hdr{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px;}
.modal-title{font-size:10px;letter-spacing:3px;color:var(--text2);}
.modal-x{background:none;border:none;color:var(--text2);cursor:pointer;font-size:20px;line-height:1;transition:color .2s;}.modal-x:hover{color:var(--red);}
.flabel{display:block;font-size:9px;letter-spacing:2px;color:var(--text2);margin-bottom:6px;}
.finput{width:100%;background:var(--bg);border:1px solid var(--border2);color:var(--text);border-radius:6px;padding:10px 12px;font-family:'Share Tech Mono',monospace;font-size:13px;margin-bottom:14px;outline:none;transition:border-color .2s;}
.finput:focus{border-color:var(--accent);}
.ftip{font-size:9px;color:var(--text3);letter-spacing:1px;margin:-8px 0 14px;line-height:1.7;}
.color-grid{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:18px;}
.cdot{width:26px;height:26px;border-radius:50%;cursor:pointer;border:2px solid transparent;transition:all .15px;}
.cdot:hover{transform:scale(1.1);}.cdot.sel{border-color:#fff;transform:scale(1.15);}
.btn-row{display:flex;gap:8px;}
.btn-ok{flex:1;background:rgba(0,180,216,0.1);border:1px solid rgba(0,180,216,0.4);color:var(--accent);cursor:pointer;padding:11px;border-radius:6px;font-family:'Share Tech Mono',monospace;font-size:11px;letter-spacing:2px;transition:all .2s;}
.btn-ok:hover{background:rgba(0,180,216,0.22);}
.btn-cancel{flex:1;background:rgba(90,127,154,0.08);border:1px solid var(--border2);color:var(--text2);cursor:pointer;padding:11px;border-radius:6px;font-family:'Share Tech Mono',monospace;font-size:11px;letter-spacing:1px;transition:all .2s;}
.btn-cancel:hover{background:rgba(90,127,154,0.2);}
.btn-danger{flex:1;background:rgba(230,57,70,0.1);border:1px solid rgba(230,57,70,0.4);color:var(--red);cursor:pointer;padding:11px;border-radius:6px;font-family:'Share Tech Mono',monospace;font-size:11px;letter-spacing:1px;transition:all .2s;}
.btn-danger:hover{background:rgba(230,57,70,0.22);}
.confirm-icon{font-size:26px;text-align:center;margin-bottom:8px;}
.confirm-msg{font-size:12px;color:var(--text2);line-height:1.9;margin-bottom:20px;text-align:center;letter-spacing:.4px;}
.confirm-msg b{color:var(--text);}

/* Add field modal */
.type-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:14px;}
.type-opt{background:var(--bg);border:1px solid var(--border2);color:var(--text2);cursor:pointer;padding:10px;border-radius:6px;font-family:'Share Tech Mono',monospace;font-size:10px;letter-spacing:1px;transition:all .2s;text-align:center;}
.type-opt:hover,.type-opt.sel{border-color:var(--accent);color:var(--accent);background:rgba(0,180,216,0.08);}

@keyframes fadeIn{from{opacity:0}to{opacity:1}}
@keyframes slideUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:none}}
</style>
</head>
<body>

<div id="header">
  <div id="header-left">
    <button id="back-btn" onclick="goBack()">&#8592;</button>
    <span class="h-logo">AVIATION</span>
    <span class="h-sep">|</span>
    <span id="header-sub">CHECKLISTEN</span>
  </div>
  <div id="header-right">
    <button class="hbtn red" id="reset-btn" style="display:none" onclick="askReset()">RESET</button>
    <button class="hbtn hbtn-plus" id="add-btn" onclick="onAdd()">+</button>
  </div>
</div>

<div id="breadcrumb"></div>

<div id="main-scroll">

  <!-- CHECKLISTEN -->
  <div id="page-checklists" class="page active">
    <div id="app">
      <div id="view-aircraft"></div>
      <div id="view-checklists" style="display:none"></div>
      <div id="view-items" style="display:none"></div>
    </div>
  </div>

  <!-- ATIS & NOTIZEN -->
  <div id="page-atis" class="page">
    <div class="atis-page-inner">
      <div class="atis-hdr">
        <div class="atis-hdr-info">
          <div class="title">ATIS &amp; NOTIZEN</div>
          <div class="sub">IFR CLEARANCE · HANDSCHRIFT · KI-ERKENNUNG</div>
        </div>
        <div class="atis-actions">
          <button class="hbtn" onclick="clearAllAtis()">&#10006; ALLE</button>
          <button class="hbtn green" onclick="atisManualSave()">&#8595; SPEICHERN</button>
        </div>
      </div>

      <!-- Edit mode bar -->
      <div class="edit-mode-bar">
        <span class="edit-mode-label">FELDER VERWALTEN</span>
        <div style="display:flex;gap:6px;">
          <button class="add-field-btn" id="add-field-btn" onclick="openAddFieldModal()" style="display:none">+ FELD</button>
          <button class="edit-mode-btn" id="edit-mode-btn" onclick="toggleEditMode()">✎ BEARBEITEN</button>
        </div>
      </div>

      <div class="atis-fields" id="atis-fields"></div>
    </div>
  </div>

</div>

<!-- SAVE BANNER -->
<div id="save-banner">
  <div class="save-row">
    <button class="hbtn" onclick="loadFile()">&#8593; LADEN</button>
    <button class="hbtn green" onclick="saveFile()">&#8595; SPEICHERN</button>
  </div>
  <div class="save-status-row">
    <div class="sdot" id="sdot"></div>
    <span class="slabel" id="slabel">BEREIT</span>
    <span id="linked-name" style="font-size:9px;color:var(--text2);letter-spacing:1px;margin-left:auto;max-width:150px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;"></span>
  </div>
</div>

<input type="file" id="file-input" accept=".json" style="display:none" onchange="onFileChosen(event)">

<div id="tab-bar">
  <button class="tab-btn active" id="tab-cl" onclick="switchTab('cl')">
    <span class="tab-icon">&#9989;</span>CHECKLISTEN
  </button>
  <button class="tab-btn" id="tab-atis" onclick="switchTab('atis')">
    <span class="tab-icon">&#128203;</span>ATIS &amp; NOTIZEN
  </button>
</div>

<div id="toast"></div>

<!-- ═══ FULLSCREEN CANVAS OVERLAY ═══ -->
<div id="canvas-fullscreen">
  <div id="canvas-fs-header">
    <span id="canvas-fs-title">&#9998; HANDSCHRIFT / IFR CLEARANCE</span>
    <div style="display:flex;gap:8px;align-items:center;">
      <span id="canvas-fs-ai-status" class="ai-status" style="display:none;"></span>
      <button id="canvas-fs-ai-btn" class="c-tool-btn ai-btn" onclick="runAiRecognition(true)">&#129504; KI ERKENNEN</button>
      <button id="canvas-fs-close" onclick="closeCanvasFullscreen()">&#10005; SCHLIESSEN</button>
    </div>
  </div>
  <div id="canvas-fs-body">
    <div id="canvas-fs-wrap"></div>
    <div id="canvas-fs-toolbar"></div>
  </div>
</div>

<!-- Aircraft Modal -->
<div class="modal-overlay" id="m-aircraft">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-title" id="m-ac-title">NEUES FLUGZEUG</span><button class="modal-x" onclick="closeModal('m-aircraft')">&#10005;</button></div>
    <label class="flabel">NAME / TYP</label><input class="finput" id="inp-ac-name" placeholder="z.B. Airbus A320">
    <label class="flabel">BESCHREIBUNG</label><input class="finput" id="inp-ac-desc" placeholder="z.B. CFM56, SOP Rev4">
    <label class="flabel">FARBE</label><div class="color-grid" id="cg-ac"></div>
    <div class="btn-row"><button class="btn-cancel" onclick="closeModal('m-aircraft')">ABBRECHEN</button><button class="btn-ok" onclick="submitAircraft()">BESTÄTIGEN ✓</button></div>
  </div>
</div>

<!-- Checklist Modal -->
<div class="modal-overlay" id="m-checklist">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-title" id="m-cl-title">NEUE CHECKLISTE</span><button class="modal-x" onclick="closeModal('m-checklist')">&#10005;</button></div>
    <label class="flabel">NAME</label><input class="finput" id="inp-cl-name" placeholder="z.B. Lineup Checklist">
    <label class="flabel">FARBE</label><div class="color-grid" id="cg-cl"></div>
    <div class="btn-row"><button class="btn-cancel" onclick="closeModal('m-checklist')">ABBRECHEN</button><button class="btn-ok" onclick="submitChecklist()">BESTÄTIGEN ✓</button></div>
  </div>
</div>

<!-- Item Modal -->
<div class="modal-overlay" id="m-item">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-title">NEUER SCHRITT</span><button class="modal-x" onclick="closeModal('m-item')">&#10005;</button></div>
    <label class="flabel">SCHRITT / AUFGABE</label>
    <input class="finput" id="inp-item-text" placeholder="z.B. Flaps – [Stellung eintragen]">
    <p class="ftip">TIPP: Nutze [Klammern] für Eingabefelder</p>
    <div class="btn-row"><button class="btn-cancel" onclick="closeModal('m-item')">ABBRECHEN</button><button class="btn-ok" onclick="submitItem()">HINZUFÜGEN</button></div>
  </div>
</div>

<!-- Confirm Modal -->
<div class="modal-overlay" id="m-confirm">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-title" id="confirm-title">BESTÄTIGUNG</span><button class="modal-x" onclick="closeModal('m-confirm')">&#10005;</button></div>
    <div class="confirm-icon" id="confirm-icon">&#128465;</div>
    <p class="confirm-msg" id="confirm-msg"></p>
    <div class="btn-row"><button class="btn-cancel" onclick="closeModal('m-confirm')">ABBRECHEN</button><button class="btn-danger" id="confirm-ok">OK</button></div>
  </div>
</div>

<!-- Add Field Modal -->
<div class="modal-overlay" id="m-add-field">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-title">NEUES FELD HINZUFÜGEN</span><button class="modal-x" onclick="closeModal('m-add-field')">&#10005;</button></div>
    <label class="flabel">BEZEICHNUNG</label>
    <input class="finput" id="inp-new-field-label" placeholder="z.B. DEPARTURE FREQUENCY">
    <label class="flabel">FELDTYP</label>
    <div class="type-grid">
      <div class="type-opt sel" data-type="text" onclick="selectNewFieldType('text',this)">&#9646; TEXTZEILE</div>
      <div class="type-opt" data-type="textarea" onclick="selectNewFieldType('textarea',this)">&#9644; TEXTAREA</div>
    </div>
    <div class="btn-row"><button class="btn-cancel" onclick="closeModal('m-add-field')">ABBRECHEN</button><button class="btn-ok" onclick="submitNewField()">HINZUFÜGEN</button></div>
  </div>
</div>

<script>
// ═══════════════════════════════════════
// DEFAULT DATA
// ═══════════════════════════════════════
const DEFAULT_CL = [
  { id:"a320", name:"Airbus A320", desc:"CFM56 / IAE V2500", color:"#00b4d8", checklists:[
    { id:"preflight", name:"Pre-Flight", color:"#00b4d8", items:[
      {id:1,t:"Cockpit Preparation – COMPLETE"},{id:2,t:"Preliminary Cockpit Check – DONE"},
      {id:3,t:"Fire Test – TESTED"},{id:4,t:"Exterior Walkround – COMPLETE"},
      {id:5,t:"Documents & Manuals – ON BOARD"},{id:6,t:"Fuel Check – [Menge in kg]"},
      {id:7,t:"ATIS – [Flughafen ICAO]"},{id:8,t:"Clearance – OBTAINED"},
    ]},
    { id:"before-start", name:"Before Start", color:"#f4a261", items:[
      {id:1,t:"Parking Brake – SET"},{id:2,t:"Beacon Light – ON"},
      {id:3,t:"ADIRS – NAV"},{id:4,t:"Baro Reference – [QNH]"},
      {id:5,t:"Windows & Doors – CLOSED"},{id:6,t:"Thrust Levers – IDLE"},
      {id:7,t:"Hydraulics – CHECK"},{id:8,t:"PAX Signs – ON"},
      {id:9,t:"FMS – CHECKED"},{id:10,t:"Departure Runway – [Runway]"},
    ]},
    { id:"after-start", name:"After Start", color:"#2dc653", items:[
      {id:1,t:"Engines – RUNNING"},{id:2,t:"Anti Ice – [CHECK / AS REQ]"},
      {id:3,t:"Electrical Power – NORMAL"},{id:4,t:"Ground Spoilers – ARMED"},
      {id:5,t:"Flaps – [Stellung]"},{id:6,t:"Pitch Trim – SET"},{id:7,t:"Rudder Trim – ZERO"},
    ]},
    { id:"taxi", name:"Taxi", color:"#e9c46a", items:[
      {id:1,t:"Taxi Clearance – RECEIVED"},{id:2,t:"Nose Wheel Steering – CHECK"},
      {id:3,t:"Brakes – CHECK"},{id:4,t:"Transponder – TA/RA"},{id:5,t:"Runway – [Runway]"},
    ]},
    { id:"lineup", name:"Lineup Checklist", color:"#e63946", items:[
      {id:1,t:"Flight Controls – CHECKED"},{id:2,t:"Flaps / Slats – [Stellung / GREEN]"},
      {id:3,t:"V1 / VR / V2 – [Werte]"},{id:4,t:"Transponder – TA/RA"},
      {id:5,t:"TCAS – TA/RA"},{id:6,t:"Cabin – SECURED"},
      {id:7,t:"Packs – [AS REQUIRED]"},{id:8,t:"Strobe Lights – ON"},{id:9,t:"Autothrust – ARMED"},
    ]},
    { id:"takeoff", name:"Takeoff / Climb", color:"#ff6b35", items:[
      {id:1,t:"Thrust Levers – FLEX / TOGA"},{id:2,t:"80 kt – CHECK"},
      {id:3,t:"V1 – ROTATE AT VR"},{id:4,t:"Positive Climb – GEAR UP"},
      {id:5,t:"Flaps – RETRACT ON SCHEDULE"},{id:6,t:"Packs – ON (above 1500 ft)"},{id:7,t:"Altimeter – [STD above TA]"},
    ]},
    { id:"descent", name:"Descent / Approach", color:"#457b9d", items:[
      {id:1,t:"Descent Briefing – COMPLETED"},{id:2,t:"ATIS – [Destination ICAO]"},
      {id:3,t:"Altimeter – QNH SET [Wert]"},{id:4,t:"Anti Ice – AS REQUIRED"},
      {id:5,t:"Minima – [DA / MDA]"},{id:6,t:"ILS / Approach – SET"},{id:7,t:"Approach Briefing – COMPLETED"},
    ]},
    { id:"landing", name:"Landing", color:"#f0b429", items:[
      {id:1,t:"Cabin – SECURED"},{id:2,t:"Landing Gear – DOWN & LOCKED"},
      {id:3,t:"Flaps – [Stellung]"},{id:4,t:"Ground Spoilers – ARMED"},
      {id:5,t:"Autobrake – [Stufe]"},{id:6,t:"Landing Lights – ON"},{id:7,t:"Go-Around Altitude – SET"},
    ]},
    { id:"after-landing", name:"After Landing", color:"#38b000", items:[
      {id:1,t:"Thrust Reversers – STOWED"},{id:2,t:"Spoilers – DISARMED / RETRACTED"},
      {id:3,t:"Flaps – RETRACTED"},{id:4,t:"Transponder – STBY"},
      {id:5,t:"Landing Lights – OFF"},{id:6,t:"APU – START (if needed)"},{id:7,t:"Taxi Lights – ON"},
    ]},
    { id:"shutdown", name:"Engine Shutdown", color:"#6c757d", items:[
      {id:1,t:"Parking Brake – SET"},{id:2,t:"Engine Masters 1 & 2 – OFF"},
      {id:3,t:"Seat Belt Signs – OFF"},{id:4,t:"Exterior Lights – OFF"},
      {id:5,t:"Fuel Pumps – OFF"},{id:6,t:"ADIRS – OFF"},
      {id:7,t:"APU Bleed – ON (ground power)"},{id:8,t:"Log – COMPLETED [Eintrag]"},
    ]},
  ]},
];

// Default ATIS fields with IFR Clearance structure
const DEFAULT_ATIS_FIELDS = [
  {id:'airport',   label:'FLUGHAFEN / ICAO',          type:'text',     ph:'z.B. EDDF, LSZH …',            aiTarget:null},
  {id:'atis_id',   label:'ATIS INFORMATION',           type:'text',     ph:'z.B. ALPHA',                    aiTarget:'atis_id'},
  {id:'wind',      label:'WIND',                       type:'text',     ph:'z.B. 270° / 12 kt',             aiTarget:'wind'},
  {id:'vis',       label:'SICHT / WETTER',             type:'text',     ph:'z.B. 9999 m, SCT035',           aiTarget:'vis'},
  {id:'temp',      label:'TEMPERATUR / TAUPUNKT',      type:'text',     ph:'z.B. +12° / +08°',             aiTarget:'temp'},
  {id:'qnh',       label:'QNH',                        type:'text',     ph:'z.B. 1013 hPa',                 aiTarget:'qnh'},
  {id:'rwy',       label:'AKTIVE RUNWAY',              type:'text',     ph:'z.B. 28L Ab, 28R An',           aiTarget:'rwy'},
  {id:'clearance', label:'DEPARTURE CLEARANCE',        type:'textarea', ph:'Route / SID / Anweisungen …',   aiTarget:'clearance'},
  {id:'squawk',    label:'SQUAWK',                     type:'text',     ph:'z.B. 2541',                     aiTarget:'squawk'},
  {id:'init_climb',label:'INITIAL CLIMB',              type:'text',     ph:'z.B. FL100 / 5000ft',           aiTarget:'init_climb'},
  {id:'freq_del',  label:'DELIVERY FREQUENCY',         type:'text',     ph:'z.B. 121.905 MHz',              aiTarget:null},
  {id:'freq_gnd',  label:'GROUND FREQUENCY',           type:'text',     ph:'z.B. 121.800 MHz',              aiTarget:null},
  {id:'freq_twr',  label:'TOWER FREQUENCY',            type:'text',     ph:'z.B. 119.900 MHz',              aiTarget:null},
  {id:'freq_dep',  label:'DEPARTURE FREQUENCY',        type:'text',     ph:'z.B. 127.725 MHz',              aiTarget:'freq_dep'},
  {id:'notes',     label:'FREIE NOTIZEN / NOTAMs',     type:'textarea', ph:'Wichtige Infos, NOTAMs …',      aiTarget:null},
  {id:'draw',      label:'HANDSCHRIFT / IFR CLEARANCE',type:'canvas',   ph:'',                              aiTarget:null},
];

const PALETTE = ["#00b4d8","#f4a261","#2dc653","#e63946","#7b2d8b","#e9c46a","#457b9d","#ff6b35","#38b000","#6c757d","#e76f51","#264653","#f72585","#4cc9f0","#b5838d"];

// ═══════════════════════════════════════
// STATE
// ═══════════════════════════════════════
let clData    = JSON.parse(JSON.stringify(DEFAULT_CL));
let clChecked = {};
let nav = [];
let pendingUncheck = null, pendingTimer = null;
let editAcId = null, editClId = null;
let selAcColor = PALETTE[0], selClColor = PALETTE[3];
let confirmCb = null;
let currentTab = 'cl';

// ATIS
let atisFields  = JSON.parse(JSON.stringify(DEFAULT_ATIS_FIELDS)); // mutable copy
let atisValues  = {};
let atisImgData = null;
let atisBuilt   = false;
let editMode    = false;
let newFieldType= 'text';

// Canvas
let atisCanvas = null, atisCtx = null;
let fsCanvas   = null, fsCtx   = null;
let drawState  = { on:false, color:'#00b4d8', size:2, tool:'pen', lx:0, ly:0 };
let canvasFullscreen = false;

// File
let fileHandle = null, lastSaved = '', saveTimer = null;

// ═══════════════════════════════════════
// TAB SWITCHING
// ═══════════════════════════════════════
function switchTab(tab) {
  currentTab = tab;
  document.getElementById('page-checklists').classList.toggle('active', tab==='cl');
  document.getElementById('page-atis').classList.toggle('active', tab==='atis');
  document.getElementById('tab-cl').classList.toggle('active', tab==='cl');
  document.getElementById('tab-atis').classList.toggle('active', tab==='atis');
  document.getElementById('save-banner').style.display = tab==='cl' ? '' : 'none';
  document.getElementById('add-btn').style.display = tab==='cl' ? '' : 'none';
  document.getElementById('reset-btn').style.display = (tab==='cl' && nav.length===2) ? '' : 'none';
  document.getElementById('back-btn').style.display = (tab==='cl' && nav.length>0) ? 'inline-block' : 'none';
  document.getElementById('breadcrumb').style.display = (tab==='cl' && nav.length>0) ? '' : 'none';
  document.getElementById('header-sub').textContent = tab==='cl' ? clHeaderSub() : 'ATIS & NOTIZEN';
  if (tab==='atis') buildAtisPage();
}

function clHeaderSub() {
  if (!nav.length) return 'CHECKLISTEN';
  const ac = clData.find(a=>a.id===nav[0]);
  if (nav.length===1) return ac ? ac.name.toUpperCase() : 'CHECKLISTEN';
  const cl = ac && ac.checklists.find(c=>c.id===nav[1]);
  return cl ? cl.name.toUpperCase() : 'CHECKLISTEN';
}

// ═══════════════════════════════════════
// LOCAL STORAGE
// ═══════════════════════════════════════
const LS = 'aviation_v5';

function buildPayload() {
  if (atisCanvas) atisImgData = atisCanvas.toDataURL();
  if (fsCanvas)   atisImgData = fsCanvas.toDataURL();
  return JSON.stringify({ clData, clChecked, atisValues, atisImgData, atisFields }, null, 2);
}

function saveLS() {
  try { localStorage.setItem(LS, buildPayload()); } catch(e){}
}

function loadLS() {
  try {
    const raw = localStorage.getItem(LS);
    if (!raw) return false;
    const p = JSON.parse(raw);
    const d = p.clData || p.data;
    if (!d || !Array.isArray(d)) return false;
    clData     = d;
    clChecked  = p.clChecked || p.checked || {};
    atisValues = p.atisValues || {};
    atisImgData= p.atisImgData || null;
    if (p.atisFields && Array.isArray(p.atisFields)) atisFields = p.atisFields;
    return true;
  } catch(e){ return false; }
}

function onChanged() {
  saveLS();
  if (fileHandle) { clearTimeout(saveTimer); saveTimer = setTimeout(writeFile, 700); }
}

// ═══════════════════════════════════════
// FILE OPERATIONS
// ═══════════════════════════════════════
function setSaveStatus(state) {
  const dot=document.getElementById('sdot'), lbl=document.getElementById('slabel'), nm=document.getElementById('linked-name');
  if (state==='saving')  { dot.className='sdot saving'; lbl.className='slabel'; lbl.textContent='SPEICHERT …'; }
  else if (state==='saved') { dot.className='sdot active'; lbl.className='slabel on'; const t=new Date(); lbl.textContent='GESPEICHERT '+t.getHours().toString().padStart(2,'0')+':'+t.getMinutes().toString().padStart(2,'0')+':'+t.getSeconds().toString().padStart(2,'0'); }
  else if (state==='linked') { dot.className='sdot active'; lbl.className='slabel on'; lbl.textContent='AUTO-ÜBERSCHREIBEN AKTIV'; nm.textContent=fileHandle?fileHandle.name:''; }
  else if (state==='error')  { dot.className='sdot'; lbl.className='slabel'; lbl.textContent='⚠ FEHLER'; }
  else { dot.className='sdot active'; lbl.className='slabel on'; lbl.textContent='BEREIT'; }
}

async function writeFile() {
  if (!fileHandle) return;
  const payload = buildPayload();
  if (payload===lastSaved) return;
  setSaveStatus('saving');
  try {
    let perm = await fileHandle.queryPermission({mode:'readwrite'});
    if (perm!=='granted') perm = await fileHandle.requestPermission({mode:'readwrite'});
    if (perm!=='granted') { setSaveStatus('error'); return; }
    const w = await fileHandle.createWritable();
    await w.write(payload); await w.close();
    lastSaved = payload; setSaveStatus('linked');
  } catch(e) { setSaveStatus('error'); }
}

async function loadFile() {
  if (window.showOpenFilePicker) {
    try {
      const [h] = await window.showOpenFilePicker({ types:[{description:'Aviation JSON',accept:{'application/json':['.json']}}], multiple:false });
      const txt = await (await h.getFile()).text();
      if (applyPayload(txt)) { fileHandle=h; lastSaved=buildPayload(); setSaveStatus('linked'); showToast('✓ GELADEN – AUTO-ÜBERSCHREIBEN AKTIV'); }
      return;
    } catch(e) { if (e.name==='AbortError') return; }
  }
  document.getElementById('file-input').click();
}

function onFileChosen(evt) {
  const f=evt.target.files[0]; if (!f) return;
  const r=new FileReader();
  r.onload=e=>{ if (applyPayload(e.target.result)) { showToast('✓ DATEN GELADEN'); setSaveStatus('saved'); } };
  r.readAsText(f); evt.target.value='';
}

function applyPayload(txt) {
  try {
    const p=JSON.parse(txt);
    const d=p.clData||p.data;
    if (!d||!Array.isArray(d)) { showToast('⚠ UNGÜLTIGE DATEI',true); return false; }
    clData=d; clChecked=p.clChecked||p.checked||{}; atisValues=p.atisValues||{}; atisImgData=p.atisImgData||null;
    if (p.atisFields&&Array.isArray(p.atisFields)) atisFields=p.atisFields;
    nav=[]; saveLS(); renderCL();
    if (currentTab==='atis') { atisBuilt=false; buildAtisPage(); }
    return true;
  } catch(e) { showToast('⚠ LADEFEHLER',true); return false; }
}

async function saveFile() {
  if (fileHandle) { lastSaved=''; await writeFile(); return; }
  const payload=buildPayload();
  const fname='aviation-'+new Date().toISOString().slice(0,10)+'.json';
  if (window.showSaveFilePicker) {
    try {
      const h=await window.showSaveFilePicker({ suggestedName:fname, types:[{description:'Aviation JSON',accept:{'application/json':['.json']}}] });
      fileHandle=h; lastSaved=''; await writeFile(); setSaveStatus('linked'); return;
    } catch(e) { if (e.name==='AbortError') return; }
  }
  const blob=new Blob([payload],{type:'application/json'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a'); a.href=url; a.download=fname;
  document.body.appendChild(a); a.click(); document.body.removeChild(a); URL.revokeObjectURL(url);
  lastSaved=payload; setSaveStatus('saved'); showToast('✓ DATEI HERUNTERGELADEN');
}

window.addEventListener('beforeunload',()=>{ saveLS(); if(fileHandle) writeFile(); });
window.addEventListener('pagehide',    ()=>{ saveLS(); if(fileHandle) writeFile(); });
setInterval(()=>{ if(fileHandle) writeFile(); }, 5000);

// ═══════════════════════════════════════
// EDIT MODE (ATIS)
// ═══════════════════════════════════════
function toggleEditMode() {
  editMode = !editMode;
  const btn = document.getElementById('edit-mode-btn');
  const addBtn = document.getElementById('add-field-btn');
  btn.textContent = editMode ? '✓ FERTIG' : '✎ BEARBEITEN';
  btn.classList.toggle('active', editMode);
  addBtn.style.display = editMode ? '' : 'none';

  // Show/hide del buttons and label editors
  document.querySelectorAll('.atis-field-wrap').forEach(w=>{
    w.classList.toggle('edit-active', editMode);
  });

  // Toggle label edit inputs
  document.querySelectorAll('.atis-field-label').forEach(lbl=>{
    lbl.style.display = editMode ? 'none' : '';
  });
  document.querySelectorAll('.label-edit-inp').forEach(inp=>{
    inp.style.display = editMode ? '' : 'none';
  });
}

// Add field modal
function openAddFieldModal() {
  newFieldType = 'text';
  document.getElementById('inp-new-field-label').value = '';
  document.querySelectorAll('.type-opt').forEach(o=>o.classList.toggle('sel', o.dataset.type==='text'));
  openModal('m-add-field');
  setTimeout(()=>document.getElementById('inp-new-field-label').focus(),50);
}

function selectNewFieldType(type, el) {
  newFieldType = type;
  document.querySelectorAll('.type-opt').forEach(o=>o.classList.remove('sel'));
  el.classList.add('sel');
}

function submitNewField() {
  const label = document.getElementById('inp-new-field-label').value.trim();
  if (!label) return;
  const id = 'custom_' + Date.now();
  const newField = { id, label, type: newFieldType, ph: '', aiTarget: null };
  // Insert before the canvas field
  const canvasIdx = atisFields.findIndex(f=>f.type==='canvas');
  if (canvasIdx >= 0) atisFields.splice(canvasIdx, 0, newField);
  else atisFields.push(newField);
  closeModal('m-add-field');
  // Rebuild page
  atisBuilt = false;
  buildAtisPage();
  if (editMode) {
    // re-apply edit mode
    document.querySelectorAll('.atis-field-wrap').forEach(w=>w.classList.add('edit-active'));
    document.querySelectorAll('.atis-field-label').forEach(l=>l.style.display='none');
    document.querySelectorAll('.label-edit-inp').forEach(i=>i.style.display='');
  }
  onChanged();
}

function askDelField(fieldId) {
  const f = atisFields.find(x=>x.id===fieldId);
  if (!f) return;
  openConfirm('FELD LÖSCHEN','🗑',`Feld <b>"${esc(f.label)}"</b> wirklich löschen?<br><span style="font-size:10px;color:var(--red)">Inhalt wird gelöscht!</span>`,'LÖSCHEN',()=>{
    atisFields = atisFields.filter(x=>x.id!==fieldId);
    delete atisValues[fieldId];
    atisBuilt = false;
    buildAtisPage();
    if (editMode) {
      document.querySelectorAll('.atis-field-wrap').forEach(w=>w.classList.add('edit-active'));
      document.querySelectorAll('.atis-field-label').forEach(l=>l.style.display='none');
      document.querySelectorAll('.label-edit-inp').forEach(i=>i.style.display='');
    }
    onChanged();
  });
}

// ═══════════════════════════════════════
// ATIS PAGE BUILD
// ═══════════════════════════════════════
function buildAtisPage() {
  if (atisBuilt) {
    // Just restore values
    atisFields.filter(d=>d.type!=='canvas').forEach(def=>{
      const af=document.getElementById('af_'+def.id);
      if (af) { const el=af.querySelector('input,textarea'); if(el) el.value=atisValues[def.id]||''; }
    });
    return;
  }
  atisBuilt = true;
  const container = document.getElementById('atis-fields');
  container.innerHTML = '';

  atisFields.forEach(def => {
    const wrap = document.createElement('div');
    wrap.className = 'atis-field-wrap';
    wrap.id = 'afw_' + def.id;

    // Delete button (visible in edit mode)
    if (def.type !== 'canvas') {
      const delBtn = document.createElement('button');
      delBtn.className = 'field-del-btn';
      delBtn.innerHTML = '−';
      delBtn.title = 'Feld löschen';
      delBtn.onclick = (e) => { e.stopPropagation(); askDelField(def.id); };
      wrap.appendChild(delBtn);
    }

    const card = document.createElement('div');
    card.className = 'atis-field';
    card.id = 'af_' + def.id;

    const hdr = document.createElement('div');
    hdr.className = 'atis-field-hdr';

    // Label + editable input
    const lblWrap = document.createElement('div');
    lblWrap.className = 'atis-field-label-wrap';

    const lbl = document.createElement('span');
    lbl.className = 'atis-field-label';
    lbl.textContent = def.label;

    const lblInp = document.createElement('input');
    lblInp.className = 'label-edit-inp';
    lblInp.value = def.label;
    lblInp.style.display = 'none';
    lblInp.addEventListener('input', () => {
      def.label = lblInp.value;
      lbl.textContent = lblInp.value;
      onChanged();
    });

    lblWrap.appendChild(lbl);
    lblWrap.appendChild(lblInp);
    hdr.appendChild(lblWrap);

    // AI status badge (for fields with aiTarget)
    if (def.aiTarget) {
      const badge = document.createElement('span');
      badge.className = 'ai-status';
      badge.id = 'ai_badge_' + def.id;
      badge.style.display = 'none';
      hdr.appendChild(badge);
    }

    const clearBtn = document.createElement('button');
    clearBtn.className = 'atis-clear-btn';
    clearBtn.textContent = '✕';
    clearBtn.title = 'Leeren';
    clearBtn.onclick = () => clearAtisField(def.id);
    hdr.appendChild(clearBtn);
    card.appendChild(hdr);

    if (def.type === 'text') {
      const inp = document.createElement('input');
      inp.type='text'; inp.className='atis-inp'; inp.placeholder=def.ph||'';
      inp.value = atisValues[def.id]||'';
      inp.addEventListener('input',()=>{ atisValues[def.id]=inp.value; onChanged(); });
      card.appendChild(inp);
    } else if (def.type === 'textarea') {
      const ta = document.createElement('textarea');
      ta.className='atis-inp'; ta.placeholder=def.ph||''; ta.rows=3; ta.style.resize='vertical';
      ta.value = atisValues[def.id]||'';
      ta.addEventListener('input',()=>{ atisValues[def.id]=ta.value; onChanged(); });
      card.appendChild(ta);
    } else if (def.type === 'canvas') {
      buildCanvasField(card);
    }

    wrap.appendChild(card);
    container.appendChild(wrap);
  });

  // Apply current edit mode state
  if (editMode) {
    document.querySelectorAll('.atis-field-wrap').forEach(w=>w.classList.add('edit-active'));
    document.querySelectorAll('.atis-field-label').forEach(l=>l.style.display='none');
    document.querySelectorAll('.label-edit-inp').forEach(i=>i.style.display='');
  }
}

// ═══════════════════════════════════════
// CANVAS FIELD (SMALL)
// ═══════════════════════════════════════
function buildCanvasField(wrapper) {
  const container = document.createElement('div');
  container.className = 'canvas-field-container';

  // Expand button
  const expandBtn = document.createElement('button');
  expandBtn.className = 'canvas-expand-btn';
  expandBtn.innerHTML = '&#x26F6; VOLLBILD';
  expandBtn.onclick = () => openCanvasFullscreen();
  container.appendChild(expandBtn);

  const wrap = document.createElement('div');
  wrap.className = 'canvas-wrap';

  const canvas = document.createElement('canvas');
  wrap.appendChild(canvas);
  container.appendChild(wrap);
  wrapper.appendChild(container);

  // Toolbar
  const tb = buildCanvasToolbar(canvas, false);
  wrapper.appendChild(tb);

  atisCanvas = canvas;
  atisCtx = canvas.getContext('2d');

  function resizeCanvas() {
    const pw = wrap.parentElement ? wrap.parentElement.offsetWidth || 360 : 360;
    const snap = canvas.width > 0 ? atisCtx.getImageData(0,0,canvas.width,canvas.height) : null;
    canvas.width  = Math.max(pw - 2, 100);
    canvas.height = Math.max(180, Math.round(pw * 0.38));
    drawIFRTemplate(atisCtx, canvas.width, canvas.height);
    if (snap && snap.width > 0) atisCtx.putImageData(snap,0,0);
    else if (atisImgData) { const img=new Image(); img.onload=()=>atisCtx.drawImage(img,0,0,canvas.width,canvas.height); img.src=atisImgData; }
  }
  requestAnimationFrame(resizeCanvas);
  window.addEventListener('resize', resizeCanvas);

  attachDrawHandlers(canvas, atisCtx, () => {
    atisImgData = canvas.toDataURL();
    // Sync to fullscreen if open
    if (canvasFullscreen && fsCanvas) {
      const img = new Image(); img.onload=()=>{ fsCtx.clearRect(0,0,fsCanvas.width,fsCanvas.height); drawIFRTemplate(fsCtx,fsCanvas.width,fsCanvas.height); fsCtx.drawImage(img,0,0,fsCanvas.width,fsCanvas.height); }; img.src=atisImgData;
    }
    onChanged();
  });
}

// ═══════════════════════════════════════
// IFR TEMPLATE LINES
// ═══════════════════════════════════════
function drawIFRTemplate(ctx, w, h) {
  const labels = [
    'ATIS INFO ___',
    'CLEARANCE ___',
    'SQUAWK ___',
    'INITIAL CLIMB ___',
    'SID / ROUTE ___',
    'DEP FREQ ___ MHz',
    'REMARKS ___',
  ];
  ctx.save();
  const lineH = Math.floor(h / (labels.length + 1));
  const fontSize = Math.max(8, Math.min(11, lineH * 0.38));
  ctx.font = `${fontSize}px 'Share Tech Mono', monospace`;
  ctx.fillStyle = 'rgba(0,180,216,0.18)';
  ctx.strokeStyle = 'rgba(0,180,216,0.12)';
  ctx.lineWidth = 0.8;
  labels.forEach((label, i) => {
    const y = lineH * (i + 1);
    ctx.beginPath(); ctx.moveTo(10, y); ctx.lineTo(w-10, y); ctx.stroke();
    ctx.fillText(label, 12, y - 3);
  });
  ctx.restore();
}

// ═══════════════════════════════════════
// FULLSCREEN CANVAS
// ═══════════════════════════════════════
function openCanvasFullscreen() {
  canvasFullscreen = true;
  const overlay = document.getElementById('canvas-fullscreen');
  overlay.classList.add('open');

  // Build canvas if not yet done
  const fsWrap = document.getElementById('canvas-fs-wrap');
  const fsTb   = document.getElementById('canvas-fs-toolbar');

  if (!fsCanvas) {
    const canvas = document.createElement('canvas');
    fsWrap.appendChild(canvas);
    fsCanvas = canvas;
    fsCtx = canvas.getContext('2d');

    // Build toolbar
    fsTb.innerHTML = '';
    const tb = buildCanvasToolbar(fsCanvas, true);
    // Move toolbar children into fsTb
    while(tb.firstChild) fsTb.appendChild(tb.firstChild);

    attachDrawHandlers(fsCanvas, fsCtx, () => {
      atisImgData = fsCanvas.toDataURL();
      // Sync to small canvas
      if (atisCanvas) {
        const img=new Image(); img.onload=()=>{ atisCtx.clearRect(0,0,atisCanvas.width,atisCanvas.height); drawIFRTemplate(atisCtx,atisCanvas.width,atisCanvas.height); atisCtx.drawImage(img,0,0,atisCanvas.width,atisCanvas.height); }; img.src=atisImgData;
      }
      onChanged();
    });
  }

  // Size fullscreen canvas
  function sizeFsCanvas() {
    const W = fsWrap.offsetWidth || window.innerWidth;
    const H = fsWrap.offsetHeight || (window.innerHeight - 120);
    fsCanvas.width  = W;
    fsCanvas.height = H;
    fsCanvas.style.width  = W + 'px';
    fsCanvas.style.height = H + 'px';
    drawIFRTemplate(fsCtx, W, H);
    if (atisImgData) {
      const img=new Image(); img.onload=()=>fsCtx.drawImage(img,0,0,W,H); img.src=atisImgData;
    }
  }
  requestAnimationFrame(sizeFsCanvas);
}

function closeCanvasFullscreen() {
  canvasFullscreen = false;
  document.getElementById('canvas-fullscreen').classList.remove('open');
  // Sync back to small canvas
  if (fsCanvas && atisCanvas) {
    atisImgData = fsCanvas.toDataURL();
    const img=new Image(); img.onload=()=>{ atisCtx.clearRect(0,0,atisCanvas.width,atisCanvas.height); drawIFRTemplate(atisCtx,atisCanvas.width,atisCanvas.height); atisCtx.drawImage(img,0,0,atisCanvas.width,atisCanvas.height); }; img.src=atisImgData;
  }
}

// ═══════════════════════════════════════
// CANVAS TOOLBAR BUILDER
// ═══════════════════════════════════════
function buildCanvasToolbar(canvas, isFullscreen) {
  const tb = document.createElement('div');
  tb.className = 'canvas-toolbar';

  const COLORS = ['#00b4d8','#2dc653','#f0b429','#e63946','#ffffff','#b8ccd8'];
  COLORS.forEach(c => {
    const sw = document.createElement('div');
    sw.className = 'c-swatch' + (c===drawState.color?' sel':'');
    sw.style.background = c;
    sw.onclick = () => {
      drawState.color = c; drawState.tool = 'pen';
      document.querySelectorAll('.c-swatch').forEach(s=>s.classList.toggle('sel', s.style.backgroundColor===c||s.style.background===c));
      document.querySelectorAll('#tb-pen,#tb-pen-fs').forEach(b=>{ if(b) b.classList.add('active'); });
      document.querySelectorAll('.c-tool-btn.eraser').forEach(b=>b.classList.remove('active'));
    };
    tb.appendChild(sw);
  });

  const sep1=document.createElement('span'); sep1.className='c-sep'; sep1.textContent='|'; tb.appendChild(sep1);
  [1,2,4,8].forEach(s=>{
    const b=document.createElement('button'); b.className='c-sz-btn'+(s===drawState.size?' active':''); b.textContent=s+'px';
    b.onclick=()=>{ drawState.size=s; document.querySelectorAll('.c-sz-btn').forEach(x=>x.classList.remove('active')); document.querySelectorAll('.c-sz-btn').forEach(x=>{ if(x.textContent===s+'px') x.classList.add('active'); }); };
    tb.appendChild(b);
  });
  const sep2=document.createElement('span'); sep2.className='c-sep'; sep2.textContent='|'; tb.appendChild(sep2);

  const penId = isFullscreen ? 'tb-pen-fs' : 'tb-pen';
  const penBtn = document.createElement('button'); penBtn.className='c-tool-btn active'; penBtn.id=penId; penBtn.textContent='✏ STIFT';
  penBtn.onclick=()=>{ drawState.tool='pen'; penBtn.classList.add('active'); eraserBtn.classList.remove('active'); };
  tb.appendChild(penBtn);

  const eraserBtn = document.createElement('button'); eraserBtn.className='c-tool-btn eraser'; eraserBtn.textContent='⌫ RADIERER';
  eraserBtn.onclick=()=>{ drawState.tool='eraser'; eraserBtn.classList.add('active'); penBtn.classList.remove('active'); };
  tb.appendChild(eraserBtn);

  const clearBtn = document.createElement('button'); clearBtn.className='c-tool-btn danger'; clearBtn.textContent='🗑 LÖSCHEN';
  clearBtn.onclick=()=>{
    if (confirm('Handschrift löschen?')) {
      const ctx = isFullscreen ? fsCtx : atisCtx;
      const cvs = isFullscreen ? fsCanvas : atisCanvas;
      if (ctx && cvs) { ctx.clearRect(0,0,cvs.width,cvs.height); drawIFRTemplate(ctx,cvs.width,cvs.height); }
      atisImgData=null;
      // Clear other canvas too
      if (isFullscreen && atisCanvas) { atisCtx.clearRect(0,0,atisCanvas.width,atisCanvas.height); drawIFRTemplate(atisCtx,atisCanvas.width,atisCanvas.height); }
      if (!isFullscreen && fsCanvas)  { fsCtx.clearRect(0,0,fsCanvas.width,fsCanvas.height); drawIFRTemplate(fsCtx,fsCanvas.width,fsCanvas.height); }
      onChanged();
    }
  };
  tb.appendChild(clearBtn);

  // AI button
  const aiBtn = document.createElement('button'); aiBtn.className='c-tool-btn ai-btn'; aiBtn.textContent='🤖 KI ERKENNEN';
  aiBtn.onclick=()=>runAiRecognition(isFullscreen);
  tb.appendChild(aiBtn);

  return tb;
}

// ═══════════════════════════════════════
// DRAW HANDLERS
// ═══════════════════════════════════════
function attachDrawHandlers(canvas, ctx, onEnd) {
  const ds = drawState;
  function pos(e) {
    const r=canvas.getBoundingClientRect();
    const sx=canvas.width/r.width, sy=canvas.height/r.height;
    const src=e.touches?e.touches[0]:e;
    return {x:(src.clientX-r.left)*sx, y:(src.clientY-r.top)*sy};
  }
  function start(e) {
    e.preventDefault(); ds.on=true;
    const {x,y}=pos(e); ds.lx=x; ds.ly=y;
    ctx.beginPath(); ctx.arc(x,y,ds.size/2,0,Math.PI*2);
    if (ds.tool==='eraser') { ctx.globalCompositeOperation='destination-out'; ctx.fillStyle='rgba(0,0,0,1)'; }
    else { ctx.globalCompositeOperation='source-over'; ctx.fillStyle=ds.color; }
    ctx.fill();
  }
  function move(e) {
    if (!ds.on) return; e.preventDefault();
    const {x,y}=pos(e);
    ctx.beginPath(); ctx.moveTo(ds.lx,ds.ly); ctx.lineTo(x,y);
    if (ds.tool==='eraser') { ctx.globalCompositeOperation='destination-out'; ctx.strokeStyle='rgba(0,0,0,1)'; ctx.lineWidth=ds.size*5; }
    else { ctx.globalCompositeOperation='source-over'; ctx.strokeStyle=ds.color; ctx.lineWidth=ds.size; }
    ctx.lineCap='round'; ctx.lineJoin='round'; ctx.stroke();
    ds.lx=x; ds.ly=y;
  }
  function end() {
    if (!ds.on) return; ds.on=false; ctx.globalCompositeOperation='source-over'; onEnd();
  }
  canvas.addEventListener('mousedown',start,{passive:false});
  canvas.addEventListener('mousemove',move,{passive:false});
  canvas.addEventListener('mouseup',end);
  canvas.addEventListener('mouseleave',end);
  canvas.addEventListener('touchstart',start,{passive:false});
  canvas.addEventListener('touchmove',move,{passive:false});
  canvas.addEventListener('touchend',end,{passive:false});
  canvas.addEventListener('touchcancel',end,{passive:false});
}

// ═══════════════════════════════════════
// AI HANDWRITING RECOGNITION
// ═══════════════════════════════════════
async function runAiRecognition(fromFullscreen) {
  const cvs = fromFullscreen ? (fsCanvas || atisCanvas) : atisCanvas;
  if (!cvs) { showToast('⚠ Kein Canvas verfügbar', true); return; }

  // Check if canvas has content
  const imgDataUrl = cvs.toDataURL('image/png');

  // Show loading state
  const fsAiStatus = document.getElementById('canvas-fs-ai-status');
  if (fromFullscreen && fsAiStatus) {
    fsAiStatus.style.display='';
    fsAiStatus.className='ai-status';
    fsAiStatus.innerHTML='<span class="ai-spinner"></span>KI ANALYSIERT …';
  }
  showToast('🤖 KI analysiert Handschrift …');

  // Build list of fields that can receive AI results
  const targetFields = atisFields.filter(f=>f.aiTarget && f.type !== 'canvas').map(f=>({id:f.id,label:f.label,aiTarget:f.aiTarget}));

  // Convert canvas to base64
  const base64 = imgDataUrl.split(',')[1];

  const systemPrompt = `Du bist ein Assistent für Piloten und erkennst Handschrift aus IFR Clearance Notizen.
Das Bild zeigt ein handschriftliches Clearance-Formular mit folgenden möglichen Feldern:
${targetFields.map(f=>`- ${f.label} (ID: ${f.aiTarget})`).join('\n')}

Extrahiere alle erkennbaren Werte und gib AUSSCHLIESSLICH ein JSON-Objekt zurück (kein Markdown, kein Text davor/danach) mit folgendem Format:
{
  "results": [
    {"fieldId": "<ID>", "value": "<erkannter Wert>", "confidence": "high|medium|low|unreadable"}
  ]
}
- Wenn ein Feld nicht erkannt werden kann: confidence = "unreadable", value = ""
- Wenn nichts geschrieben ist: gib leeres results-Array zurück
- Erkenne Squawk-Codes (4-stellig), Frequenzen (xxx.xxx), Flugflächen (FLxxx), etc.
- Für Initial Climb: Wert in ft oder FL
- Gib NUR erkannte Felder zurück, nicht alle.`;

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{
          role: 'user',
          content: [
            { type: 'image', source: { type: 'base64', media_type: 'image/png', data: base64 } },
            { type: 'text', text: 'Erkenne die Handschrift in diesem IFR Clearance Formular und extrahiere die Werte.' }
          ]
        }],
        system: systemPrompt
      })
    });

    const data = await response.json();
    const text = data.content?.map(b=>b.text||'').join('') || '';

    let parsed;
    try {
      const clean = text.replace(/```json|```/g,'').trim();
      parsed = JSON.parse(clean);
    } catch(e) {
      throw new Error('JSON Parse Fehler: ' + text.substring(0,100));
    }

    const results = parsed.results || [];
    if (results.length === 0) {
      if (fromFullscreen && fsAiStatus) { fsAiStatus.className='ai-status warn'; fsAiStatus.innerHTML='⚠ NICHTS ERKANNT'; }
      showToast('⚠ Keine Handschrift erkannt', true);
      return;
    }

    let filled=0, failed=0;
    results.forEach(r => {
      const field = atisFields.find(f=>f.aiTarget===r.fieldId);
      if (!field) return;

      const badge = document.getElementById('ai_badge_' + field.id);
      const af = document.getElementById('af_' + field.id);
      const el = af ? af.querySelector('input,textarea') : null;

      if (r.confidence === 'unreadable' || !r.value) {
        failed++;
        if (badge) { badge.style.display=''; badge.className='ai-status err'; badge.textContent='⚠ UNLESERLICH'; setTimeout(()=>{ badge.style.display='none'; },5000); }
      } else {
        filled++;
        atisValues[field.id] = r.value;
        if (el) el.value = r.value;
        if (badge) {
          badge.style.display='';
          badge.className = r.confidence==='high' ? 'ai-status ok' : 'ai-status warn';
          badge.textContent = r.confidence==='high' ? '✓ KI' : '~ KI';
          setTimeout(()=>{ badge.style.display='none'; },6000);
        }
      }
    });

    onChanged();
    const msg = `✓ KI: ${filled} Feld${filled!==1?'er':''} übertragen${failed>0?' · '+failed+' unleserlich':''}`;
    if (fromFullscreen && fsAiStatus) { fsAiStatus.style.display=''; fsAiStatus.className=failed>0?'ai-status warn':'ai-status ok'; fsAiStatus.textContent=msg; }
    showToast(msg, failed > 0);

  } catch(err) {
    console.error('AI Error:', err);
    if (fromFullscreen && fsAiStatus) { fsAiStatus.className='ai-status err'; fsAiStatus.innerHTML='⚠ FEHLER'; }
    showToast('⚠ KI-Fehler: ' + err.message.substring(0,40), true);
  }
}

// ═══════════════════════════════════════
// ATIS HELPERS
// ═══════════════════════════════════════
function clearAtisField(id) {
  if (id==='draw') {
    if (atisCanvas) { atisCtx.clearRect(0,0,atisCanvas.width,atisCanvas.height); drawIFRTemplate(atisCtx,atisCanvas.width,atisCanvas.height); }
    if (fsCanvas)   { fsCtx.clearRect(0,0,fsCanvas.width,fsCanvas.height); drawIFRTemplate(fsCtx,fsCanvas.width,fsCanvas.height); }
    atisImgData=null;
  } else {
    atisValues[id]='';
    const af=document.getElementById('af_'+id);
    if (af) { const el=af.querySelector('input,textarea'); if(el) el.value=''; }
  }
  onChanged();
}

function clearAllAtis() {
  if (!confirm('Alle ATIS-Felder und Handschrift leeren?')) return;
  atisValues={};
  if (atisCanvas) { atisCtx.clearRect(0,0,atisCanvas.width,atisCanvas.height); drawIFRTemplate(atisCtx,atisCanvas.width,atisCanvas.height); }
  if (fsCanvas)   { fsCtx.clearRect(0,0,fsCanvas.width,fsCanvas.height); drawIFRTemplate(fsCtx,fsCanvas.width,fsCanvas.height); }
  atisImgData=null;
  atisFields.filter(d=>d.type!=='canvas').forEach(def=>{
    const af=document.getElementById('af_'+def.id);
    if (af) { const el=af.querySelector('input,textarea'); if(el) el.value=''; }
  });
  onChanged(); showToast('ATIS GELEERT');
}

function atisManualSave() { onChanged(); saveFile(); }

// ═══════════════════════════════════════
// CHECKLIST RENDER
// ═══════════════════════════════════════
function renderCL() {
  onChanged();
  const lvl = nav.length;
  const ac  = lvl>=1 ? clData.find(a=>a.id===nav[0]) : null;
  const cl  = (ac&&lvl>=2) ? ac.checklists.find(c=>c.id===nav[1]) : null;

  document.getElementById('view-aircraft').style.display   = lvl===0?'':'none';
  document.getElementById('view-checklists').style.display = lvl===1?'':'none';
  document.getElementById('view-items').style.display      = lvl===2?'':'none';

  if (currentTab==='cl') {
    document.getElementById('back-btn').style.display  = lvl>0?'inline-block':'none';
    document.getElementById('reset-btn').style.display = lvl===2?'':'none';
    document.getElementById('add-btn').style.display   = '';
    document.getElementById('header-sub').textContent  = clHeaderSub();
    const bc = document.getElementById('breadcrumb');
    if (lvl>0) {
      bc.style.display='';
      let h=`<span class="bc-link" onclick="setNav([])">CHECKLISTEN</span>`;
      if (lvl>=1) h+=` › <span class="bc-link" onclick="setNav(['${nav[0]}'])">${esc(ac.name.toUpperCase())}</span>`;
      if (lvl===2) h+=` › <span style="color:var(--text2)">${esc(cl.name.toUpperCase())}</span>`;
      bc.innerHTML=h;
    } else bc.style.display='none';
  }

  if (lvl===0) renderAircraft();
  else if (lvl===1) renderChecklists(ac);
  else if (lvl===2) renderItems(ac,cl);
}

function renderAircraft() {
  const c=document.getElementById('view-aircraft');
  c.innerHTML=`<div class="view-label">AVIATION CHECKLIST MANAGER — FLUGZEUG WÄHLEN</div>`;
  if (!clData.length){c.innerHTML+=`<div class="empty-hint">KEIN FLUGZEUG<br>+ DRÜCKEN UM HINZUZUFÜGEN</div>`;return;}
  clData.forEach(ac=>{
    const d=document.createElement('div'); d.className='ac-card'; d.style.setProperty('--clr',ac.color);
    d.innerHTML=`<div class="card-info"><div class="card-name">${esc(ac.name)}</div><div class="card-meta">${esc(ac.desc||'')} · ${ac.checklists.length} CHECKLISTE${ac.checklists.length!==1?'N':''}</div></div>
    <div class="card-actions"><button class="icon-btn" onclick="event.stopPropagation();openEditAc('${ac.id}')">&#9998;</button><button class="icon-btn del" onclick="event.stopPropagation();askDelAc('${ac.id}')">&#10005;</button></div>`;
    d.addEventListener('click',()=>setNav([ac.id])); c.appendChild(d);
  });
}

function renderChecklists(ac) {
  const c=document.getElementById('view-checklists');
  c.innerHTML=`<div class="view-label">${esc(ac.name.toUpperCase())} — CHECKLISTE WÄHLEN</div>`;
  if (!ac.checklists.length){c.innerHTML+=`<div class="empty-hint">KEINE CHECKLISTEN<br>+ DRÜCKEN</div>`;return;}
  ac.checklists.forEach(cl=>{
    const {done,total,pct}=prog(ac.id,cl.id,cl.items);
    const d=document.createElement('div'); d.className='cl-card'; d.style.setProperty('--clr',cl.color);
    d.innerHTML=`<div class="card-info"><div class="card-name">${esc(cl.name)}</div>
    <div class="card-bar-row"><div class="card-bar"><div class="card-fill" style="width:${pct}%;background:${cl.color}"></div></div>
    <span class="card-count">${done}/${total}</span>${done===total&&total>0?'<span class="card-done">✓ COMPLETE</span>':''}</div></div>
    <div class="card-actions"><button class="icon-btn" onclick="event.stopPropagation();openEditCl('${cl.id}')">&#9998;</button><button class="icon-btn del" onclick="event.stopPropagation();askDelCl('${cl.id}')">&#10005;</button></div>`;
    d.addEventListener('click',()=>setNav([nav[0],cl.id])); c.appendChild(d);
  });
}

function renderItems(ac,cl) {
  const {done,total,pct}=prog(ac.id,cl.id,cl.items);
  const c=document.getElementById('view-items');
  c.innerHTML=`<div class="prog-header"><div><div class="prog-label-text">${done} / ${total} ERLEDIGT</div><div class="prog-bar-wide"><div class="prog-fill" style="width:${pct}%;background:${cl.color}"></div></div></div>${done===total&&total>0?'<div style="font-size:9px;color:var(--green);letter-spacing:2px;border:1px solid var(--green);padding:3px 10px;border-radius:4px;">✓ ABGESCHLOSSEN</div>':''}</div>`;
  if (!cl.items.length){c.innerHTML+=`<div class="empty-hint">KEINE SCHRITTE<br>+ DRÜCKEN</div>`;return;}
  cl.items.forEach(item=>{
    const key=`${ac.id}_${cl.id}_${item.id}`, isChk=!!clChecked[key], isPend=pendingUncheck===key;
    const row=document.createElement('div'); row.className='item-row'+(isChk?' ischecked':''); row.id='row_'+key;
    row.innerHTML=`${isPend?`<div class="uncheck-overlay" onclick="doUncheck('${key}')"><div class="uncheck-label">ENTFERNEN</div></div>`:''}
    <button class="chk-btn${isChk?' on':''}" style="--item-clr:${cl.color}" onclick="toggleCheck('${key}')">${isChk&&!isPend?'✓':''}</button>
    <div class="item-text${isChk?' done':''}" id="itxt_${key}">${esc(item.t)}</div>
    <div class="item-actions"><button class="edit-item" onclick="startEditItem('${ac.id}','${cl.id}','${item.id}')">&#9998;</button><button class="del-item" onclick="askDelItem('${item.id}')">&#10005;</button></div>`;
    c.appendChild(row);
  });
}

// ═══════════════════════════════════════
// HELPERS
// ═══════════════════════════════════════
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function prog(aId,cId,items){const d=items.filter(i=>clChecked[`${aId}_${cId}_${i.id}`]).length,t=items.length;return{done:d,total:t,pct:t?d/t*100:0};}
function setNav(n){nav=n;renderCL();}
function showToast(msg,warn){const t=document.getElementById('toast');t.textContent=msg;t.className=warn?'warn show':'show';clearTimeout(t._t);t._t=setTimeout(()=>t.className='',2800);}

function toggleCheck(key){
  if(clChecked[key]){
    if(pendingUncheck===key)return;
    pendingUncheck=key; clearTimeout(pendingTimer);
    pendingTimer=setTimeout(()=>{pendingUncheck=null;renderCL();},2500); renderCL();
  } else { clChecked[key]=true; renderCL(); }
}
function doUncheck(key){delete clChecked[key];pendingUncheck=null;clearTimeout(pendingTimer);renderCL();}
function goBack(){pendingUncheck=null;if(nav.length===2)nav=[nav[0]];else if(nav.length===1)nav=[];renderCL();}
function onAdd(){if(!nav.length)openNewAc();else if(nav.length===1)openNewCl();else openNewItem();}

function askReset(){
  const ac=clData.find(a=>a.id===nav[0]),cl=ac.checklists.find(c=>c.id===nav[1]);
  openConfirm('RESET','🔄',`Alle Haken in <b>${esc(cl.name)}</b> entfernen?`,'ZURÜCKSETZEN',
    ()=>{const p=`${nav[0]}_${nav[1]}_`;Object.keys(clChecked).filter(k=>k.startsWith(p)).forEach(k=>delete clChecked[k]);pendingUncheck=null;renderCL();});
}

function startEditItem(aId,cId,iId){
  const ac=clData.find(a=>a.id===aId),cl=ac.checklists.find(c=>c.id===cId),item=cl.items.find(i=>i.id==iId);
  const el=document.getElementById(`itxt_${aId}_${cId}_${iId}`); if(!el)return;
  const inp=document.createElement('input'); inp.className='inline-input'; inp.value=item.t; el.replaceWith(inp); inp.focus();
  const save=()=>{const v=inp.value.trim();if(v)item.t=v;renderCL();};
  inp.onblur=save; inp.onkeydown=e=>{if(e.key==='Enter')save();if(e.key==='Escape')renderCL();};
}

function askDelAc(id){const ac=clData.find(a=>a.id===id);openConfirm('FLUGZEUG LÖSCHEN','🗑',`<b>${esc(ac.name)}</b> und alle Checklisten löschen?<br><span style="color:var(--red);font-size:10px">Nicht rückgängig!</span>`,'LÖSCHEN',()=>{clData=clData.filter(a=>a.id!==id);Object.keys(clChecked).filter(k=>k.startsWith(id+'_')).forEach(k=>delete clChecked[k]);if(nav[0]===id)nav=[];renderCL();});}
function askDelCl(cId){const ac=clData.find(a=>a.id===nav[0]),cl=ac.checklists.find(c=>c.id===cId);openConfirm('CHECKLISTE LÖSCHEN','🗑',`<b>${esc(cl.name)}</b> löschen?`,'LÖSCHEN',()=>{ac.checklists=ac.checklists.filter(c=>c.id!==cId);Object.keys(clChecked).filter(k=>k.startsWith(`${nav[0]}_${cId}_`)).forEach(k=>delete clChecked[k]);if(nav[1]===cId)nav=[nav[0]];renderCL();});}
function askDelItem(iId){const ac=clData.find(a=>a.id===nav[0]),cl=ac.checklists.find(c=>c.id===nav[1]),item=cl.items.find(i=>i.id==iId);openConfirm('SCHRITT LÖSCHEN','🗑',`<b>"${esc(item.t.substring(0,50))}"</b> löschen?`,'LÖSCHEN',()=>{cl.items=cl.items.filter(i=>i.id!=iId);delete clChecked[`${nav[0]}_${nav[1]}_${iId}`];renderCL();});}

function openNewAc(){editAcId=null;selAcColor=PALETTE[0];document.getElementById('m-ac-title').textContent='NEUES FLUGZEUG';document.getElementById('inp-ac-name').value='';document.getElementById('inp-ac-desc').value='';buildCG('cg-ac',selAcColor,c=>{selAcColor=c;buildCG('cg-ac',selAcColor,null,true);});openModal('m-aircraft');setTimeout(()=>document.getElementById('inp-ac-name').focus(),50);}
function openEditAc(id){const ac=clData.find(a=>a.id===id);editAcId=id;selAcColor=ac.color;document.getElementById('m-ac-title').textContent='FLUGZEUG BEARBEITEN';document.getElementById('inp-ac-name').value=ac.name;document.getElementById('inp-ac-desc').value=ac.desc||'';buildCG('cg-ac',selAcColor,c=>{selAcColor=c;buildCG('cg-ac',selAcColor,null,true);});openModal('m-aircraft');}
function submitAircraft(){const name=document.getElementById('inp-ac-name').value.trim();if(!name)return;const desc=document.getElementById('inp-ac-desc').value.trim();if(editAcId){const ac=clData.find(a=>a.id===editAcId);ac.name=name;ac.desc=desc;ac.color=selAcColor;closeModal('m-aircraft');renderCL();}else{const id='ac_'+Date.now();clData.push({id,name,desc,color:selAcColor,checklists:[]});closeModal('m-aircraft');nav=[id];renderCL();}}

function openNewCl(){editClId=null;selClColor=PALETTE[3];document.getElementById('m-cl-title').textContent='NEUE CHECKLISTE';document.getElementById('inp-cl-name').value='';buildCG('cg-cl',selClColor,c=>{selClColor=c;buildCG('cg-cl',selClColor,null,true);});openModal('m-checklist');setTimeout(()=>document.getElementById('inp-cl-name').focus(),50);}
function openEditCl(cId){const ac=clData.find(a=>a.id===nav[0]),cl=ac.checklists.find(c=>c.id===cId);editClId=cId;selClColor=cl.color;document.getElementById('m-cl-title').textContent='CHECKLISTE BEARBEITEN';document.getElementById('inp-cl-name').value=cl.name;buildCG('cg-cl',selClColor,c=>{selClColor=c;buildCG('cg-cl',selClColor,null,true);});openModal('m-checklist');}
function submitChecklist(){const name=document.getElementById('inp-cl-name').value.trim();if(!name)return;if(editClId){const ac=clData.find(a=>a.id===nav[0]),cl=ac.checklists.find(c=>c.id===editClId);cl.name=name;cl.color=selClColor;closeModal('m-checklist');renderCL();}else{const ac=clData.find(a=>a.id===nav[0]),id='cl_'+Date.now();ac.checklists.push({id,name,color:selClColor,items:[]});closeModal('m-checklist');nav=[nav[0],id];renderCL();}}

function openNewItem(){document.getElementById('inp-item-text').value='';openModal('m-item');setTimeout(()=>document.getElementById('inp-item-text').focus(),50);}
function submitItem(){const text=document.getElementById('inp-item-text').value.trim();if(!text)return;const ac=clData.find(a=>a.id===nav[0]),cl=ac.checklists.find(c=>c.id===nav[1]);cl.items.push({id:Date.now(),t:text});closeModal('m-item');renderCL();}

function openConfirm(title,icon,msg,okLbl,cb){document.getElementById('confirm-title').textContent=title;document.getElementById('confirm-icon').innerHTML=icon;document.getElementById('confirm-msg').innerHTML=msg;document.getElementById('confirm-ok').textContent=okLbl;confirmCb=cb;openModal('m-confirm');}
document.getElementById('confirm-ok').onclick=()=>{closeModal('m-confirm');if(confirmCb){confirmCb();confirmCb=null;}};

function buildCG(id,sel,pick,refresh){
  const g=document.getElementById(id);
  if(refresh){g.querySelectorAll('.cdot').forEach(d=>d.classList.toggle('sel',d.dataset.c===sel));return;}
  g.innerHTML='';
  PALETTE.forEach(c=>{const d=document.createElement('div');d.className='cdot'+(c===sel?' sel':'');d.dataset.c=c;d.style.background=c;d.onclick=()=>pick&&pick(c);g.appendChild(d);});
}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}
document.querySelectorAll('.modal-overlay').forEach(m=>m.addEventListener('click',e=>{if(e.target===m)m.classList.remove('open');}));
document.getElementById('inp-ac-name').addEventListener('keydown',e=>e.key==='Enter'&&submitAircraft());
document.getElementById('inp-ac-desc').addEventListener('keydown',e=>e.key==='Enter'&&submitAircraft());
document.getElementById('inp-cl-name').addEventListener('keydown',e=>e.key==='Enter'&&submitChecklist());
document.getElementById('inp-item-text').addEventListener('keydown',e=>e.key==='Enter'&&submitItem());

// ═══════════════════════════════════════
// INIT
// ═══════════════════════════════════════
if (loadLS()) showToast('✓ LETZTER STAND GELADEN');
setSaveStatus('idle');
document.getElementById('save-banner').style.display = '';
renderCL();
</script>
</body>
</html>
