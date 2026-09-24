<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Sopaan · Time</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Source+Sans+3:wght@400;600;700&family=IBM+Plex+Mono:wght@500;600&display=swap">
<style>
  html,body{margin:0;} img{max-width:100%;} [hidden]{display:none !important;}
  :root{
    --navy:#16264A; --navy-2:#1F3B6B; --gold:#C79A3E; --gold-soft:#F3E7C9;
    --paper:#FBF9F4; --paper-2:#F1EAD8; --card:#FFFFFF;
    --ink:#211E1A; --ink-soft:#655D4C; --rule:#E4DCC8;
    --success:#2E8B57; --success-soft:#E1F2E7;
    --danger:#BF4B45; --danger-soft:#FAE3E1;
    --locked:#C7BEA9;
    --focus:#1F3B6B;
    --accent-text:#1F3B6B; --retry-text:#8A661F;
    color-scheme:light;
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
      --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
      --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
      --success:#7BC79A; --success-soft:#1B2E22;
      --danger:#E38884; --danger-soft:#331D1B;
      --locked:#4A4436;
      --focus:#E0B75B;
      --accent-text:#E0B75B; --retry-text:#E0B75B;
      color-scheme:dark;
    }
  }
  :root[data-theme="dark"]{
    --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
    --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
    --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
    --success:#7BC79A; --success-soft:#1B2E22;
    --danger:#E38884; --danger-soft:#331D1B;
    --locked:#4A4436;
    --focus:#E0B75B;
    --accent-text:#E0B75B; --retry-text:#E0B75B;
    color-scheme:dark;
  }

  *{box-sizing:border-box;}
  body{background:var(--paper); color:var(--ink); font-family:'Source Sans 3',-apple-system,'Segoe UI',sans-serif; padding-inline:0; padding-block:0;}
  h1,h2,h3{font-family:'Fraunces',Georgia,serif; text-wrap:balance; margin:0;}
  .num{font-family:'IBM Plex Mono',ui-monospace,monospace; font-variant-numeric:tabular-nums;}

  header.brand{
    background:linear-gradient(155deg,var(--navy) 0%, var(--navy-2) 100%);
    color:#F4EFDF; padding-block:calc(20px + env(safe-area-inset-top,0px)) 18px; padding-inline:20px;
  }
  .brand-row{display:flex; align-items:center; gap:12px; max-width:900px; margin:0 auto;}
  .crest{
    width:42px; height:42px; border-radius:10px; background:var(--gold); color:var(--navy);
    display:flex; align-items:center; justify-content:center; font-family:'Fraunces',serif; font-weight:700; font-size:18px; flex-shrink:0;
  }
  .brand-name{font-size:12px; letter-spacing:.08em; text-transform:uppercase; color:var(--gold); font-weight:700;}
  .series-name{font-size:19px; font-weight:700; font-family:'Fraunces',serif;}
  .chapter-eyebrow{max-width:900px; margin:14px auto 0; font-size:12px; letter-spacing:.06em; text-transform:uppercase; color:#AEB9D6;}
  .chapter-title{font-size:28px; max-width:900px; margin:2px auto 0;}
  .chapter-sub{font-size:14.5px; color:var(--gold); font-weight:700; max-width:900px; margin:3px auto 0;}

  .chapter-progress{max-width:900px; margin:14px auto 0; display:flex; align-items:center; gap:10px;}
  .cp-track{flex:1; height:6px; border-radius:99px; background:rgba(255,255,255,.18); overflow:hidden;}
  .cp-fill{height:100%; background:var(--gold); border-radius:99px; transition:width .3s ease;}
  .cp-label{font-size:11.5px; color:#CFD7EA; white-space:nowrap;}

  .tabbar{position:sticky; top:env(safe-area-inset-top,0px); z-index:15; background:var(--paper); border-bottom:1px solid var(--rule); overflow-x:auto; white-space:nowrap;}
  .tabbar-inner{max-width:900px; margin:0 auto; display:flex; padding-inline:16px;}
  .tab-btn{font-family:inherit; font-size:14px; font-weight:600; color:var(--ink-soft); background:none; border:none; padding:13px 16px; cursor:pointer; position:relative; flex-shrink:0;}
  .tab-btn.active{color:var(--accent-text);}
  .tab-btn.active::after{content:''; position:absolute; left:12px; right:12px; bottom:0; height:3px; background:var(--gold); border-radius:3px 3px 0 0;}
  .tab-count{font-size:11px; color:var(--ink-soft); margin-left:5px;}

  .slide-progress{max-width:900px; margin:0 auto; padding:10px 16px 0; display:flex; align-items:center; gap:10px;}
  .sp-track{flex:1; height:5px; border-radius:99px; background:var(--rule); overflow:hidden;}
  .sp-fill{height:100%; background:var(--accent-text); border-radius:99px; transition:width .3s ease;}
  .sp-label{font-size:12px; color:var(--ink-soft); white-space:nowrap; font-weight:600;}

  .wrap{max-width:900px; margin:0 auto; padding:16px 16px calc(110px + env(safe-area-inset-bottom,0px));}

  .qcard{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px;}
  .qhead{display:flex; align-items:flex-start; gap:10px; margin-bottom:10px;}
  .qnum{width:32px; height:32px; border-radius:8px; background:var(--gold-soft); color:var(--accent-text); display:flex; align-items:center; justify-content:center; font-weight:700; font-family:'Fraunces',serif; flex-shrink:0; font-size:14px;}
  .qtext{font-size:16px; line-height:1.55; flex:1;}
  .qtag{font-size:10.5px; color:var(--gold); background:var(--gold-soft); padding:2px 7px; border-radius:99px; font-weight:700; margin-left:6px; white-space:nowrap;}
  .marks-pill{font-size:11px; font-weight:700; color:var(--ink-soft); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; margin-left:auto; flex-shrink:0; white-space:nowrap;}
  .step-badge{font-size:11px; font-weight:700; color:var(--accent-text); background:var(--paper-2); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; display:inline-block; margin-bottom:12px;}

  .options{display:flex; flex-direction:column; gap:8px; margin-top:10px;}
  .opt{display:flex; align-items:center; gap:10px; padding:11px 12px; border:1.5px solid var(--rule); border-radius:10px; cursor:pointer; font-size:15px; background:var(--paper);}
  .opt input{accent-color:var(--navy-2);}
  .opt.is-correct{border-color:var(--success); background:var(--success-soft);}
  .opt.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .opt.locked{cursor:not-allowed;}

  .subpart-label{font-weight:700; font-size:12.5px; color:var(--accent-text); text-transform:uppercase; letter-spacing:.03em; margin:14px 0 6px;}
  .or-divider{text-align:center; font-size:11px; font-weight:700; letter-spacing:.08em; color:var(--ink-soft); margin:8px 0;}

  .steps{display:flex; flex-direction:column; gap:10px;}
  .step-line{font-size:14.5px; line-height:1.9; background:var(--paper); border:1px dashed var(--rule); border-radius:10px; padding:9px 12px;}
  .step-line.resolved{opacity:.9;}
  .blank-input{font-family:'IBM Plex Mono',monospace; font-size:14px; border:1.5px solid var(--rule); border-radius:6px; padding:3px 8px; width:120px; background:var(--card); color:var(--ink); margin:0 2px;}
  .blank-input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .blank-input.is-correct{border-color:var(--success); background:var(--success-soft);}
  .blank-input.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .blank-input[disabled]{opacity:.85;}
  .reveal-note{font-size:12px; color:var(--danger); padding-left:2px; margin-top:-2px;}

  .feedback{font-size:13.5px; padding:10px 12px; border-radius:9px; margin-top:14px; display:none;}
  .feedback.show{display:block;}
  .feedback.ok{background:var(--success-soft); color:var(--success);}
  .feedback.retry{background:var(--gold-soft); color:var(--retry-text);}
  .feedback.reveal{background:var(--danger-soft); color:var(--danger);}
  .feedback.err{background:var(--danger-soft); color:var(--danger);}
  .attempts-dots{display:inline-flex; gap:4px; margin-left:2px;}
  .attempts-dots span{width:6px; height:6px; border-radius:50%; background:var(--ink-soft); opacity:.3; display:inline-block;}
  .attempts-dots span.used{opacity:1; background:var(--danger);}

  .ar-box{background:var(--paper-2); border-radius:10px; padding:10px 12px; margin-bottom:12px; font-size:13px; color:var(--ink-soft);}

  .navbar{
    position:fixed; left:0; right:0; bottom:0; z-index:30; background:var(--paper);
    border-top:1px solid var(--rule); padding:10px 16px calc(10px + env(safe-area-inset-bottom,0px));
  }
  .navbar-inner{max-width:900px; margin:0 auto; display:flex; gap:8px; flex-wrap:wrap; align-items:center;}
  .btn{font-family:inherit; font-size:13.5px; font-weight:700; padding:10px 14px; border-radius:9px; border:1.5px solid var(--rule); background:var(--card); color:var(--ink); cursor:pointer;}
  .btn:hover{border-color:var(--navy-2);}
  .btn:disabled{opacity:.4; cursor:not-allowed;}
  .btn-primary{background:var(--navy-2); color:#fff; border-color:var(--navy-2);}
  .navbar .spacer{flex:1;}

  .fab{position:fixed; right:16px; bottom:calc(74px + env(safe-area-inset-bottom,0px)); background:var(--gold); color:var(--navy); border:none; border-radius:999px; padding:11px 16px; font-family:inherit; font-weight:700; font-size:13px; display:flex; align-items:center; gap:7px; cursor:pointer; box-shadow:0 6px 16px rgba(0,0,0,.18); z-index:35;}
  .fab-badge{background:rgba(255,255,255,.55); border-radius:99px; padding:1px 7px; font-size:11px;}

  .overlay{position:fixed; inset:0; background:rgba(20,18,14,.45); z-index:50; display:none; align-items:flex-end; justify-content:center;}
  .overlay.show{display:flex;}
  .palette{background:var(--card); width:min(480px,100%); max-height:78vh; overflow-y:auto; border-radius:18px 18px 0 0; padding:18px 18px calc(18px + env(safe-area-inset-bottom,0px)); border:1px solid var(--rule); border-bottom:none;}
  @media (min-width:640px){ .overlay{align-items:center;} .palette{border-radius:18px; border-bottom:1px solid var(--rule); max-height:74vh;} }
  .palette-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:6px;}
  .palette-head h2{font-size:16px;}
  .palette-close{background:none; border:none; font-size:20px; color:var(--ink-soft); cursor:pointer; padding:4px;}
  .palette-legend{display:flex; gap:12px; flex-wrap:wrap; font-size:11px; color:var(--ink-soft); margin:10px 0 14px;}
  .palette-legend span{display:inline-flex; align-items:center; gap:5px;}
  .dot{width:9px; height:9px; border-radius:50%; display:inline-block;}
  .dot.correct{background:var(--success);} .dot.revealed{background:var(--danger);}
  .dot.skipped{background:var(--gold);} .dot.locked{background:var(--locked);}
  .dot.current{background:var(--navy-2);}
  .chip-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(48px,1fr)); gap:8px;}
  .chip{border:1.5px solid var(--rule); border-radius:9px; padding:8px 4px; text-align:center; font-family:'IBM Plex Mono',monospace; font-size:12.5px; font-weight:600; cursor:pointer; background:var(--paper); color:var(--ink);}
  .chip[data-status="correct"]{border-color:var(--success); background:var(--success-soft); color:var(--success);}
  .chip[data-status="revealed"]{border-color:var(--danger); background:var(--danger-soft); color:var(--danger);}
  .chip[data-status="skipped"]{border-color:var(--gold); background:var(--gold-soft); color:var(--retry-text);}
  .chip[data-status="locked"]{border-color:var(--rule); color:var(--locked); cursor:not-allowed; background:var(--paper-2);}
  .chip[data-status="current"]{outline:2px solid var(--navy-2); outline-offset:1px;}

  .toast{position:fixed; left:50%; bottom:calc(140px + env(safe-area-inset-bottom,0px)); transform:translateX(-50%); background:var(--ink); color:var(--paper); padding:9px 16px; border-radius:99px; font-size:13px; opacity:0; pointer-events:none; transition:opacity .25s ease; z-index:60;}
  .toast.show{opacity:1;}

  .done-card{text-align:center; padding:36px 20px;}
  .done-card .big{font-size:38px; margin-bottom:6px;}
  .score-pills{display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin:16px 0;}
  .score-pill{padding:8px 16px; border-radius:99px; font-size:13px; font-weight:700;}

  footer.brandfoot{max-width:900px; margin:14px auto 0; padding:0 16px calc(110px + env(safe-area-inset-bottom,0px)); text-align:center; font-size:12px; color:var(--ink-soft);}

  .mode-pill{font-family:inherit; font-size:12.5px; font-weight:700; color:var(--navy); background:var(--gold); border:none; border-radius:99px; padding:6px 14px; cursor:pointer; margin-top:12px; display:inline-flex; align-items:center; gap:6px;}
  .mode-pick{display:flex; flex-direction:column; gap:14px; padding:8px 0 24px;}
  .mode-card{background:var(--card); border:1.5px solid var(--rule); border-radius:16px; padding:22px; cursor:pointer; text-align:left;}
  .mode-card:hover{border-color:var(--navy-2);}
  .mode-card .mode-icon{font-size:26px; margin-bottom:8px;}
  .mode-card h3{font-size:18px; margin-bottom:6px;}
  .mode-card p{font-size:13.5px; color:var(--ink-soft); line-height:1.5; margin:0;}
  .quiz-hint{font-size:12.5px; color:var(--ink-soft); background:var(--paper-2); border-radius:9px; padding:8px 12px; margin-bottom:14px;}
  .review-row{border:1px solid var(--rule); border-radius:10px; padding:11px 13px; margin-bottom:10px;}
  .review-tag{font-size:11.5px; font-weight:700; margin-bottom:4px; display:block;}
  .review-tag.ok{color:var(--success);} .review-tag.bad{color:var(--danger);} .review-tag.na{color:var(--ink-soft);}
  .review-q{font-size:13.5px; margin-bottom:6px; color:var(--ink-soft);}
  .review-ans{font-size:13px; margin-bottom:2px;}

  .who-row{max-width:900px; margin:12px auto 0; display:flex; flex-wrap:wrap; gap:8px; align-items:center;}
  .who-row .mode-pill{margin-top:0;}
  .who{display:inline-flex; flex-wrap:wrap; align-items:center; gap:6px; font-size:12.5px; color:#CFD7EA;}
  .who b{color:#F4EFDF;}
  .who button{font-family:inherit; font-size:12px; font-weight:700; color:#F4EFDF; background:rgba(255,255,255,.12); border:1px solid rgba(255,255,255,.22); border-radius:99px; padding:5px 11px; cursor:pointer;}
  .who button:hover{background:rgba(255,255,255,.2);}
  .login-card{max-width:460px; margin:8px auto 0; background:var(--card); border:1px solid var(--rule); border-radius:16px; padding:22px;}
  .login-card h2{font-size:21px; margin-bottom:4px;}
  .login-card p.lead{font-size:13.5px; color:var(--ink-soft); margin:0 0 16px; line-height:1.5;}
  .fld{display:flex; flex-direction:column; gap:5px; margin-bottom:12px;}
  .fld label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .fld input{font-family:inherit; font-size:15px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:9px; background:var(--paper); color:var(--ink);}
  .fld input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .fld-row{display:grid; grid-template-columns:1fr 1fr; gap:10px;}
  .login-err{font-size:13px; color:var(--danger); background:var(--danger-soft); border-radius:8px; padding:8px 10px; margin-bottom:12px;}
  .login-note{font-size:12px; color:var(--ink-soft); margin-top:12px; line-height:1.5;}
  .known{margin:0 0 16px; display:flex; flex-direction:column; gap:6px;}
  .known-label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .known-btn{display:flex; justify-content:space-between; align-items:center; gap:10px; text-align:left; font-family:inherit; font-size:14.5px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:10px; background:var(--paper); color:var(--ink); cursor:pointer;}
  .known-btn:hover{border-color:var(--navy-2);}
  .known-btn small{font-size:12px; color:var(--ink-soft);}
  .rec-card{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px; margin-bottom:14px;}
  .rec-card h2{font-size:19px; margin-bottom:10px;}
  .rec-card h3{font-size:15px; margin:4px 0 8px;}
  .rec-table-wrap{overflow-x:auto;}
  .rec-table{width:100%; border-collapse:collapse; font-size:13.5px; font-variant-numeric:tabular-nums;}
  .rec-table th{text-align:left; font-size:11.5px; text-transform:uppercase; letter-spacing:.04em; color:var(--ink-soft); padding:6px 8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-table td{padding:8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-bar{display:inline-block; width:70px; height:6px; border-radius:99px; background:var(--rule); overflow:hidden; vertical-align:middle; margin-right:6px;}
  .rec-bar i{display:block; height:100%; background:var(--success);}
  .rec-empty{font-size:13.5px; color:var(--ink-soft);}
  .sec-sub{max-width:900px; margin:0 auto; padding:10px 16px 0; font-size:12.5px; font-weight:700; color:var(--accent-text); letter-spacing:.02em;}
  .opt{flex-wrap:wrap;}
  .opt-l{font-family:'IBM Plex Mono',monospace; font-size:13px; font-weight:600; color:var(--ink-soft);}
  .opt-t{flex:1; min-width:0;}
  .opt.is-chosen:not(.is-correct):not(.is-wrong){border-color:var(--navy-2); background:var(--gold-soft);}
  .opt-tag{font-size:11px; font-weight:700; padding:2px 8px; border-radius:99px; background:var(--card); border:1px solid currentColor; white-space:nowrap;}
  .opt.is-correct .opt-tag{color:var(--success);} .opt.is-wrong .opt-tag{color:var(--danger);} .opt.is-chosen:not(.is-correct):not(.is-wrong) .opt-tag{color:var(--accent-text);}
  .chosen{font-size:13.5px; margin-top:10px; padding:8px 12px; border-radius:9px;}
  .chosen.ok{background:var(--success-soft); color:var(--success);} .chosen.bad{background:var(--danger-soft); color:var(--danger);}
  .chosen + .chosen{margin-top:6px;}
  .solution{margin-top:14px; border:1px solid var(--rule); border-left:4px solid var(--gold); background:var(--paper-2); border-radius:10px; padding:12px 14px;}
  .sol-h{font-family:'Fraunces',Georgia,serif; font-weight:700; font-size:14px; color:var(--accent-text); margin-bottom:6px;}
  .sol-line{font-size:14.5px; line-height:1.7;}
  .rev-sol summary{cursor:pointer; font-size:12.5px; font-weight:700; color:var(--accent-text); margin-top:6px;}
  .rev-sol .solution{margin-top:8px;}
  .chapter-credit{max-width:900px; margin:4px auto 0; font-size:12px; color:#CFD7EA;}
  footer.brandfoot a{color:inherit;}
  .blank-input.wide{width:260px; max-width:100%; font-family:'Source Sans 3',sans-serif;}
  .blank-input.expr{width:170px; max-width:100%;}
  /*fix-layout*/ .cp-fill,.sp-fill{width:0;} .fld{min-width:0;} .fld input{width:100%; min-width:0; box-sizing:border-box;}
  .fig{margin:6px 0 10px; display:flex; justify-content:center;}
  .figsvg{width:100%; max-width:340px; height:auto; overflow:visible;}
  .figsvg .ln,.figsvg .arm{stroke:var(--ink); stroke-width:1.6; fill:none;}
  .figsvg .arm{stroke:var(--accent-text); stroke-width:2;}
  .figsvg .pt{fill:var(--ink);}
  .figsvg .lb{fill:var(--ink); font:600 13px 'Source Sans 3',sans-serif;}
  .figsvg .al{fill:var(--accent-text); font:700 12px 'Source Sans 3',sans-serif;}
  .figsvg .wg{fill:var(--gold-soft); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .wg2{fill:rgba(199,154,62,.35); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .ra{fill:none; stroke:var(--ink); stroke-width:1.2;}
  .figsvg .ahd{fill:var(--ink);}
  .figsvg .pr{fill:var(--paper-2); stroke:var(--ink-soft); stroke-width:1.2;}
  .figsvg .tk{stroke:var(--ink-soft); stroke-width:.8;}
  .figsvg .po{fill:var(--ink); font:600 8.5px 'IBM Plex Mono',monospace;}
  .figsvg .pi{fill:var(--danger); font:600 7.5px 'IBM Plex Mono',monospace;}
  .figsvg .sh{fill:var(--gold-soft); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh2{fill:rgba(199,154,62,.38); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh3{fill:rgba(199,154,62,.22); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .none{fill:none;}
  .figsvg .hid{stroke-dasharray:5 4; fill:none;}
  .figsvg .tick{stroke:var(--ink); stroke-width:1.4; fill:none;}
  .figsvg .shd{fill:var(--accent-text); fill-opacity:.55;}
  .figsvg .cell{fill:var(--card); stroke:var(--ink); stroke-width:1.1;}
  .figsvg .dr{fill:var(--danger);} .figsvg .dw{fill:var(--card); stroke:var(--ink); stroke-width:1.2;}
  .figsvg .dotfill{fill:var(--danger);}
  .tt{border-collapse:collapse; font-size:13.5px; margin:4px auto; font-variant-numeric:tabular-nums;} .tt th,.tt td{border:1px solid var(--rule); padding:4px 9px; text-align:left;} .tt th{background:var(--paper-2); font-weight:700;} .ttw{overflow-x:auto; max-width:100%;}
  .fq{display:inline-flex; flex-direction:column; vertical-align:middle; text-align:center; font-size:.82em; line-height:1.12; margin:0 2px;}
  .fq>span:first-child{border-bottom:1.5px solid currentColor; padding:0 2px;}
  .fq>span:last-child{padding:0 2px;}
  .mx{white-space:nowrap;}
  .blank-input.fr{width:110px;}
  @media (prefers-reduced-motion:reduce){ *{transition:none !important;} }
</style>
</head>
<body>
<header class="brand">
  <div class="brand-row">
    <div class="crest">BM</div>
    <div>
      <div class="brand-name">Brain &amp; Mind Academy</div>
      <div class="series-name">Sopaan <span style="font-weight:400;font-size:14px;color:#CFD7EA;">Practice Series</span></div>
    </div>
  </div>
  <div class="chapter-eyebrow">Grade 6 Mathematics · Chapter 11</div>
  <div class="chapter-title">Time</div>
  <div class="chapter-sub">Exercises 11A–11F · Review Sets · Step-by-Step Practice</div><div class="chapter-credit">Follows Haese Mathematics 6 (MYP 1), Chapter 11</div>
  <div class="chapter-progress">
    <div class="cp-track"><div class="cp-fill" id="cpFill"></div></div>
    <div class="cp-label" id="cpLabel">0% complete</div>
  </div>
  <div class="who-row"><button class="mode-pill" id="modePill" hidden>Choose a mode</button><span class="who" id="whoBar" hidden></span></div>
</header>

<nav class="tabbar"><div class="tabbar-inner" id="tabbar"></div></nav>
<div class="sec-sub" id="secSub"></div><div class="slide-progress"><div class="sp-track"><div class="sp-fill" id="spFill"></div></div><div class="sp-label" id="spLabel">Question 1 of 49</div></div>
<div class="wrap" id="wrap"></div>
<footer class="brandfoot">Brain &amp; Mind Academy · Sopaan Practice Series · Grade 6 Mathematics<br>Exercises follow the structure of <i>Mathematics 6 (MYP 1), 3rd edition</i>, Haese Mathematics. Questions, steps and solutions written by Brain &amp; Mind Academy.</footer>

<div class="navbar"><div class="navbar-inner" id="navbarInner"></div></div>
<button class="fab" id="paletteFab"><span>Questions</span><span class="fab-badge" id="fabBadge">0/49</span></button>

<div class="overlay" id="overlay">
  <div class="palette" role="dialog" aria-label="Question palette">
    <div class="palette-head"><h2 id="paletteTitle">Question palette</h2><button class="palette-close" id="paletteClose">&times;</button></div>
    <div class="palette-legend">
      <span><i class="dot current"></i>Current</span><span><i class="dot correct"></i>Correct</span>
      <span><i class="dot revealed"></i>Revealed</span><span><i class="dot skipped"></i>Skipped</span>
      <span><i class="dot locked"></i>Locked</span>
    </div>
    <div class="chip-grid" id="paletteBody"></div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
(function(){
"use strict";

/* ================= audio ================= */
var audioCtx=null;
function ensureAudio(){ if(!audioCtx){ try{ audioCtx=new (window.AudioContext||window.webkitAudioContext)(); }catch(e){} } return audioCtx; }
function playTone(freqs,dur,type){
  var ctx=ensureAudio(); if(!ctx) return;
  try{
    var t0=ctx.currentTime;
    freqs.forEach(function(f,i){
      var o=ctx.createOscillator(), g=ctx.createGain();
      o.type=type||'sine'; o.frequency.value=f;
      var start=t0+i*dur;
      g.gain.setValueAtTime(0.0001,start);
      g.gain.exponentialRampToValueAtTime(0.16,start+0.02);
      g.gain.exponentialRampToValueAtTime(0.0001,start+dur);
      o.connect(g); g.connect(ctx.destination);
      o.start(start); o.stop(start+dur+0.02);
    });
  }catch(e){}
}
function playSuccess(){ playTone([523.25,659.25,783.99],0.11,'sine'); }
function playWrong(){ playTone([220,185],0.14,'square'); }
function playReveal(){ playTone([300,220],0.16,'triangle'); }

/* ================= helpers ================= */
function norm(s){
  return String(s===undefined||s===null?'':s).trim().toLowerCase().replace(/\s+/g,'')
    .replace(/[×∗*·]/g,'x').replace(/÷/g,'/').replace(/–|—|−/g,'-')
    .replace(/[²]/g,'^2').replace(/[³]/g,'^3').replace(/[⁴]/g,'^4').replace(/[⁵]/g,'^5')
    .replace(/[⁶]/g,'^6').replace(/[⁷]/g,'^7').replace(/[⁸]/g,'^8').replace(/[⁹]/g,'^9')
    .replace(/\^/g,'');
}
function parseNum(s){
  if(s===undefined||s===null) return null;
  var t=String(s).trim().replace(/,/g,'').replace(/[−–—]/g,'-').replace(/\s+/g,''); if(t==='') return null;
  var neg=false; if(t[0]==='-'){neg=true;t=t.slice(1);}
  var m=t.match(/^(\d+)\/(\d+)$/);
  if(m){ var v=parseInt(m[1],10)/parseInt(m[2],10); return neg?-v:v; }
  if(/^\d+(\.\d+)?$/.test(t)){ var v2=parseFloat(t); return neg?-v2:v2; }
  return null;
}
/* ---- expression checker: compares answers like (P-2w)/2 and P/2-w at random values ---- */
function exprPrep(s){
  return String(s).replace(/\s+/g,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^2').replace(/³/g,'^3').replace(/π/g,'#').replace(/pi/gi,'#').replace(/½/g,'(1/2)');
}
function exprCompile(src){
  var s=exprPrep(src), i=0, toks=[];
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length && /[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(/[a-zA-Z#]/.test(ch)){ toks.push({k:'v',v:ch}); i++; continue; }
    if('+-*/^()'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  var out=[];
  for(var t=0;t<toks.length;t++){
    var a=toks[t], b=out[out.length-1];
    if(b && (b.k==='n'||b.k==='v'||b.k===')') && (a.k==='n'||a.k==='v'||a.k==='(')) out.push({k:'&'});
    out.push(a);
  }
  var p=0;
  function peek(){ return out[p]; }
  function parseE(){ var n=parseT(); while(peek() && (peek().k==='+'||peek().k==='-')){ var o=out[p++].k, r=parseT(); n=(function(l,r,o){return function(e){ return o==='+'?l(e)+r(e):l(e)-r(e); };})(n,r,o); } return n; }
  function parseI(){ var n=parseU(); while(peek() && peek().k==='&'){ p++; var r=parseP(); n=(function(l,r){return function(e){ return l(e)*r(e); };})(n,r); } return n; }
  function parseT(){ var n=parseI(); while(peek() && (peek().k==='*'||peek().k==='/')){ var o=out[p++].k, r=parseI(); n=(function(l,r,o){return function(e){ return o==='*'?l(e)*r(e):l(e)/r(e); };})(n,r,o); } return n; }
  function parseU(){ if(peek() && peek().k==='-'){ p++; var u=parseU(); return function(e){ return -u(e); }; } if(peek() && peek().k==='+'){ p++; return parseU(); } return parseP(); }
  function parseP(){ var b=parseA(); if(peek() && peek().k==='^'){ p++; var x=parseU(); return function(e){ return Math.pow(b(e),x(e)); }; } return b; }
  function parseA(){
    var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){ return t.v; };
    if(t.k==='v') return t.v==='#' ? function(){ return Math.PI; } : function(e){ return e[t.v]; };
    if(t.k==='('){ var n=parseE(); if(!peek()||peek().k!==')') throw 0; p++; return n; }
    throw 0;
  }
  try{ var f=parseE(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function exprEqual(input,answer){
  var f=exprCompile(input), g=exprCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<8;trial++){
    var env={}; 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=1.3+Math.random()*4.1; });
    var x=f(env), y=g(env);
    if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-7*Math.max(1,Math.abs(x),Math.abs(y))) return false;
    hits++;
  }
  return hits>=3;
}
function wordsNorm(s){ return String(s||'').toLowerCase().replace(/\band\b/g,' ').replace(/[^a-z]/g,''); }
function listNorm(s){ return (String(s||'').replace(/(\d) (?=\d{3}\b)/g,'$1').match(/-?\d+(\.\d+)?/g)||[]).join(','); }
function powNorm(s){ return String(s||'').toLowerCase().replace(/\s+/g,'').replace(/[×∗*·.]/g,'x').replace(/[⁰¹²³⁴⁵⁶⁷⁸⁹]+/g,function(m){ return '^'+m.split('').map(function(c){ return '⁰¹²³⁴⁵⁶⁷⁸⁹'.indexOf(c); }).join(''); }).replace(/\^1(?!\d)/g,''); }
function fr(s){ return String(s).replace(/\{(\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>').replace(/\{(\d+)\/(\d+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); }
function gcdI(a,b){ a=Math.abs(a); b=Math.abs(b); while(b){ var t=a%b; a=b; b=t; } return a; }
function fracParse(s){ s=String(s===undefined||s===null?'':s).trim().replace(/[\u2044\u2215\u00f7]/g,'/').replace(/\s+/g,' ').replace(/\s*\/\s*/g,'/'); var m;
  if((m=s.match(/^(-?\d+)$/))) return {v:+m[1],form:'int',n:+m[1],d:1};
  if((m=s.match(/^(-?\d+)\/(\d+)$/))){ if(+m[2]===0) return null; return {v:m[1]/m[2],form:'frac',n:+m[1],d:+m[2]}; }
  if((m=s.match(/^(\d+)(?: |\+|-)(\d+)\/(\d+)$/))){ if(+m[3]===0) return null; return {v:+m[1]+m[2]/m[3],form:'mixed',w:+m[1],n:+m[2],d:+m[3]}; }
  if((m=s.match(/^-?\d*\.\d+$/))) return {v:parseFloat(s),form:'dec'};
  return null; }
function fracOK(mode,input,answer){
  if(mode==='flist'){ var A=String(input).split(/[,;]/).map(function(x){return x.trim();}).filter(Boolean), K=String(answer).split(/[,;]/).map(function(x){return x.trim();});
    if(A.length!==K.length) return false; return A.every(function(x,i){ var a=fracParse(x), k=fracParse(K[i]); return a&&k&&Math.abs(a.v-k.v)<1e-9; }); }
  var a=fracParse(input), k=fracParse(answer); if(!a||!k) return false;
  var same=Math.abs(a.v-k.v)<1e-9; if(!same) return false;
  if(mode==='fv') return true;
  if(mode==='dec') return a.form==='dec'||a.form==='int';
  if(mode==='fe') return (a.form==='frac'&&k.form==='frac'&&a.n===k.n&&a.d===k.d)||(a.form==='int'&&k.form==='int');
  if(mode==='fi') return a.form==='frac'||(a.form==='int'&&k.form==='int');
  if(mode==='fl') return a.form==='int'||(a.form==='frac'&&gcdI(a.n,a.d)===1)||(a.form==='mixed'&&a.n<a.d&&gcdI(a.n,a.d)===1);
  if(mode==='fm') return a.form==='int'||(a.form==='mixed'&&a.n>0&&a.n<a.d&&gcdI(a.n,a.d)===1);
  return false; }
function answerMatches(input,answer,accept,expr){
  if(expr==='dec'||expr==='fv'||expr==='fe'||expr==='fl'||expr==='fm'||expr==='fi'||expr==='flist'){ if(input===undefined||input===null||String(input).trim()==='') return false; return fracOK(expr,input,answer); }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  if(expr==='words'){ return [answer].concat(accept||[]).some(function(a){ return wordsNorm(a)===wordsNorm(input); }); }
  if(expr==='list'){ return [answer].concat(accept||[]).some(function(a){ return listNorm(a)===listNorm(input); }); }
  if(expr==='pow'){ return [answer].concat(accept||[]).some(function(a){ return powNorm(a)===powNorm(input); }); }
  if(expr==='time'){ var tn=function(x){ var t=String(x).toLowerCase().replace(/[\s.]/g,'').replace(/[:h]/g,''); if(/^\d{3}(am|pm)?$/.test(t)) t='0'+t; return t; }; return [answer].concat(accept||[]).some(function(a){ return tn(a)===tn(input); }); }
  if(expr==='dlist'){ var dn=function(x){ return (String(x).match(/-?\d*\.?\d+/g)||[]).map(Number).join(','); }; return [answer].concat(accept||[]).some(function(a){ return dn(a)===dn(input); }); }
  if(expr==='set'){ var sn=function(x){ return (String(x).match(/-?\d+/g)||[]).map(Number).sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return sn(a)===sn(input); }); }
  if(expr==='primes'){ var pn=function(x){ var t=powNorm(x).replace(/[^0-9x^]/g,''); var out=[]; t.split('x').forEach(function(tok){ if(!tok) return; var m=tok.split('^'); var b=+m[0], e=m[1]?+m[1]:1; for(var i=0;i<e;i++) out.push(b); }); return out.sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return pn(a)===pn(input); }); }
  if(expr==='angle'){ var an=function(x){ return String(x).toUpperCase().replace(/[^A-Z]/g,''); }; var k=an(answer), v=an(input); return v===k || v===k.split('').reverse().join(''); }
  if(expr==='expanded'){ var f=function(x){ return String(x).replace(/\s+/g,'').replace(/,/g,''); }; return [answer].concat(accept||[]).some(function(a){ return f(a)===f(input); }); }
  if(expr===true && input!==undefined && input!==null && String(input).trim()!==''){
    if(exprEqual(input,answer)) return true;
    return (accept||[]).some(function(a){ return exprEqual(input,a); });
  }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  var n1=parseNum(input), n2=parseNum(answer);
  if(n1!==null && n2!==null) return Math.abs(n1-n2)<1e-3;
  var cands=[answer].concat(accept||[]); var ni=norm(input);
  for(var i=0;i<cands.length;i++){ if(norm(cands[i])===ni) return true; }
  return false;
}
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;'); }

/* ================= DATA ================= */
var AR_OPTIONS = ["Both A and R are true, and R is the correct explanation of A","Both A and R are true, but R is NOT the correct explanation of A","A is true but R is false","A is false but R is true"];
var SECTIONS = [{"id": "s1", "label": "Ex 11A", "sub": "Time lines", "slides": [{"kind": "blank", "p": "This time line shows some Indian space missions.", "tag": "", "marks": "", "flat": [{"t": "a) In which year was Chandrayaan-1 launched? __B1__", "a": {"B1": "2008"}}, {"t": "b) Which mission came immediately after Mangalyaan? __B1__", "a": {"B1": "Chandrayaan-2"}, "expr": "words"}, {"t": "c) How many years were there between Aryabhata and Chandrayaan-3? __B1__", "a": {"B1": "48"}}, {"t": "d) How many years were there between Chandrayaan-1 and Chandrayaan-3? __B1__", "a": {"B1": "15"}}], "sol": "Read each event's year from the time line, then subtract.\na) 2008\nb) Chandrayaan-2 (2019)\nc) 2023 − 1975 = 48\nd) 2023 − 2008 = 15", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 150\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><line class=\"ln\" x1=\"10.0\" y1=\"112.0\" x2=\"290.0\" y2=\"112.0\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"20.0\" y1=\"105\" x2=\"20.0\" y2=\"119\"/><text class=\"po\" x=\"20.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">1970</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"41.7\" y1=\"108\" x2=\"41.7\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"63.3\" y1=\"105\" x2=\"63.3\" y2=\"119\"/><text class=\"po\" x=\"63.3\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">1980</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"85.0\" y1=\"108\" x2=\"85.0\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"106.7\" y1=\"105\" x2=\"106.7\" y2=\"119\"/><text class=\"po\" x=\"106.7\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">1990</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"128.3\" y1=\"108\" x2=\"128.3\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"150.0\" y1=\"105\" x2=\"150.0\" y2=\"119\"/><text class=\"po\" x=\"150.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2000</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"171.7\" y1=\"108\" x2=\"171.7\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"193.3\" y1=\"105\" x2=\"193.3\" y2=\"119\"/><text class=\"po\" x=\"193.3\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2010</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"215.0\" y1=\"108\" x2=\"215.0\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"236.7\" y1=\"105\" x2=\"236.7\" y2=\"119\"/><text class=\"po\" x=\"236.7\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2020</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"258.3\" y1=\"108\" x2=\"258.3\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"280.0\" y1=\"105\" x2=\"280.0\" y2=\"119\"/><text class=\"po\" x=\"280.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2030</text><circle class=\"dr\" cx=\"41.7\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(44.7,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">Aryabhata</text><circle class=\"dr\" cx=\"63.3\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(66.3,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">Rohini</text><circle class=\"dr\" cx=\"184.7\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(187.7,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">Chandrayaan-1</text><circle class=\"dr\" cx=\"206.3\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(209.3,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">Mangalyaan</text><circle class=\"dr\" cx=\"232.3\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(235.3,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">Chandrayaan-2</text><circle class=\"dr\" cx=\"249.7\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(252.7,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">Chandrayaan-3</text></svg>"}, {"kind": "blank", "p": "This time line shows events in Riya's life.", "tag": "", "marks": "", "flat": [{"t": "a) In which year was Riya born? __B1__", "a": {"B1": "2008"}}, {"t": "b) How old was she when she started school? __B1__", "a": {"B1": "5"}}, {"t": "c) How long after joining the swim club did she win her first medal? __B1__ years", "a": {"B1": "3"}}, {"t": "d) How old was she when she started college? __B1__", "a": {"B1": "18"}}], "sol": "a) 2008\nb) 2013 − 2008 = 5\nc) 2019 − 2016 = 3\nd) 2026 − 2008 = 18", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 150\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><line class=\"ln\" x1=\"10.0\" y1=\"112.0\" x2=\"290.0\" y2=\"112.0\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"20.0\" y1=\"105\" x2=\"20.0\" y2=\"119\"/><text class=\"po\" x=\"20.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2005</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"30.4\" y1=\"108\" x2=\"30.4\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"40.8\" y1=\"108\" x2=\"40.8\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"51.2\" y1=\"108\" x2=\"51.2\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"61.6\" y1=\"108\" x2=\"61.6\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"72.0\" y1=\"105\" x2=\"72.0\" y2=\"119\"/><text class=\"po\" x=\"72.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2010</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"82.4\" y1=\"108\" x2=\"82.4\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.8\" y1=\"108\" x2=\"92.8\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"103.2\" y1=\"108\" x2=\"103.2\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"113.6\" y1=\"108\" x2=\"113.6\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"124.0\" y1=\"105\" x2=\"124.0\" y2=\"119\"/><text class=\"po\" x=\"124.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2015</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"134.4\" y1=\"108\" x2=\"134.4\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"144.8\" y1=\"108\" x2=\"144.8\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"155.2\" y1=\"108\" x2=\"155.2\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"165.6\" y1=\"108\" x2=\"165.6\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"176.0\" y1=\"105\" x2=\"176.0\" y2=\"119\"/><text class=\"po\" x=\"176.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2020</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"186.4\" y1=\"108\" x2=\"186.4\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"196.8\" y1=\"108\" x2=\"196.8\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.2\" y1=\"108\" x2=\"207.2\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"217.6\" y1=\"108\" x2=\"217.6\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"228.0\" y1=\"105\" x2=\"228.0\" y2=\"119\"/><text class=\"po\" x=\"228.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2025</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"238.4\" y1=\"108\" x2=\"238.4\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"248.8\" y1=\"108\" x2=\"248.8\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"259.2\" y1=\"108\" x2=\"259.2\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"269.6\" y1=\"108\" x2=\"269.6\" y2=\"116\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.3\" x1=\"280.0\" y1=\"105\" x2=\"280.0\" y2=\"119\"/><text class=\"po\" x=\"280.0\" y=\"130.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2030</text><circle class=\"dr\" cx=\"51.2\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(54.2,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">born</text><circle class=\"dr\" cx=\"103.2\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(106.2,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">started school</text><circle class=\"dr\" cx=\"134.4\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(137.4,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">joined swim club</text><circle class=\"dr\" cx=\"165.6\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(168.6,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">first medal</text><circle class=\"dr\" cx=\"186.4\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(189.4,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">moved house</text><circle class=\"dr\" cx=\"238.4\" cy=\"112\" r=\"4\"/><text class=\"al\" transform=\"translate(241.4,102) rotate(-60)\" text-anchor=\"start\" style=\"font-size:10.5px\">started college</text></svg>"}, {"kind": "blank", "p": "There is no year 0: 1 BC is followed by AD 1. How many years are there between:", "tag": "", "marks": "", "flat": [{"t": "a) 3000 BC and 1000 BC? __B1__", "a": {"B1": "2000"}}, {"t": "b) 500 BC and AD 300? __B1__", "a": {"B1": "799"}}, {"t": "c) 2800 BC and AD 2026? __B1__", "a": {"B1": "4825"}}], "sol": "For two BC years, subtract. From a BC year to an AD year, add the numbers and subtract 1 (there is no year 0).\na) 3000 − 1000 = 2000\nb) 500 + 300 − 1 = 799\nc) 2800 + 2026 − 1 = 4825"}]}, {"id": "s2", "label": "Ex 11B", "sub": "Units of time", "slides": [{"kind": "blank", "p": "Which unit would you use for the time taken to (seconds, minutes, hours or days)?", "tag": "", "marks": "", "flat": [{"t": "a) brush your teeth → __B1__", "a": {"B1": "minutes"}}, {"t": "b) watch a movie → __B1__", "a": {"B1": "hours"}}, {"t": "c) run 100 metres → __B1__", "a": {"B1": "seconds"}}, {"t": "d) drink a glass of water → __B1__", "a": {"B1": "seconds"}}, {"t": "e) drive from Delhi to Chennai → __B1__", "a": {"B1": "days"}}], "sol": "Choose a unit that gives a sensible number."}, {"kind": "blank", "p": "Convert (1 week = 7 days, 1 day = 24 h, 1 h = 60 min, 1 min = 60 s):", "tag": "", "marks": "", "flat": [{"t": "a) 7 minutes = __B1__ seconds", "a": {"B1": "420"}}, {"t": "b) 10 days = __B1__ hours", "a": {"B1": "240"}}, {"t": "c) 4 hours = __B1__ minutes", "a": {"B1": "240"}}, {"t": "d) 5 weeks = __B1__ days", "a": {"B1": "35"}}, {"t": "e) 240 seconds = __B1__ minutes", "a": {"B1": "4"}}, {"t": "f) 14 days = __B1__ weeks", "a": {"B1": "2"}}, {"t": "g) 12 minutes = __B1__ seconds", "a": {"B1": "720"}}, {"t": "h) 180 minutes = __B1__ hours", "a": {"B1": "3"}}, {"t": "i) 144 hours = __B1__ days", "a": {"B1": "6"}}], "sol": "To a smaller unit, multiply; to a larger unit, divide.\na) 7 minutes = 420 seconds\nb) 10 days = 240 hours\nc) 4 hours = 240 minutes\nd) 5 weeks = 35 days\ne) 240 seconds = 4 minutes\nf) 14 days = 2 weeks\ng) 12 minutes = 720 seconds\nh) 180 minutes = 3 hours\ni) 144 hours = 6 days"}, {"kind": "blank", "p": "Jaya puts 120 cans on a shelf. Each can takes 4 seconds. How long does it take in minutes?", "tag": "", "marks": "", "flat": [{"t": "__B1__ minutes", "a": {"B1": "8"}}], "sol": "120 × 4 = 480 s = 8 min"}, {"kind": "blank", "p": "Write in minutes only:", "tag": "", "marks": "", "flat": [{"t": "a) 3 h 24 min = __B1__ min", "a": {"B1": "204"}}, {"t": "b) 5 h 43 min = __B1__ min", "a": {"B1": "343"}}, {"t": "c) 6 h 7 min = __B1__ min", "a": {"B1": "367"}}, {"t": "d) 8 h 39 min = __B1__ min", "a": {"B1": "519"}}], "sol": "hours × 60 + minutes\na) 3 × 60 + 24 = 204\nb) 5 × 60 + 43 = 343\nc) 6 × 60 + 7 = 367\nd) 8 × 60 + 39 = 519"}, {"kind": "blank", "p": "Write in seconds only:", "tag": "", "marks": "", "flat": [{"t": "a) 5 min 12 s = __B1__ s", "a": {"B1": "312"}}, {"t": "b) 35 min 27 s = __B1__ s", "a": {"B1": "2127"}}, {"t": "c) 15 min 48 s = __B1__ s", "a": {"B1": "948"}}, {"t": "d) 49 min 56 s = __B1__ s", "a": {"B1": "2996"}}], "sol": "minutes × 60 + seconds\na) 312 s\nb) 2127 s\nc) 948 s\nd) 2996 s"}, {"kind": "blank", "p": "Write in minutes and seconds:", "tag": "", "marks": "", "flat": [{"t": "a) 76 s = __B1__ min __B2__ s", "a": {"B1": "1", "B2": "16"}}, {"t": "b) 95 s = __B1__ min __B2__ s", "a": {"B1": "1", "B2": "35"}}, {"t": "c) 110 s = __B1__ min __B2__ s", "a": {"B1": "1", "B2": "50"}}, {"t": "d) 205 s = __B1__ min __B2__ s", "a": {"B1": "3", "B2": "25"}}, {"t": "e) 341 s = __B1__ min __B2__ s", "a": {"B1": "5", "B2": "41"}}, {"t": "f) 700 s = __B1__ min __B2__ s", "a": {"B1": "11", "B2": "40"}}], "sol": "Divide by 60: the quotient is minutes, the remainder is seconds.\na) 76 ÷ 60 = 1 r 16\nb) 95 ÷ 60 = 1 r 35\nc) 110 ÷ 60 = 1 r 50\nd) 205 ÷ 60 = 3 r 25\ne) 341 ÷ 60 = 5 r 41\nf) 700 ÷ 60 = 11 r 40"}, {"kind": "blank", "p": "Write in hours and minutes:", "tag": "", "marks": "", "flat": [{"t": "a) 85 min = __B1__ h __B2__ min", "a": {"B1": "1", "B2": "25"}}, {"t": "b) 100 min = __B1__ h __B2__ min", "a": {"B1": "1", "B2": "40"}}, {"t": "c) 129 min = __B1__ h __B2__ min", "a": {"B1": "2", "B2": "9"}}, {"t": "d) 146 min = __B1__ h __B2__ min", "a": {"B1": "2", "B2": "26"}}, {"t": "e) 258 min = __B1__ h __B2__ min", "a": {"B1": "4", "B2": "18"}}, {"t": "f) 499 min = __B1__ h __B2__ min", "a": {"B1": "8", "B2": "19"}}], "sol": "Divide by 60: the quotient is hours, the remainder is minutes.\na) 1 h 25 min\nb) 1 h 40 min\nc) 2 h 9 min\nd) 2 h 26 min\ne) 4 h 18 min\nf) 8 h 19 min"}, {"kind": "blank", "p": "Arjun spent 4 hours 40 minutes planting 35 trees.", "tag": "", "marks": "", "flat": [{"t": "a) Time in minutes: __B1__", "a": {"B1": "280"}}, {"t": "b) Average time per tree: __B1__ minutes", "a": {"B1": "8"}}], "sol": "a) 4 × 60 + 40 = 280\nb) 280 ÷ 35 = 8"}, {"kind": "blank", "p": "Neha runs for 25 minutes every day for two weeks. Find the total time.", "tag": "", "marks": "", "flat": [{"t": "__B1__ h __B2__ min", "a": {"B1": "5", "B2": "50"}}], "sol": "14 × 25 = 350 min = 5 h 50 min"}]}, {"id": "s3", "label": "Ex 11C", "sub": "The calendar year", "slides": [{"kind": "blank", "p": "Is each year a leap year? (yes/no)", "tag": "", "marks": "", "flat": [{"t": "a) 2020 → __B1__", "a": {"B1": "yes"}}, {"t": "b) 2025 → __B1__", "a": {"B1": "no"}}, {"t": "c) 2200 → __B1__", "a": {"B1": "no"}}, {"t": "d) 2400 → __B1__", "a": {"B1": "yes"}}, {"t": "e) 1900 → __B1__", "a": {"B1": "no"}}, {"t": "f) 2028 → __B1__", "a": {"B1": "yes"}}], "sol": "A leap year is divisible by 4, but century years must be divisible by 400.\na) 2020: yes\nb) 2025: no\nc) 2200: no\nd) 2400: yes\ne) 1900: no\nf) 2028: yes"}, {"kind": "blank", "p": "Find the number of:", "tag": "", "marks": "", "flat": [{"t": "a) days in 2026: __B1__", "a": {"B1": "365"}}, {"t": "b) months in 6 years: __B1__", "a": {"B1": "72"}}, {"t": "c) hours in June: __B1__", "a": {"B1": "720"}}, {"t": "d) hours in March: __B1__", "a": {"B1": "744"}}], "sol": "a) 2026 is not a leap year: 365\nb) 6 × 12 = 72\nc) 30 × 24 = 720\nd) 31 × 24 = 744"}, {"kind": "blank", "p": "Aman is 40 months old. Tara is 3 years old. Who is older?", "tag": "", "marks": "", "flat": [{"t": "__B1__", "a": {"B1": "Aman"}}], "sol": "3 years = 36 months, and 40 > 36, so Aman is older."}, {"kind": "blank", "p": "A four-year period includes one leap year. Write this period in:", "tag": "", "marks": "", "flat": [{"t": "a) months: __B1__", "a": {"B1": "48"}}, {"t": "b) days: __B1__", "a": {"B1": "1461"}}, {"t": "c) hours: __B1__", "a": {"B1": "35064"}}], "sol": "a) 4 × 12 = 48\nb) 3 × 365 + 366 = 1461\nc) 1461 × 24 = 35 064"}, {"kind": "blank", "p": "Find the number of days from (2026 dates, not a leap year):", "tag": "", "marks": "", "flat": [{"t": "a) March 11 to April 7 → __B1__", "a": {"B1": "27"}}, {"t": "b) May 11 to June 23 → __B1__", "a": {"B1": "43"}}, {"t": "c) July 12 to November 6 → __B1__", "a": {"B1": "117"}}, {"t": "d) September 19 to January 8 → __B1__", "a": {"B1": "111"}}, {"t": "e) January 7 to March 16 → __B1__", "a": {"B1": "68"}}], "sol": "Count the days left in the first month, add the full months, then add the days in the last month.\na) 27 days\nb) 43 days\nc) 117 days\nd) 111 days\ne) 68 days"}, {"kind": "blank", "p": "Today is March 23rd. A shop will hold a ₹2700 bicycle until May 7th.", "tag": "", "marks": "", "flat": [{"t": "a) How many days does Rohan have to save? __B1__", "a": {"B1": "45"}}, {"t": "b) How much must he save each day? ₹__B1__", "a": {"B1": "60"}}], "sol": "a) 8 + 30 + 7 = 45 days\nb) 2700 ÷ 45 = ₹60"}, {"kind": "blank", "p": "Priya arrived in Chennai on February 17th, 2026. On what date did she celebrate 100 days there?", "tag": "", "marks": "", "flat": [{"t": "__B1__ (e.g. June 3)", "a": {"B1": "May 28"}, "expr": "words"}], "sol": "February 17 + 100 days = May 28"}]}, {"id": "s4", "label": "Ex 11D", "sub": "Time calculations", "slides": [{"kind": "blank", "p": "Find the time which is (type like 3:15 pm):", "tag": "", "marks": "", "flat": [{"t": "a) 4 hours  after 3:00 am → __B1__", "a": {"B1": "7:00 am"}, "expr": "time"}, {"t": "b) 34 minutes after 6:15 am → __B1__", "a": {"B1": "6:49 am"}, "expr": "time"}, {"t": "c) 2 hours 13 minutes after 8:19 pm → __B1__", "a": {"B1": "10:32 pm"}, "expr": "time"}, {"t": "d) 1 hours 47 minutes after 1:30 pm → __B1__", "a": {"B1": "3:17 pm"}, "expr": "time"}, {"t": "e) 3 hours 27 minutes after 12:42 pm → __B1__", "a": {"B1": "4:09 pm"}, "expr": "time"}, {"t": "f) 5 hours 48 minutes after 9:51 am → __B1__", "a": {"B1": "3:39 pm"}, "expr": "time"}], "sol": "Add the hours first, then the minutes.\na) 7:00 am\nb) 6:49 am\nc) 10:32 pm\nd) 3:17 pm\ne) 4:09 pm\nf) 3:39 pm"}, {"kind": "blank", "p": "Find the time which is:", "tag": "", "marks": "", "flat": [{"t": "a) 5 hours  before 8:00 pm → __B1__", "a": {"B1": "3:00 pm"}, "expr": "time"}, {"t": "b) 21 minutes before 7:45 pm → __B1__", "a": {"B1": "7:24 pm"}, "expr": "time"}, {"t": "c) 2 hours 55 minutes before 2:00 pm → __B1__", "a": {"B1": "11:05 am"}, "expr": "time"}, {"t": "d) 1 hours 40 minutes before 5:25 am → __B1__", "a": {"B1": "3:45 am"}, "expr": "time"}, {"t": "e) 4 hours 47 minutes before 6:15 pm → __B1__", "a": {"B1": "1:28 pm"}, "expr": "time"}], "sol": "Subtract the hours first, then the minutes.\na) 3:00 pm\nb) 7:24 pm\nc) 11:05 am\nd) 3:45 am\ne) 1:28 pm"}, {"kind": "blank", "p": "High tide is at 1:45 am. Low tide is 6 hours 20 minutes later. When is low tide?", "tag": "", "marks": "", "flat": [{"t": "__B1__", "a": {"B1": "8:05 am"}, "expr": "time"}], "sol": "1:45 am + 6 h = 7:45 am; + 20 min = 8:05 am"}, {"kind": "blank", "p": "Dev must reach his friend's farm by 12:30 pm. The drive takes 1 hour 40 minutes. When should he leave?", "tag": "", "marks": "", "flat": [{"t": "__B1__", "a": {"B1": "10:50 am"}, "expr": "time"}], "sol": "12:30 pm − 1 h = 11:30 am; − 40 min = 10:50 am"}, {"kind": "blank", "p": "Find the time difference between:", "tag": "", "marks": "", "flat": [{"t": "a) 7:20 am and 10:40 am → __B1__ h __B2__ min", "a": {"B1": "3", "B2": "20"}}, {"t": "b) 11:15 am and 5:20 pm → __B1__ h __B2__ min", "a": {"B1": "6", "B2": "5"}}, {"t": "c) 3:30 pm and 9:16 pm → __B1__ h __B2__ min", "a": {"B1": "5", "B2": "46"}}, {"t": "d) 8:24 am and 7:11 pm → __B1__ h __B2__ min", "a": {"B1": "10", "B2": "47"}}], "sol": "Count on in hours, then minutes.\na) 3 h 20 min\nb) 6 h 5 min\nc) 5 h 46 min\nd) 10 h 47 min"}, {"kind": "blank", "p": "Meera fell asleep at 10:26 pm and woke at 6:05 am the next day. How long did she sleep?", "tag": "", "marks": "", "flat": [{"t": "__B1__ h __B2__ min", "a": {"B1": "7", "B2": "39"}}], "sol": "10:26 pm to 5:26 am = 7 h; 5:26 am to 6:05 am = 39 min"}, {"kind": "blank", "p": "A watch loses 3 seconds every hour. It shows the correct time at 8 am. What time will it show when the real time is 5 pm?", "tag": "", "marks": "", "flat": [{"t": "__B1__ (like 4:59:33 pm)", "a": {"B1": "4:59:33 pm"}, "expr": "time"}], "sol": "8 am to 5 pm is 9 hours, so it loses 27 seconds: 4:59:33 pm"}]}, {"id": "s5", "label": "Ex 11E", "sub": "24-hour time", "slides": [{"kind": "blank", "p": "Write in 24-hour time (4 digits, e.g. 08:55). 12:00 am is midnight and 12:00 pm is noon.", "tag": "", "marks": "", "flat": [{"t": "a) 3:13 am → __B1__", "a": {"B1": "03:13"}, "expr": "time"}, {"t": "b) 11:17 am → __B1__", "a": {"B1": "11:17"}, "expr": "time"}, {"t": "c) 12:00 am → __B1__", "a": {"B1": "00:00"}, "expr": "time"}, {"t": "d) 12:47 pm → __B1__", "a": {"B1": "12:47"}, "expr": "time"}, {"t": "e) 5:41 pm → __B1__", "a": {"B1": "17:41"}, "expr": "time"}, {"t": "f) 9:22 am → __B1__", "a": {"B1": "09:22"}, "expr": "time"}, {"t": "g) 2:09 pm → __B1__", "a": {"B1": "14:09"}, "expr": "time"}, {"t": "h) 12:00 pm → __B1__", "a": {"B1": "12:00"}, "expr": "time"}, {"t": "i) 10:56 am → __B1__", "a": {"B1": "10:56"}, "expr": "time"}, {"t": "j) 6:14 pm → __B1__", "a": {"B1": "18:14"}, "expr": "time"}, {"t": "k) 8:19 pm → __B1__", "a": {"B1": "20:19"}, "expr": "time"}, {"t": "l) 11:59 pm → __B1__", "a": {"B1": "23:59"}, "expr": "time"}], "sol": "am times: keep the hours (12 am → 00). pm times: add 12 to the hours (except 12 pm).\na) 03:13\nb) 11:17\nc) 00:00\nd) 12:47\ne) 17:41\nf) 09:22\ng) 14:09\nh) 12:00\ni) 10:56\nj) 18:14\nk) 20:19\nl) 23:59"}, {"kind": "blank", "p": "Write in 12-hour time (e.g. 4:30 pm):", "tag": "", "marks": "", "flat": [{"t": "a) 03:40 → __B1__", "a": {"B1": "3:40 am"}, "expr": "time"}, {"t": "b) 06:35 → __B1__", "a": {"B1": "6:35 am"}, "expr": "time"}, {"t": "c) 18:26 → __B1__", "a": {"B1": "6:26 pm"}, "expr": "time"}, {"t": "d) 12:00 → __B1__", "a": {"B1": "12:00 pm"}, "expr": "time"}, {"t": "e) 19:39 → __B1__", "a": {"B1": "7:39 pm"}, "expr": "time"}, {"t": "f) 06:15 → __B1__", "a": {"B1": "6:15 am"}, "expr": "time"}, {"t": "g) 15:45 → __B1__", "a": {"B1": "3:45 pm"}, "expr": "time"}, {"t": "h) 20:17 → __B1__", "a": {"B1": "8:17 pm"}, "expr": "time"}, {"t": "i) 13:11 → __B1__", "a": {"B1": "1:11 pm"}, "expr": "time"}, {"t": "j) 23:48 → __B1__", "a": {"B1": "11:48 pm"}, "expr": "time"}], "sol": "Hours 00–11 are am; 12–23 are pm (subtract 12 from 13–23).\na) 3:40 am\nb) 6:35 am\nc) 6:26 pm\nd) 12:00 pm\ne) 7:39 pm\nf) 6:15 am\ng) 3:45 pm\nh) 8:17 pm\ni) 1:11 pm\nj) 11:48 pm"}, {"kind": "mcq", "text": "What is wrong with the 24-hour time 08:62?", "opts": ["There are only 60 minutes in an hour", "The hour cannot start with 0", "Nothing", "It should be written 8:62"], "correct": 0, "tag": "", "sol": "Minutes go from 00 to 59, so 62 is impossible."}, {"kind": "mcq", "text": "What is wrong with the 24-hour time 25:41?", "opts": ["Hours go from 00 to 23, so 25 is impossible", "Minutes cannot be 41", "Nothing", "It needs am or pm"], "correct": 0, "tag": "", "sol": "The largest hour in 24-hour time is 23."}, {"kind": "blank", "p": "Write the time on each clock in 24-hour time:", "tag": "", "marks": "", "flat": [{"t": "a) morning → __B1__", "a": {"B1": "07:15"}, "expr": "time", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 170\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><circle class=\"sh\" cx=\"150\" cy=\"80\" r=\"62\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"150.0\" y1=\"20.0\" x2=\"150.0\" y2=\"27.0\"/><text class=\"po\" x=\"150.0\" y=\"37.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">12</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"156.3\" y1=\"20.3\" x2=\"156.0\" y2=\"23.3\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"162.5\" y1=\"21.3\" x2=\"161.9\" y2=\"24.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"168.5\" y1=\"22.9\" x2=\"167.6\" y2=\"25.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"174.4\" y1=\"25.2\" x2=\"173.2\" y2=\"27.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"180.0\" y1=\"28.0\" x2=\"176.5\" y2=\"34.1\"/><text class=\"po\" x=\"171.5\" y=\"42.8\" text-anchor=\"middle\" dominant-baseline=\"middle\">1</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"185.3\" y1=\"31.5\" x2=\"183.5\" y2=\"33.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"190.1\" y1=\"35.4\" x2=\"188.1\" y2=\"37.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"194.6\" y1=\"39.9\" x2=\"192.4\" y2=\"41.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"198.5\" y1=\"44.7\" x2=\"196.1\" y2=\"46.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"202.0\" y1=\"50.0\" x2=\"195.9\" y2=\"53.5\"/><text class=\"po\" x=\"187.2\" y=\"58.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"204.8\" y1=\"55.6\" x2=\"202.1\" y2=\"56.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.1\" y1=\"61.5\" x2=\"204.2\" y2=\"62.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"208.7\" y1=\"67.5\" x2=\"205.8\" y2=\"68.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"209.7\" y1=\"73.7\" x2=\"206.7\" y2=\"74.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"210.0\" y1=\"80.0\" x2=\"203.0\" y2=\"80.0\"/><text class=\"po\" x=\"193.0\" y=\"80.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">3</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"209.7\" y1=\"86.3\" x2=\"206.7\" y2=\"86.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"208.7\" y1=\"92.5\" x2=\"205.8\" y2=\"91.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.1\" y1=\"98.5\" x2=\"204.2\" y2=\"97.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"204.8\" y1=\"104.4\" x2=\"202.1\" y2=\"103.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"202.0\" y1=\"110.0\" x2=\"195.9\" y2=\"106.5\"/><text class=\"po\" x=\"187.2\" y=\"101.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">4</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"198.5\" y1=\"115.3\" x2=\"196.1\" y2=\"113.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"194.6\" y1=\"120.1\" x2=\"192.4\" y2=\"118.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"190.1\" y1=\"124.6\" x2=\"188.1\" y2=\"122.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"185.3\" y1=\"128.5\" x2=\"183.5\" y2=\"126.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"180.0\" y1=\"132.0\" x2=\"176.5\" y2=\"125.9\"/><text class=\"po\" x=\"171.5\" y=\"117.2\" text-anchor=\"middle\" dominant-baseline=\"middle\">5</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"174.4\" y1=\"134.8\" x2=\"173.2\" y2=\"132.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"168.5\" y1=\"137.1\" x2=\"167.6\" y2=\"134.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"162.5\" y1=\"138.7\" x2=\"161.9\" y2=\"135.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"156.3\" y1=\"139.7\" x2=\"156.0\" y2=\"136.7\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"150.0\" y1=\"140.0\" x2=\"150.0\" y2=\"133.0\"/><text class=\"po\" x=\"150.0\" y=\"123.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">6</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"143.7\" y1=\"139.7\" x2=\"144.0\" y2=\"136.7\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"137.5\" y1=\"138.7\" x2=\"138.1\" y2=\"135.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"131.5\" y1=\"137.1\" x2=\"132.4\" y2=\"134.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"125.6\" y1=\"134.8\" x2=\"126.8\" y2=\"132.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"120.0\" y1=\"132.0\" x2=\"123.5\" y2=\"125.9\"/><text class=\"po\" x=\"128.5\" y=\"117.2\" text-anchor=\"middle\" dominant-baseline=\"middle\">7</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"114.7\" y1=\"128.5\" x2=\"116.5\" y2=\"126.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"109.9\" y1=\"124.6\" x2=\"111.9\" y2=\"122.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"105.4\" y1=\"120.1\" x2=\"107.6\" y2=\"118.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"101.5\" y1=\"115.3\" x2=\"103.9\" y2=\"113.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"98.0\" y1=\"110.0\" x2=\"104.1\" y2=\"106.5\"/><text class=\"po\" x=\"112.8\" y=\"101.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">8</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"95.2\" y1=\"104.4\" x2=\"97.9\" y2=\"103.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.9\" y1=\"98.5\" x2=\"95.8\" y2=\"97.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"91.3\" y1=\"92.5\" x2=\"94.2\" y2=\"91.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"90.3\" y1=\"86.3\" x2=\"93.3\" y2=\"86.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"90.0\" y1=\"80.0\" x2=\"97.0\" y2=\"80.0\"/><text class=\"po\" x=\"107.0\" y=\"80.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">9</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"90.3\" y1=\"73.7\" x2=\"93.3\" y2=\"74.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"91.3\" y1=\"67.5\" x2=\"94.2\" y2=\"68.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.9\" y1=\"61.5\" x2=\"95.8\" y2=\"62.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"95.2\" y1=\"55.6\" x2=\"97.9\" y2=\"56.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"98.0\" y1=\"50.0\" x2=\"104.1\" y2=\"53.5\"/><text class=\"po\" x=\"112.8\" y=\"58.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">10</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"101.5\" y1=\"44.7\" x2=\"103.9\" y2=\"46.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"105.4\" y1=\"39.9\" x2=\"107.6\" y2=\"41.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"109.9\" y1=\"35.4\" x2=\"111.9\" y2=\"37.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"114.7\" y1=\"31.5\" x2=\"116.5\" y2=\"33.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"120.0\" y1=\"28.0\" x2=\"123.5\" y2=\"34.1\"/><text class=\"po\" x=\"128.5\" y=\"42.8\" text-anchor=\"middle\" dominant-baseline=\"middle\">11</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"125.6\" y1=\"25.2\" x2=\"126.8\" y2=\"27.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"131.5\" y1=\"22.9\" x2=\"132.4\" y2=\"25.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"137.5\" y1=\"21.3\" x2=\"138.1\" y2=\"24.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"143.7\" y1=\"20.3\" x2=\"144.0\" y2=\"23.3\"/><line class=\"arm\" style=\"stroke:var(--ink);stroke-width:3.5;stroke-linecap:round\" x1=\"150\" y1=\"80\" x2=\"131.1\" y2=\"104.6\"/><line class=\"arm\" style=\"stroke:var(--ink);stroke-width:2.2;stroke-linecap:round\" x1=\"150\" y1=\"80\" x2=\"198.4\" y2=\"80.0\"/><circle class=\"pt\" cx=\"150\" cy=\"80\" r=\"3.5\"/><text class=\"al\" x=\"150.0\" y=\"156.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">morning</text></svg>"}, {"t": "b) afternoon → __B1__", "a": {"B1": "14:50"}, "expr": "time", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 170\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><circle class=\"sh\" cx=\"150\" cy=\"80\" r=\"62\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"150.0\" y1=\"20.0\" x2=\"150.0\" y2=\"27.0\"/><text class=\"po\" x=\"150.0\" y=\"37.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">12</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"156.3\" y1=\"20.3\" x2=\"156.0\" y2=\"23.3\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"162.5\" y1=\"21.3\" x2=\"161.9\" y2=\"24.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"168.5\" y1=\"22.9\" x2=\"167.6\" y2=\"25.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"174.4\" y1=\"25.2\" x2=\"173.2\" y2=\"27.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"180.0\" y1=\"28.0\" x2=\"176.5\" y2=\"34.1\"/><text class=\"po\" x=\"171.5\" y=\"42.8\" text-anchor=\"middle\" dominant-baseline=\"middle\">1</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"185.3\" y1=\"31.5\" x2=\"183.5\" y2=\"33.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"190.1\" y1=\"35.4\" x2=\"188.1\" y2=\"37.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"194.6\" y1=\"39.9\" x2=\"192.4\" y2=\"41.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"198.5\" y1=\"44.7\" x2=\"196.1\" y2=\"46.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"202.0\" y1=\"50.0\" x2=\"195.9\" y2=\"53.5\"/><text class=\"po\" x=\"187.2\" y=\"58.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"204.8\" y1=\"55.6\" x2=\"202.1\" y2=\"56.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.1\" y1=\"61.5\" x2=\"204.2\" y2=\"62.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"208.7\" y1=\"67.5\" x2=\"205.8\" y2=\"68.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"209.7\" y1=\"73.7\" x2=\"206.7\" y2=\"74.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"210.0\" y1=\"80.0\" x2=\"203.0\" y2=\"80.0\"/><text class=\"po\" x=\"193.0\" y=\"80.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">3</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"209.7\" y1=\"86.3\" x2=\"206.7\" y2=\"86.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"208.7\" y1=\"92.5\" x2=\"205.8\" y2=\"91.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.1\" y1=\"98.5\" x2=\"204.2\" y2=\"97.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"204.8\" y1=\"104.4\" x2=\"202.1\" y2=\"103.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"202.0\" y1=\"110.0\" x2=\"195.9\" y2=\"106.5\"/><text class=\"po\" x=\"187.2\" y=\"101.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">4</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"198.5\" y1=\"115.3\" x2=\"196.1\" y2=\"113.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"194.6\" y1=\"120.1\" x2=\"192.4\" y2=\"118.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"190.1\" y1=\"124.6\" x2=\"188.1\" y2=\"122.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"185.3\" y1=\"128.5\" x2=\"183.5\" y2=\"126.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"180.0\" y1=\"132.0\" x2=\"176.5\" y2=\"125.9\"/><text class=\"po\" x=\"171.5\" y=\"117.2\" text-anchor=\"middle\" dominant-baseline=\"middle\">5</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"174.4\" y1=\"134.8\" x2=\"173.2\" y2=\"132.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"168.5\" y1=\"137.1\" x2=\"167.6\" y2=\"134.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"162.5\" y1=\"138.7\" x2=\"161.9\" y2=\"135.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"156.3\" y1=\"139.7\" x2=\"156.0\" y2=\"136.7\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"150.0\" y1=\"140.0\" x2=\"150.0\" y2=\"133.0\"/><text class=\"po\" x=\"150.0\" y=\"123.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">6</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"143.7\" y1=\"139.7\" x2=\"144.0\" y2=\"136.7\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"137.5\" y1=\"138.7\" x2=\"138.1\" y2=\"135.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"131.5\" y1=\"137.1\" x2=\"132.4\" y2=\"134.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"125.6\" y1=\"134.8\" x2=\"126.8\" y2=\"132.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"120.0\" y1=\"132.0\" x2=\"123.5\" y2=\"125.9\"/><text class=\"po\" x=\"128.5\" y=\"117.2\" text-anchor=\"middle\" dominant-baseline=\"middle\">7</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"114.7\" y1=\"128.5\" x2=\"116.5\" y2=\"126.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"109.9\" y1=\"124.6\" x2=\"111.9\" y2=\"122.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"105.4\" y1=\"120.1\" x2=\"107.6\" y2=\"118.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"101.5\" y1=\"115.3\" x2=\"103.9\" y2=\"113.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"98.0\" y1=\"110.0\" x2=\"104.1\" y2=\"106.5\"/><text class=\"po\" x=\"112.8\" y=\"101.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">8</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"95.2\" y1=\"104.4\" x2=\"97.9\" y2=\"103.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.9\" y1=\"98.5\" x2=\"95.8\" y2=\"97.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"91.3\" y1=\"92.5\" x2=\"94.2\" y2=\"91.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"90.3\" y1=\"86.3\" x2=\"93.3\" y2=\"86.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"90.0\" y1=\"80.0\" x2=\"97.0\" y2=\"80.0\"/><text class=\"po\" x=\"107.0\" y=\"80.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">9</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"90.3\" y1=\"73.7\" x2=\"93.3\" y2=\"74.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"91.3\" y1=\"67.5\" x2=\"94.2\" y2=\"68.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.9\" y1=\"61.5\" x2=\"95.8\" y2=\"62.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"95.2\" y1=\"55.6\" x2=\"97.9\" y2=\"56.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"98.0\" y1=\"50.0\" x2=\"104.1\" y2=\"53.5\"/><text class=\"po\" x=\"112.8\" y=\"58.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">10</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"101.5\" y1=\"44.7\" x2=\"103.9\" y2=\"46.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"105.4\" y1=\"39.9\" x2=\"107.6\" y2=\"41.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"109.9\" y1=\"35.4\" x2=\"111.9\" y2=\"37.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"114.7\" y1=\"31.5\" x2=\"116.5\" y2=\"33.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"120.0\" y1=\"28.0\" x2=\"123.5\" y2=\"34.1\"/><text class=\"po\" x=\"128.5\" y=\"42.8\" text-anchor=\"middle\" dominant-baseline=\"middle\">11</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"125.6\" y1=\"25.2\" x2=\"126.8\" y2=\"27.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"131.5\" y1=\"22.9\" x2=\"132.4\" y2=\"25.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"137.5\" y1=\"21.3\" x2=\"138.1\" y2=\"24.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"143.7\" y1=\"20.3\" x2=\"144.0\" y2=\"23.3\"/><line class=\"arm\" style=\"stroke:var(--ink);stroke-width:3.5;stroke-linecap:round\" x1=\"150\" y1=\"80\" x2=\"180.9\" y2=\"77.3\"/><line class=\"arm\" style=\"stroke:var(--ink);stroke-width:2.2;stroke-linecap:round\" x1=\"150\" y1=\"80\" x2=\"108.1\" y2=\"55.8\"/><circle class=\"pt\" cx=\"150\" cy=\"80\" r=\"3.5\"/><text class=\"al\" x=\"150.0\" y=\"156.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">afternoon</text></svg>"}, {"t": "c) evening → __B1__", "a": {"B1": "20:40"}, "expr": "time", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 170\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><circle class=\"sh\" cx=\"150\" cy=\"80\" r=\"62\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"150.0\" y1=\"20.0\" x2=\"150.0\" y2=\"27.0\"/><text class=\"po\" x=\"150.0\" y=\"37.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">12</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"156.3\" y1=\"20.3\" x2=\"156.0\" y2=\"23.3\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"162.5\" y1=\"21.3\" x2=\"161.9\" y2=\"24.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"168.5\" y1=\"22.9\" x2=\"167.6\" y2=\"25.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"174.4\" y1=\"25.2\" x2=\"173.2\" y2=\"27.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"180.0\" y1=\"28.0\" x2=\"176.5\" y2=\"34.1\"/><text class=\"po\" x=\"171.5\" y=\"42.8\" text-anchor=\"middle\" dominant-baseline=\"middle\">1</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"185.3\" y1=\"31.5\" x2=\"183.5\" y2=\"33.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"190.1\" y1=\"35.4\" x2=\"188.1\" y2=\"37.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"194.6\" y1=\"39.9\" x2=\"192.4\" y2=\"41.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"198.5\" y1=\"44.7\" x2=\"196.1\" y2=\"46.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"202.0\" y1=\"50.0\" x2=\"195.9\" y2=\"53.5\"/><text class=\"po\" x=\"187.2\" y=\"58.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"204.8\" y1=\"55.6\" x2=\"202.1\" y2=\"56.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.1\" y1=\"61.5\" x2=\"204.2\" y2=\"62.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"208.7\" y1=\"67.5\" x2=\"205.8\" y2=\"68.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"209.7\" y1=\"73.7\" x2=\"206.7\" y2=\"74.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"210.0\" y1=\"80.0\" x2=\"203.0\" y2=\"80.0\"/><text class=\"po\" x=\"193.0\" y=\"80.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">3</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"209.7\" y1=\"86.3\" x2=\"206.7\" y2=\"86.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"208.7\" y1=\"92.5\" x2=\"205.8\" y2=\"91.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"207.1\" y1=\"98.5\" x2=\"204.2\" y2=\"97.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"204.8\" y1=\"104.4\" x2=\"202.1\" y2=\"103.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"202.0\" y1=\"110.0\" x2=\"195.9\" y2=\"106.5\"/><text class=\"po\" x=\"187.2\" y=\"101.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">4</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"198.5\" y1=\"115.3\" x2=\"196.1\" y2=\"113.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"194.6\" y1=\"120.1\" x2=\"192.4\" y2=\"118.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"190.1\" y1=\"124.6\" x2=\"188.1\" y2=\"122.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"185.3\" y1=\"128.5\" x2=\"183.5\" y2=\"126.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"180.0\" y1=\"132.0\" x2=\"176.5\" y2=\"125.9\"/><text class=\"po\" x=\"171.5\" y=\"117.2\" text-anchor=\"middle\" dominant-baseline=\"middle\">5</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"174.4\" y1=\"134.8\" x2=\"173.2\" y2=\"132.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"168.5\" y1=\"137.1\" x2=\"167.6\" y2=\"134.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"162.5\" y1=\"138.7\" x2=\"161.9\" y2=\"135.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"156.3\" y1=\"139.7\" x2=\"156.0\" y2=\"136.7\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"150.0\" y1=\"140.0\" x2=\"150.0\" y2=\"133.0\"/><text class=\"po\" x=\"150.0\" y=\"123.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">6</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"143.7\" y1=\"139.7\" x2=\"144.0\" y2=\"136.7\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"137.5\" y1=\"138.7\" x2=\"138.1\" y2=\"135.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"131.5\" y1=\"137.1\" x2=\"132.4\" y2=\"134.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"125.6\" y1=\"134.8\" x2=\"126.8\" y2=\"132.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"120.0\" y1=\"132.0\" x2=\"123.5\" y2=\"125.9\"/><text class=\"po\" x=\"128.5\" y=\"117.2\" text-anchor=\"middle\" dominant-baseline=\"middle\">7</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"114.7\" y1=\"128.5\" x2=\"116.5\" y2=\"126.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"109.9\" y1=\"124.6\" x2=\"111.9\" y2=\"122.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"105.4\" y1=\"120.1\" x2=\"107.6\" y2=\"118.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"101.5\" y1=\"115.3\" x2=\"103.9\" y2=\"113.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"98.0\" y1=\"110.0\" x2=\"104.1\" y2=\"106.5\"/><text class=\"po\" x=\"112.8\" y=\"101.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">8</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"95.2\" y1=\"104.4\" x2=\"97.9\" y2=\"103.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.9\" y1=\"98.5\" x2=\"95.8\" y2=\"97.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"91.3\" y1=\"92.5\" x2=\"94.2\" y2=\"91.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"90.3\" y1=\"86.3\" x2=\"93.3\" y2=\"86.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"90.0\" y1=\"80.0\" x2=\"97.0\" y2=\"80.0\"/><text class=\"po\" x=\"107.0\" y=\"80.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">9</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"90.3\" y1=\"73.7\" x2=\"93.3\" y2=\"74.0\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"91.3\" y1=\"67.5\" x2=\"94.2\" y2=\"68.1\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"92.9\" y1=\"61.5\" x2=\"95.8\" y2=\"62.4\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"95.2\" y1=\"55.6\" x2=\"97.9\" y2=\"56.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"98.0\" y1=\"50.0\" x2=\"104.1\" y2=\"53.5\"/><text class=\"po\" x=\"112.8\" y=\"58.5\" text-anchor=\"middle\" dominant-baseline=\"middle\">10</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"101.5\" y1=\"44.7\" x2=\"103.9\" y2=\"46.5\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"105.4\" y1=\"39.9\" x2=\"107.6\" y2=\"41.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"109.9\" y1=\"35.4\" x2=\"111.9\" y2=\"37.6\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"114.7\" y1=\"31.5\" x2=\"116.5\" y2=\"33.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:1.5\" x1=\"120.0\" y1=\"28.0\" x2=\"123.5\" y2=\"34.1\"/><text class=\"po\" x=\"128.5\" y=\"42.8\" text-anchor=\"middle\" dominant-baseline=\"middle\">11</text><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"125.6\" y1=\"25.2\" x2=\"126.8\" y2=\"27.9\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"131.5\" y1=\"22.9\" x2=\"132.4\" y2=\"25.8\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"137.5\" y1=\"21.3\" x2=\"138.1\" y2=\"24.2\"/><line class=\"tk\" style=\"stroke:var(--ink);stroke-width:0.7\" x1=\"143.7\" y1=\"20.3\" x2=\"144.0\" y2=\"23.3\"/><line class=\"arm\" style=\"stroke:var(--ink);stroke-width:3.5;stroke-linecap:round\" x1=\"150\" y1=\"80\" x2=\"119.5\" y2=\"85.4\"/><line class=\"arm\" style=\"stroke:var(--ink);stroke-width:2.2;stroke-linecap:round\" x1=\"150\" y1=\"80\" x2=\"108.1\" y2=\"104.2\"/><circle class=\"pt\" cx=\"150\" cy=\"80\" r=\"3.5\"/><text class=\"al\" x=\"150.0\" y=\"156.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">evening</text></svg>"}], "sol": "a) 7:15 am = 07:15\nb) 2:50 pm = 14:50\nc) 8:40 pm = 20:40"}, {"kind": "blank", "p": "Arrivals at Delhi airport (24-hour time):", "tag": "", "marks": "", "flat": [{"t": "a) Which flight is due at 3:50 pm? __B1__", "a": {"B1": "AI 202"}}, {"t": "b) Flight 6E 71 is delayed 1 h 35 min. New arrival time (24-hour): __B1__", "a": {"B1": "18:00"}, "expr": "time"}, {"t": "c) How long before flight UK 18 is flight AI 305 due? __B1__ h __B2__ min", "a": {"B1": "2", "B2": "35"}}], "sol": "a) 3:50 pm = 15:50 → AI 202\nb) 16:25 + 1:35 = 18:00\nc) 17:15 − 14:40 = 2 h 35 min", "fig": "<div class=\"ttw\"><table class=\"tt\"><tr><th>Flight</th><th>From</th><th>Arrival</th></tr><tr><td>AI 305</td><td>Mumbai</td><td>14:40</td></tr><tr><td>AI 202</td><td>London</td><td>15:50</td></tr><tr><td>6E 71</td><td>Chennai</td><td>16:25</td></tr><tr><td>SG 40</td><td>Dubai</td><td>16:45</td></tr><tr><td>UK 18</td><td>Singapore</td><td>17:15</td></tr></table></div>"}]}, {"id": "s6", "label": "Ex 11F", "sub": "Timetables", "slides": [{"kind": "blank", "p": "This timetable shows one school day.", "tag": "", "marks": "", "flat": [{"t": "a) At what time does Science start? __B1__", "a": {"B1": "10:50"}, "expr": "time"}, {"t": "b) Which class is on at 1:30 pm? __B1__", "a": {"B1": "English"}}, {"t": "c) How long is the Music class? __B1__ min", "a": {"B1": "45"}}, {"t": "d) How long is Mathematics? __B1__ min", "a": {"B1": "50"}}, {"t": "e) How long is the school day? __B1__ h __B2__ min", "a": {"B1": "6", "B2": "10"}}], "sol": "a) 10:50\nb) English (1:25–2:10)\nc) 45 min\nd) 50 min\ne) 8:00 am to 2:10 pm = 6 h 10 min", "fig": "<div class=\"ttw\"><table class=\"tt\"><tr><th>Class</th><th>Time</th></tr><tr><td>Hindi</td><td>8:00 – 8:45</td></tr><tr><td>Music</td><td>8:45 – 9:30</td></tr><tr><td>Break</td><td>9:30 – 10:00</td></tr><tr><td>Mathematics</td><td>10:00 – 10:50</td></tr><tr><td>Science</td><td>10:50 – 11:40</td></tr><tr><td>Lunch</td><td>11:40 – 12:40</td></tr><tr><td>Sport</td><td>12:40 – 1:25</td></tr><tr><td>English</td><td>1:25 – 2:10</td></tr></table></div>"}, {"kind": "blank", "p": "A city tour bus timetable (Bus A, B, C):", "tag": "", "marks": "", "flat": [{"t": "a) How many buses are there? __B1__", "a": {"B1": "3"}}, {"t": "b) What is the latest departure time from the Railway Station? __B1__", "a": {"B1": "09:40"}, "expr": "time"}, {"t": "c) How long does Bus A take from the Zoo to the Fort? __B1__ min", "a": {"B1": "55"}}, {"t": "d) How long is a complete trip? __B1__ h", "a": {"B1": "2"}}, {"t": "e) You must reach the Lake by 10:20. What is the latest bus you can take? __B1__", "a": {"B1": "B"}}], "sol": "a) 3\nb) 09:40 (Bus C)\nc) 09:30 to 10:25 = 55 min\nd) 09:00 to 11:00 = 2 h\ne) Bus A (9:55) and Bus B (10:15) arrive in time; the latest is Bus B", "fig": "<div class=\"ttw\"><table class=\"tt\"><tr><th>Stop</th><th>Bus A</th><th>Bus B</th><th>Bus C</th></tr><tr><td>Railway Station</td><td>09:00</td><td>09:20</td><td>09:40</td></tr><tr><td>Museum</td><td>09:12</td><td>09:32</td><td>09:52</td></tr><tr><td>Zoo</td><td>09:30</td><td>09:50</td><td>10:10</td></tr><tr><td>Lake</td><td>09:55</td><td>10:15</td><td>10:35</td></tr><tr><td>Fort</td><td>10:25</td><td>10:45</td><td>11:05</td></tr><tr><td>Railway Station</td><td>11:00</td><td>11:20</td><td>11:40</td></tr></table></div>"}, {"kind": "blank", "p": "A TV guide:", "tag": "", "marks": "", "flat": [{"t": "a) At what time does Kids Quiz start (12-hour time)? __B1__", "a": {"B1": "5:15 pm"}, "expr": "time"}, {"t": "b) Which programme starts at 6:30 pm? __B1__", "a": {"B1": "Cricket Live"}}, {"t": "c) How long is the News? __B1__ min", "a": {"B1": "30"}}, {"t": "d) How long is Cricket Live? __B1__ h __B2__ min", "a": {"B1": "2", "B2": "30"}}, {"t": "e) Ravi missed the last 40 minutes of Movie Night. At what time did he go to bed? __B1__", "a": {"B1": "10:30 pm"}, "expr": "time"}], "sol": "a) 17:15 = 5:15 pm\nb) 18:30\nc) 18:00 to 18:30\nd) 18:30 to 21:00\ne) Movie Night ends 23:10; 40 min earlier is 22:30 = 10:30 pm", "fig": "<div class=\"ttw\"><table class=\"tt\"><tr><th>Time</th><th>Programme</th></tr><tr><td>16:00</td><td>Cartoon Club</td></tr><tr><td>16:30</td><td>Science Quest</td></tr><tr><td>17:15</td><td>Kids Quiz</td></tr><tr><td>18:00</td><td>News</td></tr><tr><td>18:30</td><td>Cricket Live</td></tr><tr><td>21:00</td><td>Movie Night</td></tr><tr><td>23:10</td><td>Late News</td></tr></table></div>"}]}, {"id": "s7", "label": "Review 11A", "sub": "Review set 11A", "slides": [{"kind": "blank", "p": "Convert:", "tag": "", "marks": "", "flat": [{"t": "a) 12 hours = __B1__ minutes", "a": {"B1": "720"}}, {"t": "b) 4 minutes = __B1__ seconds", "a": {"B1": "240"}}, {"t": "c) 72 hours = __B1__ days", "a": {"B1": "3"}}], "sol": "a) 12 × 60\nb) 4 × 60\nc) 72 ÷ 24"}, {"kind": "blank", "p": "Write 168 minutes in hours and minutes:", "tag": "", "marks": "", "flat": [{"t": "__B1__ h __B2__ min", "a": {"B1": "2", "B2": "48"}}], "sol": "168 ÷ 60 = 2 r 48"}, {"kind": "blank", "p": "Is each year a leap year? (yes/no)", "tag": "", "marks": "", "flat": [{"t": "a) 1986 → __B1__", "a": {"B1": "no"}}, {"t": "b) 2052 → __B1__", "a": {"B1": "yes"}}, {"t": "c) 2300 → __B1__", "a": {"B1": "no"}}], "sol": "a) not divisible by 4\nb) divisible by 4\nc) century not divisible by 400"}, {"kind": "blank", "p": "Sunscreen is applied at 9:40 am and lasts 2 hours 30 minutes. When must it be reapplied?", "tag": "", "marks": "", "flat": [{"t": "__B1__", "a": {"B1": "12:10 pm"}, "expr": "time"}], "sol": "9:40 am + 2 h 30 min = 12:10 pm"}, {"kind": "blank", "p": "Write in 12-hour time:", "tag": "", "marks": "", "flat": [{"t": "a) 04:15 → __B1__", "a": {"B1": "4:15 am"}, "expr": "time"}, {"t": "b) 13:00 → __B1__", "a": {"B1": "1:00 pm"}, "expr": "time"}, {"t": "c) 23:35 → __B1__", "a": {"B1": "11:35 pm"}, "expr": "time"}], "sol": "a) 4:15 am\nb) 1:00 pm\nc) 11:35 pm"}, {"kind": "blank", "p": "A play starts at 8:20 pm. Sunita arrives when the clock reads 19:57.", "tag": "", "marks": "", "flat": [{"t": "a) 19:57 in 12-hour time: __B1__", "a": {"B1": "7:57 pm"}, "expr": "time"}, {"t": "b) Minutes until the play begins: __B1__", "a": {"B1": "23"}}, {"t": "c) The play lasts 135 minutes. In hours and minutes: __B1__ h __B2__ min", "a": {"B1": "2", "B2": "15"}}, {"t": "d) When does it finish? __B1__", "a": {"B1": "10:35 pm"}, "expr": "time"}], "sol": "a) 7:57 pm\nb) 8:20 − 7:57 = 23 min\nc) 2 h 15 min\nd) 8:20 pm + 2 h 15 min = 10:35 pm"}]}, {"id": "s8", "label": "Review 11B", "sub": "Review set 11B", "slides": [{"kind": "blank", "p": "Find the time:", "tag": "", "marks": "", "flat": [{"t": "a) 6 hours after 10 am → __B1__", "a": {"B1": "4:00 pm"}, "expr": "time"}, {"t": "b) 3 hours 21 minutes before 8 pm → __B1__", "a": {"B1": "4:39 pm"}, "expr": "time"}], "sol": "a) 4:00 pm\nb) 4:39 pm"}, {"kind": "blank", "p": "Find the time difference between 11:17 am and 2:56 pm:", "tag": "", "marks": "", "flat": [{"t": "__B1__ h __B2__ min", "a": {"B1": "3", "B2": "39"}}], "sol": "11:17 → 2:17 pm is 3 h; → 2:56 is 39 min"}, {"kind": "blank", "p": "Find the number of:", "tag": "", "marks": "", "flat": [{"t": "a) hours in September: __B1__", "a": {"B1": "720"}}, {"t": "b) days in 2028: __B1__", "a": {"B1": "366"}}], "sol": "a) 30 × 24\nb) 2028 is a leap year"}, {"kind": "blank", "p": "A cake bakes for 75 minutes. It goes in at 3:57 pm. When should it come out?", "tag": "", "marks": "", "flat": [{"t": "__B1__", "a": {"B1": "5:12 pm"}, "expr": "time"}], "sol": "3:57 + 1 h 15 min = 5:12 pm"}, {"kind": "blank", "p": "Write in 24-hour time:", "tag": "", "marks": "", "flat": [{"t": "a) 12:32 am → __B1__", "a": {"B1": "00:32"}, "expr": "time"}, {"t": "b) 10:15 am → __B1__", "a": {"B1": "10:15"}, "expr": "time"}, {"t": "c) 5:49 pm → __B1__", "a": {"B1": "17:49"}, "expr": "time"}], "sol": "a) 00:32\nb) 10:15\nc) 17:49"}, {"kind": "blank", "p": "Find the number of days from July 7th to October 22nd.", "tag": "", "marks": "", "flat": [{"t": "__B1__", "a": {"B1": "107"}}], "sol": "24 + 31 + 30 + 22 = 107"}, {"kind": "blank", "p": "Rahul jogged from 7:26 am until 9:15 am. For how long did he jog?", "tag": "", "marks": "", "flat": [{"t": "__B1__ h __B2__ min", "a": {"B1": "1", "B2": "49"}}], "sol": "7:26 → 8:26 is 1 h; → 9:15 is 49 min"}]}];
/* ================= build slide lists ================= */
var SLIDES = {}; SECTIONS.forEach(function(sec){ SLIDES[sec.id]=sec.slides; });
var TAB_DEFS = SECTIONS.map(function(sec){ return {id:sec.id, label:sec.label, sub:sec.sub}; });

/* ================= state ================= */
function blankItem(slide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    return {status:'unanswered', attempts:0, choice:undefined};
  }
  return {status:'unanswered', curStep:0, stepStates: slide.flat.map(function(){ return {status:'unanswered', attempts:0, inputs:{}}; })};
}
function defaultState(){
  var s={tabs:{}};
  TAB_DEFS.forEach(function(td){
    s.tabs[td.id] = { idx:0, maxReached:0, items: SLIDES[td.id].map(function(sl){ return blankItem(sl); }) };
  });
  return s;
}
var appState = {mode:null, learning:null, quiz:null};
var state = null;      // alias for appState[appState.mode]
var MODE = null;
var activeTab=TAB_DEFS[0].id;

function setMode(m){
  appState.mode = m;
  if(!appState[m]) appState[m] = defaultState();
  state = appState[m];
  MODE = m;
}
/* ================= student accounts (saved on this device) ================= */
var SHEET_KEY='sopaan-g6-ch11';
var ACC_KEY='sopaan-students-v1';
var storageOK=true;
var MEM={};
function lsGet(k){ var r=null; try{ r=localStorage.getItem(k); }catch(e){ storageOK=false; }
  if(r===null||r===undefined) r=MEM[k]||null; try{ return r?JSON.parse(r):null; }catch(e){ return null; } }
function lsSet(k,v){ var j=JSON.stringify(v); MEM[k]=j; try{ localStorage.setItem(k,j); return true; }catch(e){ storageOK=false; return false; } }
try{ localStorage.setItem('sopaan-probe','1'); localStorage.removeItem('sopaan-probe'); }catch(e){ storageOK=false; }
function hashPin(pin,salt){ var h=2166136261, str=salt+'|'+pin; for(var i=0;i<str.length;i++){ h^=str.charCodeAt(i); h=Math.imul(h,16777619)>>>0; } return h.toString(36); }
function accKey(name,roll){ return (name.trim().toLowerCase().replace(/\s+/g,' ')+'#'+roll.trim().toLowerCase()); }
function accounts(){ return lsGet(ACC_KEY)||{students:{}}; }
var student=null; // {key,name,roll}
var records=[];   // finished-tab history for this student on this sheet
function progKey(){ return SHEET_KEY+'::'+student.key; }

function loadState(){
  appState = {mode:null, learning:null, quiz:null}; records=[]; activeTab=TAB_DEFS[0].id;
  var saved=lsGet(progKey());
  if(!saved) return;
  try{
    ['learning','quiz'].forEach(function(m){
      if(saved[m] && saved[m].tabs){
        var fresh = defaultState();
        TAB_DEFS.forEach(function(td){
          if(saved[m].tabs[td.id] && saved[m].tabs[td.id].items && saved[m].tabs[td.id].items.length===SLIDES[td.id].length){
            fresh.tabs[td.id] = saved[m].tabs[td.id];
          }
        });
        appState[m] = fresh;
      }
    });
    if(saved.mode==='learning' || saved.mode==='quiz') appState.mode = saved.mode;
    if(saved.activeTab && TAB_DEFS.some(function(t){ return t.id===saved.activeTab; })) activeTab = saved.activeTab;
    if(Array.isArray(saved.records)) records = saved.records;
  }catch(e){}
}
function saveState(){
  if(!student) return;
  lsSet(progKey(), {mode:appState.mode, learning:appState.learning, quiz:appState.quiz, activeTab:activeTab, records:records, updated:Date.now()});
  var acc=accounts(); if(acc.students[student.key]){ acc.students[student.key].last=Date.now(); lsSet(ACC_KEY,acc); }
}
function addRecord(mode, tabId, correct, revealed, skipped, total){
  records.unshift({at:Date.now(), mode:mode, tab:tabId, correct:correct, revealed:revealed, skipped:skipped, total:total});
  if(records.length>60) records.length=60;
  saveState();
}
function fmtDate(ms){ try{ return new Date(ms).toLocaleString(undefined,{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'}); }catch(e){ return ''; } }

function renderWho(){
  var el=document.getElementById('whoBar');
  if(!student){ el.hidden=true; el.innerHTML=''; return; }
  el.hidden=false;
  el.innerHTML='Signed in as <b>'+esc(student.name)+'</b> · Roll '+esc(student.roll)+
    ' <button id="btnRecord">My record</button> <button id="btnSignOut">Sign out</button>';
  document.getElementById('btnRecord').addEventListener('click', renderRecord);
  document.getElementById('btnSignOut').addEventListener('click', signOut);
}
function signOut(){
  saveState(); student=null; state=null; MODE=null;
  var acc=accounts(); delete acc.current; lsSet(ACC_KEY,acc);
  document.getElementById('modePill').hidden=true;
  renderWho(); renderLogin();
}
function signIn(key){
  var acc=accounts(); var st=acc.students[key]; if(!st) return;
  student={key:key, name:st.name, roll:st.roll};
  acc.current=key; st.last=Date.now(); lsSet(ACC_KEY,acc);
  loadState(); renderWho();
  if(appState.mode==='learning' || appState.mode==='quiz'){
    setMode(appState.mode); document.getElementById('modePill').hidden=false; updateModePill();
    showChrome(true); buildTabbar(); renderSlide();
    showToast('Welcome back, '+st.name.split(' ')[0]+'. Picking up where you left off.');
  } else {
    renderModePicker();
  }
}
function renderLogin(msg){
  showChrome(false);
  var acc=accounts(); var keys=Object.keys(acc.students).sort(function(a,b){ return (acc.students[b].last||0)-(acc.students[a].last||0); });
  var h='<div class="login-card"><h2>Student sign-in</h2>'+
    '<p class="lead">Sign in to save your answers, see your record and continue where you left off next time.</p>';
  if(!storageOK) h+='<div class="login-err">This browser is blocking saved data (for example, a private window). You can still practise, but progress will not be kept after you close the page.</div>';
  if(msg) h+='<div class="login-err">'+esc(msg)+'</div>';
  if(keys.length){
    h+='<div class="known"><span class="known-label">Continue as</span>';
    keys.slice(0,6).forEach(function(k){ var st=acc.students[k];
      h+='<button class="known-btn" data-k="'+esc(k)+'"><span>'+esc(st.name)+' <small>· Roll '+esc(st.roll)+'</small></span><small>'+(st.last?'Last active '+fmtDate(st.last):'')+'</small></button>'; });
    h+='</div>';
  }
  h+='<form id="loginForm" novalidate>'+
    '<div class="fld"><label for="lgName">Full name</label><input id="lgName" autocomplete="name" required></div>'+
    '<div class="fld-row"><div class="fld"><label for="lgRoll">Roll no.</label><input id="lgRoll" required></div>'+
    '<div class="fld"><label for="lgPin">4-digit PIN</label><input id="lgPin" type="password" inputmode="numeric" maxlength="4" autocomplete="off" required></div></div>'+
    '<button class="btn btn-primary" type="submit" style="width:100%;">Sign in</button>'+
    '<p class="login-note">New here? Enter your name, roll no. and a PIN you will remember, and your profile is created. Progress is saved on this device, so use the same device and browser to continue.</p>'+
    '</form></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  wrap.querySelectorAll('.known-btn').forEach(function(b){
    b.addEventListener('click', function(){
      var st=accounts().students[b.dataset.k];
      document.getElementById('lgName').value=st.name; document.getElementById('lgRoll').value=st.roll;
      document.getElementById('lgPin').focus();
    });
  });
  document.getElementById('loginForm').addEventListener('submit', function(e){
    e.preventDefault();
    var name=document.getElementById('lgName').value.trim(), roll=document.getElementById('lgRoll').value.trim(), pin=document.getElementById('lgPin').value.trim();
    if(!name||!roll){ renderLoginErr('Enter your name and roll no.'); return; }
    if(!/^\d{4}$/.test(pin)){ renderLoginErr('Your PIN must be exactly 4 digits.'); return; }
    var k=accKey(name,roll); var acc=accounts();
    if(acc.students[k]){
      if(acc.students[k].pin!==hashPin(pin,k)){ renderLoginErr('That PIN does not match this name and roll no. Try again.'); return; }
    } else {
      acc.students[k]={name:name.replace(/\s+/g,' '), roll:roll, pin:hashPin(pin,k), created:Date.now()};
      lsSet(ACC_KEY,acc);
    }
    signIn(k);
  });
}
function renderLoginErr(m){
  var n=document.getElementById('lgName').value, r=document.getElementById('lgRoll').value;
  renderLogin(m); document.getElementById('lgName').value=n; document.getElementById('lgRoll').value=r; document.getElementById('lgPin').focus();
}
function tabSummary(m){
  var st=appState[m]; if(!st) return null;
  return TAB_DEFS.map(function(td){
    var items=st.tabs[td.id].items, n=items.length;
    var c=items.filter(function(i){return i.status==='correct';}).length;
    var done=items.filter(function(i){return i.status!=='unanswered';}).length;
    return {label:td.label, n:n, done:done, correct:c};
  });
}
function renderRecord(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+' · Time</p>';
  ['learning','quiz'].forEach(function(m){
    var sum=tabSummary(m);
    h+='<h3>'+(m==='learning'?'📘 Learning Sheet':'📝 Quiz Mode')+'</h3>';
    if(!sum){ h+='<p class="rec-empty">Not started yet.</p>'; return; }
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>Section</th><th>Progress</th><th>Correct first time</th></tr></thead><tbody>';
    sum.forEach(function(r){ var pct=Math.round(r.done/r.n*100);
      h+='<tr><td>'+r.label+'</td><td><span class="rec-bar"><i style="width:'+pct+'%"></i></span>'+r.done+' / '+r.n+'</td><td>'+(m==='quiz'?'—':r.correct+' / '+r.n)+'</td></tr>'; });
    h+='</tbody></table></div>';
  });
  h+='</div><div class="rec-card"><h3>Finished sections</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sections finished yet. Each time you finish a tab, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>When</th><th>Mode</th><th>Section</th><th>Score</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+(r.mode==='learning'?' <span class="rec-empty">('+r.revealed+' revealed, '+r.skipped+' skipped)</span>':'')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){
    if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker();
  });
  window.scrollTo({top:0});
}

/* ================= tab bar ================= */
function buildTabbar(){
  var el=document.getElementById('tabbar');
  el.innerHTML = TAB_DEFS.map(function(t){
    return '<button class="tab-btn'+(t.id===activeTab?' active':'')+'" data-tab="'+t.id+'">'+t.label+'<span class="tab-count">'+SLIDES[t.id].length+'</span></button>';
  }).join('');
  el.querySelectorAll('.tab-btn').forEach(function(btn){
    btn.addEventListener('click', function(){ activeTab=btn.dataset.tab; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  });
}

/* ================= rendering ================= */
function canProceed(item){ return item.status==='correct'||item.status==='revealed'||item.status==='skipped'; }

function renderSlide(){
  if(!state.tabs[activeTab]){ activeTab=TAB_DEFS[0].id; }
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  if(ts.idx>=slides.length||ts.idx<0) ts.idx=0;
  var idx = ts.idx;
  var slide = slides[idx];
  var item = ts.items[idx];

  var tdef=TAB_DEFS.find(function(t){return t.id===activeTab;});
  document.getElementById('spLabel').textContent = tdef.label+' · Question '+(idx+1)+' of '+slides.length;
  document.getElementById('secSub').textContent = tdef.label+' — '+tdef.sub;
  document.getElementById('spFill').style.width = Math.round(((idx)/(Math.max(slides.length-1,1)))*100)+'%';

  var h='<div class="qcard">';
  if(slide.kind==='mcq' || slide.kind==='ar'){
    h += renderChoiceBody(slide, item, idx);
  } else {
    h += renderBlankBody(slide, item, idx);
  }
  h += '<div class="feedback" id="feedbackBox"></div>';
  if(MODE==='learning' && (item.status==='correct'||item.status==='revealed')) h += solutionHTML(slide);
  h += '</div>';

  document.getElementById('wrap').innerHTML = h;
  wireSlideEvents(slide, item, idx);
  restoreFeedback(item);
  renderNavbar(item);
  updateFab();
  saveState();
}

function solutionHTML(slide){
  if(!slide.sol) return '';
  return '<div class="solution"><div class="sol-h">Solution</div>'+slide.sol.split('\n').map(function(l){ return '<div class="sol-line">'+fr(esc(l))+'</div>'; }).join('')+'</div>';
}
var LETTERS=['a','b','c','d'];
function chosenHTML(slide,item){
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(item.choice===undefined) return '';
  var ok=item.choice===slide.correct;
  var h='<div class="chosen '+(ok?'ok':'bad')+'"><b>Your answer:</b> ('+LETTERS[item.choice]+') '+fr(esc(opts[item.choice]))+(ok?' ✓':' ✗')+'</div>';
  if(!ok) h+='<div class="chosen ok"><b>Correct answer:</b> ('+LETTERS[slide.correct]+') '+fr(esc(opts[slide.correct]))+'</div>';
  return h;
}
function renderChoiceBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div>';
  if(slide.kind==='mcq'){
    h += '<div class="qtext">'+fr(esc(slide.text))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  } else {
    h += '<div class="qtext"><span class="qtag" style="margin-left:0;margin-right:6px;">A / R</span>Assertion (A): '+fr(esc(slide.a))+'<br>Reason (R): '+fr(esc(slide.r))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  }
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(MODE==='quiz') h += '<div class="quiz-hint">Quiz mode — pick an option. The correct answer is revealed once you finish this tab.</div>';
  var locked = MODE==='learning' && (item.status==='correct' || item.status==='revealed');
  h += '<div class="options">';
  opts.forEach(function(opt,i){
    var cls='opt';
    if(locked){
      if(i===slide.correct) cls+=' is-correct';
      else if(item.choice===i) cls+=' is-wrong';
      cls+=' locked';
    }
    if(item.choice===i) cls+=' is-chosen';
    h += '<label class="'+cls+'"><input type="radio" name="choice" value="'+i+'" '+(item.choice===i?'checked':'')+' '+(locked?'disabled':'')+'> <span class="opt-l">('+LETTERS[i]+')</span> <span class="opt-t">'+fr(esc(opt))+'</span>'+(item.choice===i?'<span class="opt-tag">'+(locked?(i===slide.correct?'Your answer ✓':'Your answer ✗'):'Selected')+'</span>':'')+'</label>';
  });
  h += '</div>';
  if(locked) h += chosenHTML(slide,item);
  return h;
}

function renderBlankBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div><div class="qtext">';
  if(slide.kind==='case'){ h += '<b>'+esc(slide.title)+'.</b> '+esc(slide.body); }
  else { h += fr(esc(slide.p)); }
  h += (slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  if(slide.marks) h += '<div class="marks-pill">'+slide.marks+'</div>';
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';

  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  var blankCount=0; slide.flat.forEach(function(s){ blankCount+=Object.keys(s.a).length; });

  if(MODE==='quiz'){
    h += '<div class="step-badge">'+blankCount+' blank'+(blankCount===1?'':'s')+' in this question</div>';
    h += '<div class="quiz-hint">Quiz mode — fill in what you can. Correct answers are revealed once you finish this tab.</div>';
    if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
    if(hasExpr) h += '<div class="quiz-hint">Type expressions like <b>(P-2w)/2</b>, <b>2A/b</b> or <b>V/(pi*r^2)</b>. Use ^ for powers and pi for π. Any equivalent form is accepted.</div>';
    h += '<div class="steps">';
    for(var qi=0; qi<total; qi++){
      var qstep = slide.flat[qi];
      var qss = item.stepStates[qi];
      if(qstep.partLabel) h += '<div class="subpart-label">'+esc(qstep.partLabel)+'</div>';
      if(qstep.orDivider) h += '<div class="or-divider">OR</div>';
      var qline = fr(qstep.t);
      Object.keys(qstep.a).forEach(function(bkey){
        var val = qss.inputs[bkey]||'';
        var inp='<input class="blank-input'+(['fv','fe','fl','fm','fi','dec'].indexOf(qstep.expr)>=0?' fr':(qstep.expr==='flist'||qstep.expr==='dlist')?' wide':qstep.expr===true?' expr':(qstep.expr==='words'||qstep.expr==='list'||qstep.expr==='expanded'||qstep.expr==='set'||qstep.expr==='primes'?' wide':''))+'" data-step="'+qi+'" data-bkey="'+bkey+'" value="'+esc(val)+'">';
        qline = qline.replace('__'+bkey+'__', inp);
      });
      if(qstep.fig) h += '<div class="fig">'+qstep.fig+'</div>';
      h += '<div class="step-line">'+qline+'</div>';
    }
    h += '</div>';
    return h;
  }

  if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
  if(hasExpr) h += '<div class="quiz-hint">Type expressions like <b>(P-2w)/2</b>, <b>2A/b</b> or <b>V/(pi*r^2)</b>. Use ^ for powers and pi for π. Any equivalent form is accepted.</div>';
  var locked = item.status==='correct' || item.status==='revealed';
  var upto = locked ? total-1 : item.curStep;
  h += '<div class="step-badge">Step '+(Math.min(item.curStep,total-1)+1)+' of '+total+'</div>';
  h += '<div class="steps">';
  for(var i=0;i<=upto;i++){
    var step = slide.flat[i];
    var ss = item.stepStates[i];
    if(step.partLabel) h += '<div class="subpart-label">'+esc(step.partLabel)+'</div>';
    if(step.orDivider) h += '<div class="or-divider">OR</div>';
    var resolved = ss.status==='correct' || ss.status==='revealed';
    var line = fr(step.t);
    Object.keys(step.a).forEach(function(bkey){
      var fs = ss.inputs['fs_'+bkey];
      var cls = fs==='correct'?'is-correct':(fs==='wrong'?'is-wrong':'');
      var val = ss.inputs[bkey]||'';
      var dis = resolved ? 'disabled':'';
      var inp='<input class="blank-input '+cls+(['fv','fe','fl','fm','fi','dec'].indexOf(step.expr)>=0?' fr':(step.expr==='flist'||step.expr==='dlist')?' wide':step.expr===true?' expr':(step.expr==='words'||step.expr==='list'||step.expr==='expanded'||step.expr==='set'||step.expr==='primes'?' wide':''))+'" data-step="'+i+'" data-bkey="'+bkey+'" value="'+esc(val)+'" '+dis+'>';
      line = line.replace('__'+bkey+'__', inp);
    });
    if(step.fig) h += '<div class="fig">'+step.fig+'</div>';
    h += '<div class="step-line'+(resolved?' resolved':'')+'">'+line+'</div>';
    if(ss.status==='revealed'){
      var reveals=[];
      Object.keys(step.a).forEach(function(bkey){ reveals.push(bkey+' = '+esc(step.a[bkey])); });
      h += '<div class="reveal-note">correct: '+reveals.join(', ')+'</div>';
    }
  }
  h += '</div>';
  return h;
}

var __flash=null;
function restoreFeedback(item){
  var fb=document.getElementById('feedbackBox'); if(!fb) return;
  if(__flash){ fb.className='feedback show '+__flash.c; fb.innerHTML=__flash.h; __flash=null; return; }
  if(MODE==='quiz'){ fb.className='feedback'; fb.innerHTML=''; return; }
  if(item.status==='correct'){ fb.className='feedback show ok'; fb.innerHTML='<b>All done — correct!</b>'; }
  else if(item.status==='revealed'){ fb.className='feedback show reveal'; fb.innerHTML='<b>Answer revealed above.</b> Move on whenever you’re ready.'; }
  else if(item.status==='skipped'){ fb.className='feedback show retry'; fb.innerHTML='Skipped — revisit it anytime from the Question Palette.'; }
  else { fb.className='feedback'; fb.innerHTML=''; }
}

function slideIsAnswered(slide,item){
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return item.stepStates.some(function(ss){ return Object.keys(ss.inputs).some(function(k){ return k.indexOf('fs_')!==0 && ss.inputs[k] && String(ss.inputs[k]).trim()!==''; }); });
}
function renderNavbar(item){
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  var slide = slides[ts.idx];
  var isLast = ts.idx === slides.length-1;
  var h='';
  h += '<button class="btn" id="btnPrev" '+(ts.idx===0?'disabled':'')+'>&larr; Previous</button>';

  if(MODE==='quiz'){
    h += '<button class="btn" id="btnSkip">Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnNext">'+(isLast?'Finish':'Next →')+'</button>';
  } else {
    h += '<button class="btn" id="btnSkip" '+(item.status!=='unanswered'?'disabled':'')+'>Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnCheck" '+(item.status!=='unanswered'?'disabled':'')+'>Check</button>';
    h += '<button class="btn btn-primary" id="btnNext" '+(canProceed(item)?'':'disabled')+'>'+(isLast?'Finish':'Next →')+'</button>';
  }
  document.getElementById('navbarInner').innerHTML = h;

  document.getElementById('btnPrev').addEventListener('click', function(){ if(ts.idx>0){ ts.idx--; renderSlide(); } });

  if(MODE==='quiz'){
    document.getElementById('btnSkip').addEventListener('click', function(){
      item.status='skipped';
      advanceQuiz(ts, slides);
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      item.status = slideIsAnswered(slide,item) ? 'answered' : 'unanswered';
      advanceQuiz(ts, slides);
    });
  } else {
    document.getElementById('btnSkip').addEventListener('click', function(){
      if(item.status==='unanswered'){ item.status='skipped'; renderSlide(); }
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      if(!canProceed(item)) return;
      if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
      else { renderFinished(); }
    });
    document.getElementById('btnCheck').addEventListener('click', function(){ handleCheck(); });
  }
}
function advanceQuiz(ts, slides){
  if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
  else { renderFinished(); }
}

function wireSlideEvents(slide, item, idx){
  document.querySelectorAll('input[type="radio"][name="choice"]').forEach(function(r){
    r.addEventListener('change', function(){ item.choice=parseInt(r.value,10); saveState();
      document.querySelectorAll('.opt').forEach(function(l){ l.classList.remove('is-chosen'); var t=l.querySelector('.opt-tag'); if(t) t.remove(); });
      var lab=r.closest('.opt'); lab.classList.add('is-chosen'); var tg=document.createElement('span'); tg.className='opt-tag'; tg.textContent='Selected'; lab.appendChild(tg); });
  });
  document.querySelectorAll('.blank-input').forEach(function(inp){
    inp.addEventListener('input', function(){
      var si=parseInt(inp.dataset.step,10), bk=inp.dataset.bkey;
      item.stepStates[si].inputs[bk]=inp.value;
      saveState();
    });
  });
}

function handleCheck(){
  var ts = state.tabs[activeTab];
  var slide = SLIDES[activeTab][ts.idx];
  var item = ts.items[ts.idx];
  var fb = document.getElementById('feedbackBox');

  if(slide.kind==='mcq' || slide.kind==='ar'){
    if(item.choice===undefined){ fb.className='feedback show err'; fb.innerHTML='Please choose an option first.'; return; }
    var ok = item.choice===slide.correct;
    if(ok){
      item.status='correct'; playSuccess();
      fb.className='feedback show ok'; fb.innerHTML='<b>Correct!</b>';
    } else {
      item.attempts=(item.attempts||0)+1;
      if(item.attempts>=2){ item.status='revealed'; playReveal(); }
      else { playWrong(); fb.className='feedback show retry'; fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'}; }
    }
    renderSlide();
    return;
  }

  // blank / case
  var step = slide.flat[item.curStep];
  var ss = item.stepStates[item.curStep];
  var blanks = Object.keys(step.a);
  var missing = blanks.some(function(k){ return !ss.inputs[k] || String(ss.inputs[k]).trim()===''; });
  if(missing){ fb.className='feedback show err'; fb.innerHTML='Fill in every blank in this step before checking.'; return; }

  var allGood=true;
  blanks.forEach(function(k){
    var good=answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr);
    ss.inputs['fs_'+k]=good?'correct':'wrong';
    if(!good) allGood=false;
  });

  if(allGood){
    ss.status='correct'; playSuccess();
    advanceStepOrFinish(item, slide);
  } else {
    ss.attempts=(ss.attempts||0)+1;
    if(ss.attempts>=2){
      ss.status='revealed'; playReveal();
      advanceStepOrFinish(item, slide);
    } else {
      playWrong();
      fb.className='feedback show retry';
      fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'};
      renderSlide();
      return;
    }
  }
  renderSlide();
}

function advanceStepOrFinish(item, slide){
  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  if(item.curStep < total-1){
    item.curStep++;
  } else {
    var anyRevealed = item.stepStates.some(function(ss){ return ss.status==='revealed'; });
    item.status = anyRevealed ? 'revealed' : 'correct';
  }
}

/* ================= palette ================= */
var overlay=document.getElementById('overlay');
function statusOf(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  return ts.items[i].status==='unanswered' ? 'locked' : ts.items[i].status;
}
function buildPalette(){
  var slides=SLIDES[activeTab];
  document.getElementById('paletteTitle').textContent = TAB_DEFS.find(function(t){return t.id===activeTab;}).label+' · Question palette';
  var body=document.getElementById('paletteBody');
  var html='';
  for(var i=0;i<slides.length;i++){
    html += '<div class="chip" data-status="'+statusOf(activeTab,i)+'" data-idx="'+i+'">'+(i+1)+'</div>';
  }
  body.innerHTML = html;
  body.querySelectorAll('.chip').forEach(function(chip){
    chip.addEventListener('click', function(){
      var i=parseInt(chip.dataset.idx,10);
      var ts=state.tabs[activeTab];
      if(i>ts.maxReached){ showToast('Finish the earlier questions to unlock this one.'); return; }
      ts.idx=i; closePalette(); renderSlide();
    });
  });
}
function openPalette(){ buildPalette(); overlay.classList.add('show'); }
function closePalette(){ overlay.classList.remove('show'); }
var toastTimer;
function showToast(msg){
  var t=document.getElementById('toast'); t.textContent=msg; t.classList.add('show');
  clearTimeout(toastTimer); toastTimer=setTimeout(function(){ t.classList.remove('show'); },2200);
}
document.getElementById('paletteFab').addEventListener('click', openPalette);
document.getElementById('paletteClose').addEventListener('click', closePalette);
overlay.addEventListener('click', function(e){ if(e.target===overlay) closePalette(); });

function updateFab(){
  var slides=SLIDES[activeTab];
  var done=state.tabs[activeTab].items.filter(function(it){ return it.status==='correct'||it.status==='revealed'||it.status==='skipped'; }).length;
  document.getElementById('fabBadge').textContent = done+'/'+slides.length;
}

/* ================= overall progress + finish ================= */
function updateChapterProgress(){
  var total=0, done=0;
  TAB_DEFS.forEach(function(td){
    state.tabs[td.id].items.forEach(function(it){
      total++;
      if(it.status==='correct'||it.status==='revealed'||it.status==='skipped') done++;
    });
  });
  var pct = total>0 ? Math.round((done/total)*100) : 0;
  document.getElementById('cpFill').style.width=pct+'%';
  document.getElementById('cpLabel').textContent=pct+'% complete';
}
function isSlideCorrect(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice===slide.correct;
  return slide.flat.every(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).every(function(k){ return answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr); });
  });
}
function isSlideAttempted(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return slide.flat.some(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).some(function(k){ return ss.inputs[k] && String(ss.inputs[k]).trim()!==''; });
  });
}
function slideLabel(slide){
  var t = slide.kind==='case' ? slide.title : (slide.kind==='ar' ? slide.a : (slide.p||slide.text||''));
  t = String(t);
  return t.length>90 ? t.slice(0,90)+'…' : t;
}
function slideAnswerText(slide, item, correctSide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
    if(correctSide) return '('+LETTERS[slide.correct]+') '+opts[slide.correct];
    return item.choice!==undefined ? '('+LETTERS[item.choice]+') '+opts[item.choice] : '— not attempted —';
  }
  return slide.flat.map(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).map(function(k){
      return correctSide ? step.a[k] : (ss.inputs[k] || '—');
    }).join(', ');
  }).join('  |  ');
}

function renderFinished(){
  if(MODE==='quiz'){ renderQuizResults(); return; }
  var ts=state.tabs[activeTab];
  var correct=ts.items.filter(function(i){return i.status==='correct';}).length;
  var revealed=ts.items.filter(function(i){return i.status==='revealed';}).length;
  var skipped=ts.items.filter(function(i){return i.status==='skipped';}).length;
  var h='<div class="qcard done-card"><div class="big">✨</div><h2>Tab complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">You worked through all '+ts.items.length+' questions in this tab.</p>';
  if(!ts.recorded){ ts.recorded=true; addRecord('learning', activeTab, correct, revealed, skipped, ts.items.length); }
  h+='<div class="score-pills">'+
     '<span class="score-pill" style="background:var(--success-soft);color:var(--success);">'+correct+' correct</span>'+
     '<span class="score-pill" style="background:var(--danger-soft);color:var(--danger);">'+revealed+' revealed</span>'+
     '<span class="score-pill" style="background:var(--gold-soft);color:var(--retry-text);">'+skipped+' skipped</span></div>'+
     '<button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; ts.recorded=false; renderSlide(); });
  updateChapterProgress(); saveState();
}

function renderQuizResults(){
  var ts=state.tabs[activeTab];
  var slides=SLIDES[activeTab];
  var correctCount=0, attemptedCount=0;
  var rowsHtml = slides.map(function(slide,i){
    var item=ts.items[i];
    var ok=isSlideCorrect(activeTab,i);
    var att=isSlideAttempted(activeTab,i);
    if(ok) correctCount++;
    if(att) attemptedCount++;
    var tagCls = ok?'ok':(att?'bad':'na');
    var tagText = ok?'Correct':(att?'Incorrect':'Not attempted');
    var row='<div class="review-row">';
    row+='<span class="review-tag '+tagCls+'">Q'+(i+1)+' · '+tagText+'</span>';
    row+='<div class="review-q">'+fr(esc(slideLabel(slide)))+'</div>';
    row+='<div class="review-ans"><b>Your answer:</b> '+fr(esc(slideAnswerText(slide,item,false)))+'</div>';
    if(!ok) row+='<div class="review-ans" style="color:var(--success);"><b>Correct answer:</b> '+fr(esc(slideAnswerText(slide,item,true)))+'</div>';
    if(slide.sol) row+='<details class="rev-sol"><summary>Show solution</summary>'+solutionHTML(slide)+'</details>';
    row+='</div>';
    return row;
  }).join('');

  addRecord('quiz', activeTab, correctCount, 0, 0, slides.length);
  var h='<div class="qcard done-card" style="text-align:left;">';
  h+='<div style="text-align:center;"><div class="big">🏁</div><h2>Quiz complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">'+correctCount+' / '+slides.length+' correct · '+attemptedCount+' attempted</p></div>';
  h+='<div style="margin-top:16px;">'+rowsHtml+'</div>';
  h+='<div style="text-align:center;margin-top:6px;"><button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  h+='</div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; renderSlide(); });
  playSuccess();
  updateChapterProgress(); saveState();
}

/* ================= mode picker ================= */
function updateModePill(){
  var btn=document.getElementById('modePill');
  if(!btn) return;
  btn.textContent = MODE==='quiz' ? '📝 Quiz Mode · switch' : '📘 Learning Sheet · switch';
}
function showChrome(show){
  document.querySelector('.tabbar').style.display = show?'':'none';
  document.querySelector('.slide-progress').style.display = show?'':'none';
  document.querySelector('.navbar').style.display = show?'':'none';
  document.getElementById('paletteFab').style.display = show?'':'none';
}
function renderModePicker(){
  showChrome(false);
  var wrap=document.getElementById('wrap');
  wrap.innerHTML =
    '<div class="mode-pick">'+
      '<div class="mode-card" data-pick="learning"><div class="mode-icon">📘</div><h3>Learning Sheet</h3>'+
      '<p>Work through each question step by step with instant feedback — two tries, then the correct value is revealed right there so you can keep moving.</p></div>'+
      '<div class="mode-card" data-pick="quiz"><div class="mode-icon">📝</div><h3>Quiz Mode</h3>'+
      '<p>Attempt every question with no hints along the way. Your score and the full answer key are shown together once you finish the tab — just like the real exam.</p></div>'+
    '</div>';
  wrap.querySelectorAll('[data-pick]').forEach(function(card){
    card.addEventListener('click', function(){
      setMode(card.dataset.pick);
      document.getElementById('modePill').hidden=false;
      updateModePill();
      showChrome(true);
      buildTabbar();
      renderSlide();
    });
  });
}
document.getElementById('modePill').addEventListener('click', function(){
  if(!appState.mode){ return; }
  setMode(appState.mode==='quiz' ? 'learning' : 'quiz');
  updateModePill();
  showChrome(true);
  buildTabbar();
  renderSlide();
});

/* ================= boot ================= */
var _origRenderSlide = renderSlide;
renderSlide = function(){ _origRenderSlide(); updateChapterProgress(); updateModePill(); };

renderLogin();
})();
</script>
</body>
</html>
