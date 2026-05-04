# stete_od_nepogoda

<style>
*{box-sizing:border-box;margin:0;padding:0}
.wrap{font-family:var(--font-sans);max-width:680px;padding:0 0 2rem}

.gov-header{
  background:var(--color-background-primary);
  border-bottom:3px solid #1a3a6b;
  padding:14px 0 12px;
  margin-bottom:0;
}
.gov-stripe{height:4px;background:linear-gradient(90deg,#1a3a6b 0%,#1a3a6b 60%,#c0392b 60%,#c0392b 100%);margin-bottom:12px}
.gov-inner{display:flex;align-items:center;gap:14px;padding:0 20px}
.gov-logo{
  width:44px;height:44px;background:#1a3a6b;border-radius:4px;
  display:flex;align-items:center;justify-content:center;flex-shrink:0;
}
.gov-logo svg{width:26px;height:26px;fill:white}
.gov-title h1{font-size:15px;font-weight:500;color:#1a3a6b;letter-spacing:0.01em;margin-bottom:2px}
.gov-title p{font-size:11px;color:var(--color-text-secondary);letter-spacing:0.02em;text-transform:uppercase}
.gov-badge{
  margin-left:auto;display:flex;align-items:center;gap:6px;
  background:var(--color-background-secondary);
  border:0.5px solid var(--color-border-tertiary);
  border-radius:var(--border-radius-md);
  padding:5px 10px;font-size:11px;color:var(--color-text-secondary);
  font-family:var(--font-mono);
}
.dot-g{width:7px;height:7px;border-radius:50%;background:#27ae60;animation:blink 2s infinite;flex-shrink:0}
.dot-y{width:7px;height:7px;border-radius:50%;background:#f39c12;flex-shrink:0}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}

.nav-bar{
  background:var(--color-background-secondary);
  border-bottom:0.5px solid var(--color-border-tertiary);
  display:flex;padding:0 20px;
}
.nav-tab{
  padding:11px 16px 10px;font-size:12px;font-weight:500;
  letter-spacing:0.03em;text-transform:uppercase;
  cursor:pointer;border:none;background:transparent;
  color:var(--color-text-secondary);
  border-bottom:2px solid transparent;margin-bottom:-0.5px;
  transition:all .15s;font-family:var(--font-sans);
}
.nav-tab.active{color:#1a3a6b;border-bottom-color:#1a3a6b}
.nav-tab:hover:not(.active){color:var(--color-text-primary)}

.body{padding:20px}
.panel{display:none}
.panel.active{display:block}

.stats-row{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:20px}
.stat-card{
  background:var(--color-background-secondary);
  border:0.5px solid var(--color-border-tertiary);
  border-radius:var(--border-radius-md);
  padding:12px 14px;
}
.stat-card.danger{border-left:3px solid #c0392b;border-radius:0 var(--border-radius-md) var(--border-radius-md) 0}
.stat-card.warn{border-left:3px solid #e67e22;border-radius:0 var(--border-radius-md) var(--border-radius-md) 0}
.stat-n{font-size:22px;font-weight:500;color:var(--color-text-primary);font-family:var(--font-mono)}
.stat-l{font-size:10px;color:var(--color-text-secondary);text-transform:uppercase;letter-spacing:0.06em;margin-top:3px}

.form-section{margin-bottom:18px}
.field-label{
  display:block;font-size:11px;font-weight:500;
  text-transform:uppercase;letter-spacing:0.06em;
  color:var(--color-text-secondary);margin-bottom:6px;
}
.required{color:#c0392b;margin-left:2px}
select,input,textarea{
  width:100%;padding:9px 11px;
  border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);
  background:var(--color-background-primary);
  color:var(--color-text-primary);
  font-size:13px;font-family:var(--font-sans);
  transition:border-color .15s,box-shadow .15s;
  -webkit-appearance:none;appearance:none;
}
select{
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='10' height='10' viewBox='0 0 24 24' fill='none' stroke='%23888' stroke-width='2'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");
  background-repeat:no-repeat;background-position:right 11px center;padding-right:30px;
}
textarea{min-height:76px;resize:vertical;line-height:1.5}
input:focus,select:focus,textarea:focus{
  outline:none;border-color:#1a3a6b;
  box-shadow:0 0 0 3px rgba(26,58,107,0.1);
}
input::placeholder,textarea::placeholder{color:var(--color-text-secondary);opacity:.7}

.sev-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:4px}
.sev-opt{
  border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);
  padding:10px 8px;cursor:pointer;text-align:center;
  background:var(--color-background-primary);
  transition:all .15s;font-family:var(--font-sans);
}
.sev-num{font-size:16px;font-weight:500;display:block;font-family:var(--font-mono)}
.sev-name{font-size:10px;color:var(--color-text-secondary);text-transform:uppercase;letter-spacing:0.04em;margin-top:2px;display:block}
.sev-opt[data-s="1"].on{border-color:#e67e22;background:#fef9f0}
.sev-opt[data-s="1"].on .sev-num{color:#c05e00}
.sev-opt[data-s="2"].on{border-color:#e67e22;background:#fef3e2}
.sev-opt[data-s="2"].on .sev-num{color:#a04000}
.sev-opt[data-s="3"].on{border-color:#c0392b;background:#fdf0ef}
.sev-opt[data-s="3"].on .sev-num{color:#921f1f}
.sev-opt[data-s="4"].on{border-color:#921f1f;background:#fbebeb}
.sev-opt[data-s="4"].on .sev-num{color:#6b1515}
.sev-opt:hover:not(.on){border-color:var(--color-border-primary)}

.sev-desc-row{
  display:grid;grid-template-columns:repeat(4,1fr);gap:8px;
  font-size:10px;color:var(--color-text-secondary);
  text-align:center;margin-bottom:16px;letter-spacing:0em;
}

.row2{display:flex;gap:8px}
.row2 input{flex:1}
.btn-sm{
  padding:9px 12px;border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);
  background:var(--color-background-secondary);
  color:var(--color-text-secondary);cursor:pointer;
  font-size:12px;font-family:var(--font-sans);font-weight:500;
  white-space:nowrap;transition:all .15s;
}
.btn-sm:hover{border-color:var(--color-border-primary);color:var(--color-text-primary)}
.btn-sm.active{border-color:#1a3a6b;color:#1a3a6b;background:rgba(26,58,107,.06)}

.acc-pill{
  display:inline-flex;align-items:center;gap:5px;
  font-size:10px;padding:3px 8px;border-radius:var(--border-radius-md);
  font-family:var(--font-mono);margin-top:5px;display:none;
}
.hint-txt{font-size:11px;color:var(--color-text-secondary);margin-top:5px;font-family:var(--font-mono)}

#locMap{
  width:100%;height:200px;border-radius:var(--border-radius-md);
  border:0.5px solid var(--color-border-secondary);
  margin:8px 0 4px;cursor:crosshair;
}
.map-hint{font-size:10px;color:var(--color-text-secondary);text-align:center;margin-bottom:14px;font-family:var(--font-mono);letter-spacing:0.02em}

.img-zone{
  border:0.5px dashed var(--color-border-primary);
  border-radius:var(--border-radius-md);
  padding:18px;text-align:center;cursor:pointer;
  position:relative;background:var(--color-background-secondary);
  transition:all .15s;margin-bottom:16px;
}
.img-zone:hover{border-color:#1a3a6b;background:rgba(26,58,107,.03)}
.img-zone input{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.img-zone-icon{width:20px;height:20px;margin:0 auto 6px;opacity:.4}
.img-zone p{font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono)}
.img-prev-box{width:100%;max-height:110px;object-fit:cover;border-radius:6px;margin-top:8px;display:none}

.divider{height:0.5px;background:var(--color-border-tertiary);margin:18px 0}

.btn-submit{
  width:100%;padding:12px;
  background:#1a3a6b;color:white;
  border:none;border-radius:var(--border-radius-md);
  font-size:13px;font-weight:500;cursor:pointer;
  font-family:var(--font-sans);letter-spacing:0.02em;
  transition:opacity .15s,transform .1s;
}
.btn-submit:hover{opacity:.9;transform:translateY(-1px)}
.btn-submit:active{transform:translateY(0)}

.notice{
  font-size:12px;padding:10px 12px;
  border-radius:var(--border-radius-md);
  font-family:var(--font-mono);margin-bottom:14px;display:none;
  border-left:3px solid;border-radius:0 var(--border-radius-md) var(--border-radius-md) 0;
}
.notice-ok{background:var(--color-background-success);color:var(--color-text-success);border-color:#27ae60}
.notice-warn{background:var(--color-background-warning);color:var(--color-text-warning);border-color:#e67e22}
.notice-err{background:var(--color-background-danger);color:var(--color-text-danger);border-color:#c0392b}

#mainMap{
  width:100%;height:400px;
  border-radius:var(--border-radius-md);
  border:0.5px solid var(--color-border-secondary);
}
.legend-row{display:flex;gap:16px;flex-wrap:wrap;padding:10px 0 2px}
.leg-item{display:flex;align-items:center;gap:6px;font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono)}
.leg-dot{width:9px;height:9px;border-radius:50%;flex-shrink:0}

.ev-list{display:flex;flex-direction:column;gap:8px}
.ev-card{
  background:var(--color-background-primary);
  border:0.5px solid var(--color-border-tertiary);
  border-radius:var(--border-radius-md);
  padding:12px 14px;display:flex;gap:12px;align-items:flex-start;
  transition:border-color .15s;
}
.ev-card:hover{border-color:var(--color-border-secondary)}
.ev-id{
  font-family:var(--font-mono);font-size:10px;
  color:var(--color-text-secondary);margin-bottom:3px;
}
.ev-title{font-size:13px;font-weight:500;margin-bottom:4px}
.ev-desc{font-size:12px;color:var(--color-text-secondary);margin-bottom:6px;line-height:1.45}
.ev-meta{display:flex;align-items:center;gap:6px;flex-wrap:wrap}
.status-pill{
  font-size:10px;font-weight:500;padding:2px 8px;
  border-radius:var(--border-radius-md);
  letter-spacing:0.03em;text-transform:uppercase;
  font-family:var(--font-mono);
}
.ev-thumb{width:52px;height:52px;border-radius:6px;object-fit:cover;border:0.5px solid var(--color-border-tertiary);flex-shrink:0}
.ev-loc{font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono)}
.empty-state{text-align:center;padding:40px 16px;color:var(--color-text-secondary);font-size:13px;font-family:var(--font-mono)}

.loading-wrap{
  display:flex;flex-direction:column;align-items:center;
  justify-content:center;padding:48px 16px;gap:12px;
}
.spinner{width:28px;height:28px;border:2px solid var(--color-border-secondary);border-top-color:#1a3a6b;border-radius:50%;animation:spin .7s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.loading-wrap p{font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono)}

.lang-switcher{
  display:flex;align-items:center;gap:4px;
  margin-left:auto;
}
.lang-btn{
  padding:4px 8px;font-size:11px;font-weight:500;
  border:0.5px solid var(--color-border-tertiary);
  border-radius:var(--border-radius-md);
  background:transparent;color:var(--color-text-secondary);
  cursor:pointer;font-family:var(--font-mono);
  transition:all .15s;
}
.lang-btn.active{background:#1a3a6b;color:white;border-color:#1a3a6b}
.lang-btn:hover:not(.active){border-color:#1a3a6b;color:#1a3a6b}

/* Admin login */
.admin-bar{
  display:flex;align-items:center;gap:8px;
  padding:8px 20px;
  background:var(--color-background-secondary);
  border-bottom:0.5px solid var(--color-border-tertiary);
  font-size:11px;font-family:var(--font-mono);
}
.admin-badge{
  display:inline-flex;align-items:center;gap:5px;
  background:#1a3a6b;color:white;
  padding:3px 9px;border-radius:var(--border-radius-md);
  font-size:10px;font-weight:500;letter-spacing:0.04em;
}
.admin-badge svg{width:10px;height:10px;fill:white}
.btn-admin-login{
  margin-left:auto;padding:4px 10px;
  border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);
  background:transparent;color:var(--color-text-secondary);
  cursor:pointer;font-size:11px;font-family:var(--font-mono);
  transition:all .15s;
}
.btn-admin-login:hover{border-color:#1a3a6b;color:#1a3a6b}
.btn-admin-logout{
  margin-left:auto;padding:4px 10px;
  border:0.5px solid #c0392b40;
  border-radius:var(--border-radius-md);
  background:transparent;color:#c0392b;
  cursor:pointer;font-size:11px;font-family:var(--font-mono);
  transition:all .15s;
}
.btn-admin-logout:hover{background:#fdf0ef}

/* Resolve modal */
.modal-overlay{
  position:fixed;inset:0;background:rgba(0,0,0,0.45);
  display:flex;align-items:center;justify-content:center;
  z-index:9999;padding:16px;
}
.modal-box{
  background:var(--color-background-primary);
  border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);
  width:100%;max-width:440px;
  box-shadow:0 8px 32px rgba(0,0,0,0.18);
  overflow:hidden;
}
.modal-header{
  display:flex;align-items:center;justify-content:space-between;
  padding:14px 16px 12px;
  border-bottom:0.5px solid var(--color-border-tertiary);
}
.modal-title{font-size:13px;font-weight:500;color:var(--color-text-primary)}
.modal-ref{font-size:10px;color:var(--color-text-secondary);font-family:var(--font-mono);margin-top:2px}
.modal-close{
  width:24px;height:24px;border:none;background:transparent;
  cursor:pointer;color:var(--color-text-secondary);font-size:18px;
  display:flex;align-items:center;justify-content:center;
  border-radius:4px;transition:background .15s;
}
.modal-close:hover{background:var(--color-background-secondary)}
.modal-body{padding:16px}
.modal-img-zone{
  border:0.5px dashed var(--color-border-primary);
  border-radius:var(--border-radius-md);
  padding:20px;text-align:center;cursor:pointer;
  position:relative;background:var(--color-background-secondary);
  transition:all .15s;margin-bottom:12px;
}
.modal-img-zone:hover{border-color:#27ae60;background:rgba(39,174,96,.04)}
.modal-img-zone.has-img{border-color:#27ae60;border-style:solid}
.modal-img-zone input{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.modal-img-zone p{font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono);margin-top:6px}
.modal-img-zone svg{width:22px;height:22px;margin:0 auto;opacity:.4;display:block}
.modal-prev{width:100%;max-height:120px;object-fit:cover;border-radius:6px;margin-top:8px;display:none}
.modal-note{font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono);margin-bottom:12px;line-height:1.5}
.modal-err{
  font-size:11px;color:#c0392b;background:#fdf0ef;
  border:0.5px solid #c0392b40;border-radius:var(--border-radius-md);
  padding:8px 10px;margin-bottom:10px;font-family:var(--font-mono);display:none;
}
.modal-footer{
  display:flex;gap:8px;padding:12px 16px;
  border-top:0.5px solid var(--color-border-tertiary);
}
.btn-cancel{
  flex:1;padding:10px;border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);background:var(--color-background-secondary);
  color:var(--color-text-secondary);cursor:pointer;font-size:12px;font-family:var(--font-sans);
  font-weight:500;transition:all .15s;
}
.btn-cancel:hover{border-color:var(--color-border-primary);color:var(--color-text-primary)}
.btn-resolve{
  flex:2;padding:10px;border:none;
  border-radius:var(--border-radius-md);background:#27ae60;
  color:white;cursor:pointer;font-size:12px;font-family:var(--font-sans);
  font-weight:500;transition:all .15s;letter-spacing:0.02em;
}
.btn-resolve:hover{opacity:.9}

/* Resolved card style */
.ev-card.resolved{border-left:3px solid #27ae60;border-radius:0 var(--border-radius-md) var(--border-radius-md) 0;opacity:.85}
.resolved-thumb{
  width:52px;height:52px;border-radius:6px;object-fit:cover;
  border:1.5px solid #27ae6060;flex-shrink:0;
}

/* Admin login input modal */
.login-modal-overlay{
  position:fixed;inset:0;background:rgba(0,0,0,0.45);
  display:flex;align-items:center;justify-content:center;
  z-index:9999;padding:16px;
}
.login-modal-box{
  background:var(--color-background-primary);
  border:0.5px solid var(--color-border-secondary);
  border-radius:var(--border-radius-md);
  width:100%;max-width:320px;
  box-shadow:0 8px 32px rgba(0,0,0,0.18);
  padding:20px;
}
.login-modal-box h3{font-size:14px;font-weight:500;margin-bottom:4px;color:var(--color-text-primary)}
.login-modal-box p{font-size:11px;color:var(--color-text-secondary);font-family:var(--font-mono);margin-bottom:14px}
.login-modal-box input{margin-bottom:10px}
.login-modal-btns{display:flex;gap:8px}
</style>

<div class="wrap">
  <div class="gov-header">
    <div class="gov-stripe"></div>
    <div class="gov-inner">
      <div class="gov-logo">
        <svg viewBox="0 0 24 24"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
      </div>
      <div class="gov-title">
        <h1 data-i18n="title">Sistem za prijavu štete od nepogoda</h1>
        <p data-i18n="subtitle">Civilna zaštita · Upravljanje vanrednim situacijama</p>
      </div>
      <div style="display:flex;flex-direction:column;align-items:flex-end;gap:6px;margin-left:auto">
        <div class="lang-switcher">
          <button class="lang-btn active" onclick="setLang('sr')">SR</button>
          <button class="lang-btn" onclick="setLang('en')">EN</button>
          <button class="lang-btn" onclick="setLang('de')">DE</button>
        </div>
        <div class="gov-badge">
          <span class="dot-g" id="netDot"></span>
          <span id="netTxt">Online</span>
        </div>
      </div>
    </div>
  </div>

  <div class="nav-bar">
    <button class="nav-tab active" onclick="goTab('add')" data-i18n="tab_add">Nova prijava</button>
    <button class="nav-tab" onclick="goTab('map')" data-i18n="tab_map">Karta</button>
    <button class="nav-tab" onclick="goTab('list')" data-i18n="tab_list">Evidencija</button>
  </div>

  <!-- Admin bar -->
  <div class="admin-bar" id="adminBar">
    <span id="adminBarText" style="color:var(--color-text-secondary)" data-i18n="admin_hint">Administrator: prijavite se za upravljanje prijavama</span>
    <button class="btn-admin-login" id="adminLoginBtn" onclick="openLoginModal()" data-i18n="admin_login">Prijava</button>
    <span class="admin-badge" id="adminBadge" style="display:none">
      <svg viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
      <span data-i18n="admin_badge">ADMINISTRATOR</span>
    </span>
    <button class="btn-admin-logout" id="adminLogoutBtn" style="display:none" onclick="adminLogout()" data-i18n="admin_logout">Odjava</button>
  </div>

  <!-- Admin login modal -->
  <div class="login-modal-overlay" id="loginModal" style="display:none" onclick="if(event.target===this)closeLoginModal()">
    <div class="login-modal-box">
      <h3 data-i18n="admin_login_title">Administrator prijava</h3>
      <p data-i18n="admin_login_sub">Unesite administratorsku lozinku</p>
      <input type="password" id="adminPassInput" data-i18n-ph="admin_pass_ph" placeholder="Lozinka..." onkeydown="if(event.key==='Enter')doAdminLogin()">
      <div class="modal-err" id="loginErr" data-i18n="admin_wrong_pass">Pogrešna lozinka.</div>
      <div class="login-modal-btns">
        <button class="btn-cancel" onclick="closeLoginModal()" data-i18n="btn_cancel">Otkaži</button>
        <button class="btn-resolve" onclick="doAdminLogin()" data-i18n="admin_login">Prijava</button>
      </div>
    </div>
  </div>

  <!-- Resolve modal -->
  <div class="modal-overlay" id="resolveModal" style="display:none" onclick="if(event.target===this)closeResolveModal()">
    <div class="modal-box">
      <div class="modal-header">
        <div>
          <div class="modal-title" data-i18n="resolve_title">Označi prijavu kao rešenu</div>
          <div class="modal-ref" id="resolveRef"></div>
        </div>
        <button class="modal-close" onclick="closeResolveModal()">×</button>
      </div>
      <div class="modal-body">
        <p class="modal-note" data-i18n="resolve_note">Obavezno priložite fotografiju kao dokaz da je prijava rešena.</p>
        <div class="modal-img-zone" id="resolveImgZone">
          <input type="file" accept="image/*" capture="environment" onchange="loadResolveImg(event)">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M23 19a2 2 0 01-2 2H3a2 2 0 01-2-2V8a2 2 0 012-2h4l2-3h6l2 3h4a2 2 0 012 2z"/>
            <circle cx="12" cy="13" r="4"/>
          </svg>
          <p id="resolveImgLbl" data-i18n="resolve_img_lbl">Kliknite za dodavanje fotografije dokaza</p>
          <img id="resolveImgPrev" class="modal-prev" alt="">
        </div>
        <div class="modal-err" id="resolveErr" data-i18n="resolve_err">Fotografija je obavezna za označavanje prijave kao rešene.</div>
      </div>
      <div class="modal-footer">
        <button class="btn-cancel" onclick="closeResolveModal()" data-i18n="btn_cancel">Otkaži</button>
        <button class="btn-resolve" onclick="doResolve()" data-i18n="resolve_btn">✓ Označi kao rešeno</button>
      </div>
    </div>
  </div>

  <div class="body">

    <div class="panel active" id="tab-add">
      <div class="notice notice-ok" id="nOk" data-i18n="notice_ok">Prijava je uspešno evidentirana i dostupna svim korisnicima sistema.</div>
      <div class="notice notice-warn" id="nOff" data-i18n="notice_off">Offline — prijava sačuvana lokalno. Biće automatski sinhronizovana.</div>
      <div class="notice notice-err" id="nErr"></div>

      <div class="stats-row">
        <div class="stat-card">
          <div class="stat-n" id="sAll">—</div>
          <div class="stat-l" data-i18n="stat_all">Ukupno prijava</div>
        </div>
        <div class="stat-card warn">
          <div class="stat-n" id="sPend" style="color:#e67e22">—</div>
          <div class="stat-l" data-i18n="stat_pend">Na čekanju</div>
        </div>
        <div class="stat-card danger">
          <div class="stat-n" id="sCrit" style="color:#c0392b">—</div>
          <div class="stat-l" data-i18n="stat_crit">Kritično (3–4)</div>
        </div>
      </div>

      <div class="form-section">
        <label class="field-label" data-i18n="lbl_type">Vrsta nepogode <span class="required">*</span></label>
        <select id="fType">
          <option value="" data-i18n="opt_type_default">— Izaberite vrstu nepogode —</option>
          <option value="earthquake" data-i18n="dis_earthquake">Zemljotres</option>
          <option value="flood" data-i18n="dis_flood">Poplava</option>
          <option value="tsunami" data-i18n="dis_tsunami">Cunami</option>
          <option value="hurricane" data-i18n="dis_hurricane">Uragan / oluja</option>
          <option value="wildfire" data-i18n="dis_wildfire">Šumski požar</option>
          <option value="landslide" data-i18n="dis_landslide">Klizište</option>
          <option value="drought" data-i18n="dis_drought">Suša</option>
          <option value="other" data-i18n="dis_other">Ostalo</option>
        </select>
      </div>

      <div class="form-section">
        <label class="field-label" data-i18n="lbl_sev">Stepen štete <span class="required">*</span></label>
        <div class="sev-grid">
          <button class="sev-opt" data-s="1" onclick="pickSev(1)">
            <span class="sev-num">I</span>
            <span class="sev-name" data-i18n="sev1">Neznatna</span>
          </button>
          <button class="sev-opt" data-s="2" onclick="pickSev(2)">
            <span class="sev-num">II</span>
            <span class="sev-name" data-i18n="sev2">Umerena</span>
          </button>
          <button class="sev-opt" data-s="3" onclick="pickSev(3)">
            <span class="sev-num">III</span>
            <span class="sev-name" data-i18n="sev3">Teška</span>
          </button>
          <button class="sev-opt" data-s="4" onclick="pickSev(4)">
            <span class="sev-num">IV</span>
            <span class="sev-name" data-i18n="sev4">Katastrofalna</span>
          </button>
        </div>
        <div class="sev-desc-row">
          <span data-i18n="sevd1">Manja oštećenja</span>
          <span data-i18n="sevd2">Značajna šteta</span>
          <span data-i18n="sevd3">Velika razaranja</span>
          <span data-i18n="sevd4">Potpuno uništenje</span>
        </div>
      </div>

      <div class="form-section">
        <label class="field-label" data-i18n="lbl_desc">Opis oštećenja <span class="required">*</span></label>
        <textarea id="fDesc" data-i18n-ph="ph_desc" placeholder="Opišite oštećenja, broj povređenih, evakuacije, stanje infrastrukture..."></textarea>
      </div>

      <div class="divider"></div>

      <div class="form-section">
        <label class="field-label" data-i18n="lbl_loc">Lokacija <span class="required">*</span></label>
        <div class="row2" style="margin-bottom:8px">
          <input id="fLoc" data-i18n-ph="ph_loc" placeholder="Naziv mesta, opštine...">
          <button class="btn-sm" id="gpsBtn" onclick="getGPS()" data-i18n="btn_gps">GPS lokacija</button>
        </div>
        <div class="row2">
          <input id="fLat" data-i18n-ph="ph_lat" placeholder="Geografska širina" type="number" step="any" oninput="onCoordInput()">
          <input id="fLng" data-i18n-ph="ph_lng" placeholder="Geografska dužina" type="number" step="any" oninput="onCoordInput()">
        </div>
        <div id="accPill" class="acc-pill"></div>
        <p class="hint-txt" id="coordHint" data-i18n="coord_hint">Koristite GPS ili kliknite na kartu za precizno određivanje lokacije</p>
        <div id="locMap"></div>
        <p class="map-hint" data-i18n="map_hint">Kliknite na kartu za postavljanje lokacije prijave</p>
      </div>

      <div class="form-section">
        <label class="field-label" data-i18n="lbl_photo">Fotografija oštećenja</label>
        <div class="img-zone">
          <input type="file" accept="image/*" capture="environment" onchange="loadImg(event)">
          <svg class="img-zone-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M23 19a2 2 0 01-2 2H3a2 2 0 01-2-2V8a2 2 0 012-2h4l2-3h6l2 3h4a2 2 0 012 2z"/>
            <circle cx="12" cy="13" r="4"/>
          </svg>
          <p id="imgLbl" data-i18n="img_lbl">Priložite fotografiju oštećenja (opciono)</p>
          <img id="imgPrev" class="img-prev-box" alt="">
        </div>
      </div>

      <button class="btn-submit" onclick="doSubmit()" data-i18n="btn_submit">Evidentiraj prijavu</button>
    </div>

    <div class="panel" id="tab-map">
      <div id="mainMap"></div>
      <div class="legend-row">
        <div class="leg-item"><div class="leg-dot" style="background:#e67e22"></div><span data-i18n="leg1">Stepen I</span></div>
        <div class="leg-item"><div class="leg-dot" style="background:#d35400"></div><span data-i18n="leg2">Stepen II</span></div>
        <div class="leg-item"><div class="leg-dot" style="background:#c0392b"></div><span data-i18n="leg3">Stepen III</span></div>
        <div class="leg-item"><div class="leg-dot" style="background:#7b241c"></div><span data-i18n="leg4">Stepen IV</span></div>
      </div>
      <p style="font-size:10px;color:var(--color-text-secondary);margin-top:4px;font-family:var(--font-mono)" data-i18n="map_footer">Kliknite na marker za detalje prijave · Karta keširana, radi offline</p>
    </div>

    <div class="panel" id="tab-list">
      <div id="evList" class="ev-list"></div>
    </div>

  </div>
</div>

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
const SEV_C=['','#e67e22','#d35400','#c0392b','#7b241c'];
const SEV_BG=['','#fef3e2','#fef0e7','#fdecea','#f9e5e5'];
const SEV_TC=['','#a04000','#7c2d12','#7b241c','#5a1010'];
const SEV_R=[0,9,12,16,20];
const RN=['','I','II','III','IV'];

// ── i18n ──────────────────────────────────────────────────────────────────
const LANGS={
  sr:{
    title:'Sistem za prijavu štete od nepogoda',
    subtitle:'Civilna zaštita · Upravljanje vanrednim situacijama',
    tab_add:'Nova prijava',tab_map:'Karta',tab_list:'Evidencija',
    notice_ok:'Prijava je uspešno evidentirana i dostupna svim korisnicima sistema.',
    notice_off:'Offline — prijava sačuvana lokalno. Biće automatski sinhronizovana.',
    stat_all:'Ukupno prijava',stat_pend:'Na čekanju',stat_crit:'Kritično (3–4)',
    lbl_type:'Vrsta nepogode',lbl_sev:'Stepen štete',lbl_desc:'Opis oštećenja',
    lbl_loc:'Lokacija',lbl_photo:'Fotografija oštećenja',
    opt_type_default:'— Izaberite vrstu nepogode —',
    dis_earthquake:'Zemljotres',dis_flood:'Poplava',dis_tsunami:'Cunami',
    dis_hurricane:'Uragan / oluja',dis_wildfire:'Šumski požar',
    dis_landslide:'Klizište',dis_drought:'Suša',dis_other:'Ostalo',
    sev1:'Neznatna',sev2:'Umerena',sev3:'Teška',sev4:'Katastrofalna',
    sevd1:'Manja oštećenja',sevd2:'Značajna šteta',sevd3:'Velika razaranja',sevd4:'Potpuno uništenje',
    ph_desc:'Opišite oštećenja, broj povređenih, evakuacije, stanje infrastrukture...',
    ph_loc:'Naziv mesta, opštine...',ph_lat:'Geografska širina',ph_lng:'Geografska dužina',
    btn_gps:'GPS lokacija',coord_hint:'Koristite GPS ili kliknite na kartu za precizno određivanje lokacije',
    map_hint:'Kliknite na kartu za postavljanje lokacije prijave',
    img_lbl:'Priložite fotografiju oštećenja (opciono)',
    btn_submit:'Evidentiraj prijavu',
    leg1:'Stepen I',leg2:'Stepen II',leg3:'Stepen III',leg4:'Stepen IV',
    map_footer:'Kliknite na marker za detalje prijave · Karta keširana, radi offline',
    online:'Online',offline:'Offline',
    pending_lbl:'Na čekanju',
    gps_searching:'Tražim...',gps_hint_searching:'Tražim GPS signal, molimo sačekajte...',
    gps_acc:'Tačnost lokacije: ±',gps_ok:'GPS lokacija uspešno određena',
    gps_err1:'Pristup lokaciji odbijen. Proverite podešavanja.',
    gps_err2:'GPS signal nije pronađen.',gps_err3:'Timeout — pokušajte ponovo na otvorenom prostoru.',
    gps_na:'GPS nije dostupan na ovom uređaju.',gps_generic:'Greška GPS-a.',
    map_click:'Lokacija određena klikom na kartu',
    coord_reset:'Koristite GPS ili kliknite na kartu za precizno određivanje lokacije',
    err_type:'Obavezno polje: Vrsta nepogode.',err_sev:'Obavezno polje: Stepen štete.',
    err_desc:'Obavezno polje: Opis oštećenja.',err_loc:'Obavezno polje: Lokacija.',
    err_coords:'Odredite tačnu lokaciju GPS-om ili klikom na kartu.',
    ok_submit:'Prijava evidentirana i dostupna svim korisnicima sistema.',
    off_submit:'Prijava sačuvana lokalno. Sinhronizacija kada se veza uspostavi.',
    sync_ok:'Offline prijave su uspešno sinhronizovane sa sistemom.',
    empty_list:'Nema evidentiranih prijava u sistemu.\nDodajte prvu prijavu putem obrasca.',
    admin_hint:'Administrator: prijavite se za upravljanje prijavama',
    admin_login:'Prijava',admin_badge:'ADMINISTRATOR',admin_logout:'Odjava',
    admin_login_title:'Administrator prijava',admin_login_sub:'Unesite administratorsku lozinku',
    admin_pass_ph:'Lozinka...',admin_wrong_pass:'Pogrešna lozinka.',
    resolve_title:'Označi prijavu kao rešenu',
    resolve_note:'Obavezno priložite fotografiju kao dokaz da je prijava rešena.',
    resolve_img_lbl:'Kliknite za dodavanje fotografije dokaza',
    resolve_err:'Fotografija je obavezna za označavanje prijave kao rešene.',
    resolve_btn:'✓ Označi kao rešeno',resolve_ok:'Prijava uspešno označena kao rešena.',
    resolved_lbl:'REŠENO',resolved_by:'Rešio administrator',
    btn_cancel:'Otkaži',btn_resolve_card:'Označi kao rešeno',
  },
  en:{
    title:'Disaster Damage Reporting System',
    subtitle:'Civil Protection · Emergency Management',
    tab_add:'New Report',tab_map:'Map',tab_list:'Records',
    notice_ok:'Report successfully recorded and available to all system users.',
    notice_off:'Offline — report saved locally. Will sync automatically.',
    stat_all:'Total reports',stat_pend:'Pending',stat_crit:'Critical (3–4)',
    lbl_type:'Disaster type',lbl_sev:'Damage severity',lbl_desc:'Damage description',
    lbl_loc:'Location',lbl_photo:'Damage photo',
    opt_type_default:'— Select disaster type —',
    dis_earthquake:'Earthquake',dis_flood:'Flood',dis_tsunami:'Tsunami',
    dis_hurricane:'Hurricane / storm',dis_wildfire:'Wildfire',
    dis_landslide:'Landslide',dis_drought:'Drought',dis_other:'Other',
    sev1:'Minor',sev2:'Moderate',sev3:'Severe',sev4:'Catastrophic',
    sevd1:'Minor damage',sevd2:'Significant damage',sevd3:'Major destruction',sevd4:'Total destruction',
    ph_desc:'Describe damage, number of injured, evacuations, infrastructure status...',
    ph_loc:'Town, municipality name...',ph_lat:'Latitude',ph_lng:'Longitude',
    btn_gps:'GPS location',coord_hint:'Use GPS or click on the map for precise location',
    map_hint:'Click on the map to set report location',
    img_lbl:'Attach damage photo (optional)',
    btn_submit:'Submit report',
    leg1:'Level I',leg2:'Level II',leg3:'Level III',leg4:'Level IV',
    map_footer:'Click marker for report details · Map cached, works offline',
    online:'Online',offline:'Offline',
    pending_lbl:'Pending',
    gps_searching:'Searching...',gps_hint_searching:'Searching for GPS signal, please wait...',
    gps_acc:'Location accuracy: ±',gps_ok:'GPS location successfully acquired',
    gps_err1:'Location access denied. Check your settings.',
    gps_err2:'GPS signal not found.',gps_err3:'Timeout — try again in an open area.',
    gps_na:'GPS not available on this device.',gps_generic:'GPS error.',
    map_click:'Location set by map click',
    coord_reset:'Use GPS or click on the map for precise location',
    err_type:'Required field: Disaster type.',err_sev:'Required field: Damage severity.',
    err_desc:'Required field: Damage description.',err_loc:'Required field: Location.',
    err_coords:'Set exact location using GPS or by clicking the map.',
    ok_submit:'Report recorded and available to all system users.',
    off_submit:'Report saved locally. Will sync when connection is restored.',
    sync_ok:'Offline reports successfully synced with the system.',
    empty_list:'No reports recorded in the system.\nAdd the first report via the form.',
    admin_hint:'Administrator: log in to manage reports',
    admin_login:'Login',admin_badge:'ADMINISTRATOR',admin_logout:'Logout',
    admin_login_title:'Administrator login',admin_login_sub:'Enter the administrator password',
    admin_pass_ph:'Password...',admin_wrong_pass:'Incorrect password.',
    resolve_title:'Mark report as resolved',
    resolve_note:'A photo is required as proof that the report has been resolved.',
    resolve_img_lbl:'Click to attach proof photo',
    resolve_err:'A photo is required to mark the report as resolved.',
    resolve_btn:'✓ Mark as resolved',resolve_ok:'Report successfully marked as resolved.',
    resolved_lbl:'RESOLVED',resolved_by:'Resolved by administrator',
    btn_cancel:'Cancel',btn_resolve_card:'Mark as resolved',
  },
  de:{
    title:'System zur Meldung von Katastrophenschäden',
    subtitle:'Zivilschutz · Notfallmanagement',
    tab_add:'Neue Meldung',tab_map:'Karte',tab_list:'Aufzeichnungen',
    notice_ok:'Meldung erfolgreich erfasst und für alle Systembenutzer verfügbar.',
    notice_off:'Offline — Meldung lokal gespeichert. Wird automatisch synchronisiert.',
    stat_all:'Meldungen gesamt',stat_pend:'Ausstehend',stat_crit:'Kritisch (3–4)',
    lbl_type:'Katastrophenart',lbl_sev:'Schadensgrad',lbl_desc:'Schadensbeschreibung',
    lbl_loc:'Standort',lbl_photo:'Schadensfoto',
    opt_type_default:'— Katastrophenart auswählen —',
    dis_earthquake:'Erdbeben',dis_flood:'Überschwemmung',dis_tsunami:'Tsunami',
    dis_hurricane:'Hurrikan / Sturm',dis_wildfire:'Waldbrand',
    dis_landslide:'Erdrutsch',dis_drought:'Dürre',dis_other:'Sonstiges',
    sev1:'Geringfügig',sev2:'Mäßig',sev3:'Schwer',sev4:'Katastrophal',
    sevd1:'Geringer Schaden',sevd2:'Erheblicher Schaden',sevd3:'Große Zerstörung',sevd4:'Totalzerstörung',
    ph_desc:'Schäden, Verletzte, Evakuierungen, Infrastrukturzustand beschreiben...',
    ph_loc:'Ort, Gemeindename...',ph_lat:'Breitengrad',ph_lng:'Längengrad',
    btn_gps:'GPS-Standort',coord_hint:'GPS verwenden oder auf Karte klicken für genauen Standort',
    map_hint:'Auf die Karte klicken, um den Meldestandort festzulegen',
    img_lbl:'Schadensfoto anhängen (optional)',
    btn_submit:'Meldung einreichen',
    leg1:'Stufe I',leg2:'Stufe II',leg3:'Stufe III',leg4:'Stufe IV',
    map_footer:'Auf Marker klicken für Meldedetails · Karte gecacht, funktioniert offline',
    online:'Online',offline:'Offline',
    pending_lbl:'Ausstehend',
    gps_searching:'Suche...',gps_hint_searching:'GPS-Signal wird gesucht, bitte warten...',
    gps_acc:'Standortgenauigkeit: ±',gps_ok:'GPS-Standort erfolgreich ermittelt',
    gps_err1:'Standortzugriff verweigert. Einstellungen prüfen.',
    gps_err2:'GPS-Signal nicht gefunden.',gps_err3:'Timeout — auf freiem Gelände erneut versuchen.',
    gps_na:'GPS auf diesem Gerät nicht verfügbar.',gps_generic:'GPS-Fehler.',
    map_click:'Standort per Kartenklick festgelegt',
    coord_reset:'GPS verwenden oder auf Karte klicken für genauen Standort',
    err_type:'Pflichtfeld: Katastrophenart.',err_sev:'Pflichtfeld: Schadensgrad.',
    err_desc:'Pflichtfeld: Schadensbeschreibung.',err_loc:'Pflichtfeld: Standort.',
    err_coords:'Genauen Standort per GPS oder Kartenklick festlegen.',
    ok_submit:'Meldung erfasst und für alle Systembenutzer verfügbar.',
    off_submit:'Meldung lokal gespeichert. Sync wenn Verbindung wiederhergestellt.',
    sync_ok:'Offline-Meldungen erfolgreich mit dem System synchronisiert.',
    empty_list:'Keine Meldungen im System erfasst.\nErste Meldung über das Formular hinzufügen.',
    admin_hint:'Administrator: Anmelden zur Verwaltung der Meldungen',
    admin_login:'Anmelden',admin_badge:'ADMINISTRATOR',admin_logout:'Abmelden',
    admin_login_title:'Administrator-Anmeldung',admin_login_sub:'Administratorpasswort eingeben',
    admin_pass_ph:'Passwort...',admin_wrong_pass:'Falsches Passwort.',
    resolve_title:'Meldung als gelöst markieren',
    resolve_note:'Ein Foto als Nachweis der Lösung ist erforderlich.',
    resolve_img_lbl:'Klicken zum Anhängen des Nachweisfotos',
    resolve_err:'Ein Foto ist erforderlich, um die Meldung als gelöst zu markieren.',
    resolve_btn:'✓ Als gelöst markieren',resolve_ok:'Meldung erfolgreich als gelöst markiert.',
    resolved_lbl:'GELÖST',resolved_by:'Gelöst vom Administrator',
    btn_cancel:'Abbrechen',btn_resolve_card:'Als gelöst markieren',
  }
};

let currentLang='sr';

function t(key){return LANGS[currentLang][key]||LANGS.sr[key]||key}

function applyLang(){
  document.querySelectorAll('[data-i18n]').forEach(el=>{
    const key=el.getAttribute('data-i18n');
    // For labels that contain a <span class="required">, preserve it
    const req=el.querySelector('.required');
    if(req){el.childNodes[0].textContent=t(key)+' ';return}
    el.textContent=t(key);
  });
  document.querySelectorAll('[data-i18n-ph]').forEach(el=>{
    el.placeholder=t(el.getAttribute('data-i18n-ph'));
  });
  // Update network badge
  const on=navigator.onLine;
  document.getElementById('netTxt').textContent=on?t('online'):t('offline');
  // Update active lang button
  document.querySelectorAll('.lang-btn').forEach(b=>b.classList.toggle('active',b.textContent.toLowerCase()===currentLang));
  // Update dynamic data
  updateStats();
  renderList();
  refreshMarkers();
  // Update DIS map
  DIS.earthquake=t('dis_earthquake');DIS.flood=t('dis_flood');DIS.tsunami=t('dis_tsunami');
  DIS.hurricane=t('dis_hurricane');DIS.wildfire=t('dis_wildfire');DIS.landslide=t('dis_landslide');
  DIS.drought=t('dis_drought');DIS.other=t('dis_other');
  // Update SEV_L
  SEV_L[1]=t('sev1');SEV_L[2]=t('sev2');SEV_L[3]=t('sev3');SEV_L[4]=t('sev4');
}

function setLang(lang){
  currentLang=lang;
  try{localStorage.setItem('dr_lang',lang)}catch(e){}
  applyLang();
}

const SEV_L=['','Neznatna','Umerena','Teška','Katastrofalna'];
const DIS={earthquake:'Zemljotres',flood:'Poplava',tsunami:'Cunami',hurricane:'Uragan',wildfire:'Požar',landslide:'Klizište',drought:'Suša',other:'Ostalo'};

let selSev=0,imgData=null,reports=[];
let locMap=null,locMarker=null,mainMap=null,mainInited=false;
let isAdmin=false,resolveTargetId=null,resolveImgData=null;

const ADMIN_PASS='admin1234'; // lozinka administratora

// ── Admin login ───────────────────────────────────────────────────────────
function openLoginModal(){
  document.getElementById('loginModal').style.display='flex';
  document.getElementById('adminPassInput').value='';
  document.getElementById('loginErr').style.display='none';
  setTimeout(()=>document.getElementById('adminPassInput').focus(),50);
}
function closeLoginModal(){
  document.getElementById('loginModal').style.display='none';
}
function doAdminLogin(){
  const pass=document.getElementById('adminPassInput').value;
  if(pass===ADMIN_PASS){
    isAdmin=true;
    closeLoginModal();
    document.getElementById('adminLoginBtn').style.display='none';
    document.getElementById('adminBarText').style.display='none';
    document.getElementById('adminBadge').style.display='inline-flex';
    document.getElementById('adminLogoutBtn').style.display='inline-flex';
    renderList();
  } else {
    document.getElementById('loginErr').style.display='block';
    document.getElementById('adminPassInput').select();
  }
}
function adminLogout(){
  isAdmin=false;
  document.getElementById('adminLoginBtn').style.display='';
  document.getElementById('adminBarText').style.display='';
  document.getElementById('adminBadge').style.display='none';
  document.getElementById('adminLogoutBtn').style.display='none';
  renderList();
}

// ── Resolve modal ─────────────────────────────────────────────────────────
function openResolveModal(id){
  resolveTargetId=id;
  resolveImgData=null;
  const r=reports.find(x=>x.id===id);
  document.getElementById('resolveRef').textContent=(r?.refId||'')+(r?' · '+r.location:'');
  document.getElementById('resolveImgZone').classList.remove('has-img');
  document.getElementById('resolveImgPrev').style.display='none';
  document.getElementById('resolveImgLbl').textContent=t('resolve_img_lbl');
  document.getElementById('resolveErr').style.display='none';
  document.getElementById('resolveModal').style.display='flex';
}
function closeResolveModal(){
  document.getElementById('resolveModal').style.display='none';
  resolveTargetId=null;resolveImgData=null;
}
function loadResolveImg(e){
  const f=e.target.files[0];if(!f)return;
  const reader=new FileReader();
  reader.onload=x=>{
    const img=new Image();
    img.onload=()=>{
      const c=document.createElement('canvas');
      const MAX=800;let w=img.width,h=img.height;
      if(w>MAX){h=Math.round(h*MAX/w);w=MAX}
      if(h>MAX){w=Math.round(w*MAX/h);h=MAX}
      c.width=w;c.height=h;
      c.getContext('2d').drawImage(img,0,0,w,h);
      resolveImgData=c.toDataURL('image/jpeg',0.75);
      const p=document.getElementById('resolveImgPrev');
      p.src=resolveImgData;p.style.display='block';
      document.getElementById('resolveImgLbl').textContent=f.name;
      document.getElementById('resolveImgZone').classList.add('has-img');
      document.getElementById('resolveErr').style.display='none';
    };
    img.src=x.target.result;
  };
  reader.readAsDataURL(f);
}
async function doResolve(){
  if(!resolveImgData){
    document.getElementById('resolveErr').style.display='block';return;
  }
  const idx=reports.findIndex(x=>x.id===resolveTargetId);
  if(idx===-1)return;
  reports[idx].resolved=true;
  reports[idx].resolvedImg=resolveImgData;
  reports[idx].resolvedDate=new Date().toLocaleString('sr');
  await saveData();
  closeResolveModal();
  showNotice('nOk',t('resolve_ok'));
  renderList();
  refreshMarkers();
  updateStats();
}

function updateNet(){
  const on=navigator.onLine;
  document.getElementById('netDot').className=on?'dot-g':'dot-y';
  document.getElementById('netTxt').textContent=on?t('online'):t('offline');
}
window.addEventListener('online',()=>{updateNet();syncOffline()});
window.addEventListener('offline',updateNet);

async function loadData(){
  try{
    const r=await window.storage.get('disaster_reports_shared',true);
    if(r&&r.value) reports=JSON.parse(r.value);
    else reports=[];
  }catch(e){
    try{const l=localStorage.getItem('dr_gov_v1');if(l)reports=JSON.parse(l)}catch(e2){reports=[];}
  }
}

async function saveData(){
  try{
    if(navigator.onLine){
      await window.storage.set('disaster_reports_shared',JSON.stringify(reports),true);
      localStorage.removeItem('dr_offline_q');
    }else{
      const q=JSON.parse(localStorage.getItem('dr_offline_q')||'[]');
      const newItems=reports.filter(r=>r.pending);
      localStorage.setItem('dr_offline_q',JSON.stringify([...newItems,...q]));
      localStorage.setItem('dr_gov_v1',JSON.stringify(reports));
    }
  }catch(e){localStorage.setItem('dr_gov_v1',JSON.stringify(reports))}
}

async function syncOffline(){
  try{
    // Always clear pending flag on all reports when online
    reports=reports.map(x=>({...x,pending:false}));
    const l=localStorage.getItem('dr_offline_q');
    const q=l?JSON.parse(l):[];
    if(q.length){
      const r=await window.storage.get('disaster_reports_shared',true);
      const remote=r&&r.value?JSON.parse(r.value):[];
      const merged=[...q.map(x=>({...x,pending:false})),...remote];
      const seen=new Set();
      const deduped=merged.filter(x=>{if(seen.has(x.id))return false;seen.add(x.id);return true});
      await window.storage.set('disaster_reports_shared',JSON.stringify(deduped),true);
      reports=deduped;
      localStorage.removeItem('dr_offline_q');
      showNotice('nOk',t('sync_ok'));
    }else{
      // No offline queue, just save cleared pending flags
      await window.storage.set('disaster_reports_shared',JSON.stringify(reports),true);
    }
    updateStats();
    renderList();
    refreshMarkers();
  }catch(e){}
}

function updateStats(){
  document.getElementById('sAll').textContent=reports.length;
  document.getElementById('sPend').textContent=reports.filter(r=>r.pending).length;
  document.getElementById('sCrit').textContent=reports.filter(r=>r.severity>=3).length;
}

function showNotice(id,msg,dur=4000){
  const el=document.getElementById(id);
  if(msg)el.textContent=msg;
  el.style.display='block';
  setTimeout(()=>el.style.display='none',dur);
}

function goTab(t){
  document.querySelectorAll('.nav-tab').forEach((el,i)=>el.classList.toggle('active',['add','map','list'][i]===t));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.getElementById('tab-'+t).classList.add('active');
  if(t==='map'){initMainMap();refreshMarkers()}
  if(t==='list')renderList();
}

function pickSev(n){
  selSev=n;
  document.querySelectorAll('.sev-opt').forEach(b=>b.classList.toggle('on',+b.dataset.s===n));
}

function loadImg(e){
  const f=e.target.files[0];if(!f)return;
  const reader=new FileReader();
  reader.onload=x=>{
    const img=new Image();
    img.onload=()=>{
      const c=document.createElement('canvas');
      const MAX=800;let w=img.width,h=img.height;
      if(w>MAX){h=Math.round(h*MAX/w);w=MAX}
      if(h>MAX){w=Math.round(w*MAX/h);h=MAX}
      c.width=w;c.height=h;
      c.getContext('2d').drawImage(img,0,0,w,h);
      imgData=c.toDataURL('image/jpeg',0.75);
      const p=document.getElementById('imgPrev');
      p.src=imgData;p.style.display='block';
      document.getElementById('imgLbl').textContent=f.name;
    };
    img.src=x.target.result;
  };
  reader.readAsDataURL(f);
}

function getGPS(){
  if(!navigator.geolocation){showNotice('nErr',t('gps_na'));return}
  const btn=document.getElementById('gpsBtn');
  btn.textContent=t('gps_searching');btn.classList.add('active');
  document.getElementById('coordHint').textContent=t('gps_hint_searching');
  navigator.geolocation.getCurrentPosition(pos=>{
    const lat=pos.coords.latitude,lng=pos.coords.longitude,acc=Math.round(pos.coords.accuracy);
    document.getElementById('fLat').value=lat.toFixed(6);
    document.getElementById('fLng').value=lng.toFixed(6);
    const pill=document.getElementById('accPill');
    pill.style.display='inline-flex';
    pill.textContent=t('gps_acc')+acc+'m';
    const good=acc<30;
    pill.style.background=good?'var(--color-background-success)':'var(--color-background-warning)';
    pill.style.color=good?'var(--color-text-success)':'var(--color-text-warning)';
    pill.style.border='0.5px solid '+(good?'var(--color-border-success)':'var(--color-border-warning)');
    pill.style.borderRadius='var(--border-radius-md)';
    pill.style.padding='3px 9px';
    pill.style.fontSize='10px';
    pill.style.fontFamily='var(--font-mono)';
    document.getElementById('coordHint').textContent=t('gps_ok');
    btn.textContent=t('btn_gps');btn.classList.remove('active');
    if(locMap){locMap.setView([lat,lng],16);placeLocMarker(lat,lng)}
  },err=>{
    btn.textContent=t('btn_gps');btn.classList.remove('active');
    const m={1:t('gps_err1'),2:t('gps_err2'),3:t('gps_err3')};
    document.getElementById('coordHint').textContent=m[err.code]||t('gps_generic');
  },{enableHighAccuracy:true,timeout:15000,maximumAge:0});
}

function initLocMap(){
  if(locMap)return;
  locMap=L.map('locMap',{zoomControl:true,attributionControl:false}).setView([44.8,20.4],6);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{maxZoom:19,crossOrigin:true}).addTo(locMap);
  locMap.on('click',e=>{
    placeLocMarker(e.latlng.lat,e.latlng.lng);
    document.getElementById('fLat').value=e.latlng.lat.toFixed(6);
    document.getElementById('fLng').value=e.latlng.lng.toFixed(6);
    document.getElementById('coordHint').textContent=t('map_click');
    document.getElementById('accPill').style.display='none';
  });
}

function placeLocMarker(lat,lng){
  if(locMarker)locMap.removeLayer(locMarker);
  locMarker=L.marker([lat,lng],{
    icon:L.divIcon({
      html:`<div style="width:14px;height:14px;background:#1a3a6b;border:2.5px solid white;border-radius:50%;box-shadow:0 1px 4px rgba(0,0,0,0.4)"></div>`,
      iconSize:[14,14],iconAnchor:[7,7],className:''
    })
  }).addTo(locMap);
}

function onCoordInput(){
  const lat=parseFloat(document.getElementById('fLat').value);
  const lng=parseFloat(document.getElementById('fLng').value);
  if(!isNaN(lat)&&!isNaN(lng)&&locMap){locMap.setView([lat,lng],14);placeLocMarker(lat,lng)}
}

async function doSubmit(){
  const type=document.getElementById('fType').value;
  const desc=document.getElementById('fDesc').value.trim();
  const loc=document.getElementById('fLoc').value.trim();
  const lat=parseFloat(document.getElementById('fLat').value);
  const lng=parseFloat(document.getElementById('fLng').value);
  if(!type){showNotice('nErr',t('err_type'));return}
  if(!selSev){showNotice('nErr',t('err_sev'));return}
  if(!desc){showNotice('nErr',t('err_desc'));return}
  if(!loc){showNotice('nErr',t('err_loc'));return}
  if(isNaN(lat)||isNaN(lng)){showNotice('nErr',t('err_coords'));return}

  const id='SH-'+String(Date.now()).slice(-6);
  const r={
    id:Date.now(),refId:id,type,severity:selSev,
    description:desc,location:loc,lat,lng,image:imgData,
    date:new Date().toLocaleString('sr'),pending:!navigator.onLine,
    accuracy:document.getElementById('accPill').textContent||null
  };
  reports.unshift(r);
  await saveData();
  updateStats();

  if(navigator.onLine) showNotice('nOk',t('ok_submit')+' ('+id+')');
  else showNotice('nOff',id+' — '+t('off_submit'));

  document.getElementById('fType').value='';
  document.getElementById('fDesc').value='';
  document.getElementById('fLoc').value='';
  document.getElementById('fLat').value='';
  document.getElementById('fLng').value='';
  document.getElementById('imgLbl').textContent=t('img_lbl');
  document.getElementById('imgPrev').style.display='none';
  document.getElementById('accPill').style.display='none';
  document.getElementById('coordHint').textContent=t('coord_reset');
  imgData=null;selSev=0;
  document.querySelectorAll('.sev-opt').forEach(b=>b.classList.remove('on'));
  if(locMarker){locMap.removeLayer(locMarker);locMarker=null}
  locMap.setView([44.8,20.4],6);
}

function initMainMap(){
  if(mainInited)return;
  mainInited=true;
  mainMap=L.map('mainMap').setView([20,10],2);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{attribution:'© OpenStreetMap',maxZoom:19,crossOrigin:true}).addTo(mainMap);
}

function refreshMarkers(){
  if(!mainMap)return;
  mainMap.eachLayer(l=>{if(l instanceof L.CircleMarker)mainMap.removeLayer(l)});
  reports.forEach(r=>{
    const fillColor=r.resolved?'#27ae60':SEV_C[r.severity];
    const c=L.circleMarker([r.lat,r.lng],{
      radius:SEV_R[r.severity],fillColor,
      color:'white',weight:2,fillOpacity:0.9
    }).addTo(mainMap);
    c.bindPopup(`
      <div style="font-family:var(--font-sans,sans-serif);min-width:200px">
        <div style="font-size:10px;color:#888;font-family:monospace;margin-bottom:4px">${r.refId||''} · ${r.date}</div>
        <div style="font-weight:500;font-size:14px;margin-bottom:4px">${DIS[r.type]||r.type}</div>
        <div style="font-size:12px;color:#666;margin-bottom:7px">📍 ${r.location}</div>
        <span style="background:${SEV_BG[r.severity]};color:${SEV_TC[r.severity]};padding:3px 9px;border-radius:4px;font-size:10px;font-weight:500;text-transform:uppercase;letter-spacing:.04em">${RN[r.severity]}: ${SEV_L[r.severity]}</span>
        ${r.resolved?`<span style="background:#eafaf1;color:#1e8449;padding:3px 9px;border-radius:4px;font-size:10px;font-weight:500;text-transform:uppercase;letter-spacing:.04em;margin-left:4px">✓ ${t('resolved_lbl')}</span>`:''}
        <div style="font-size:12px;color:#333;margin-top:9px;line-height:1.45">${r.description.slice(0,140)}${r.description.length>140?'...':''}</div>
        ${r.accuracy?`<div style="font-size:10px;color:#999;margin-top:4px;font-family:monospace">${r.accuracy}</div>`:''}
        ${r.image?`<img src="${r.image}" style="width:100%;height:85px;object-fit:cover;border-radius:6px;margin-top:8px">`:''}
        ${r.resolved&&r.resolvedImg?`<div style="font-size:10px;color:#1e8449;margin-top:6px;font-family:monospace">✓ ${t('resolved_by')} · ${r.resolvedDate}</div><img src="${r.resolvedImg}" style="width:100%;height:85px;object-fit:cover;border-radius:6px;margin-top:4px;border:1.5px solid #27ae6060">`:''}
        ${r.pending?`<div style="font-size:10px;color:#e67e22;margin-top:5px;font-family:monospace">${t('pending_lbl')} - sync</div>`:''}
      </div>`);
  });
}

function renderList(){
  const el=document.getElementById('evList');
  if(!reports.length){
    el.innerHTML=`<div class="empty-state">${t('empty_list').replace('\n','<br>')}</div>`;
    return;
  }
  el.innerHTML=reports.map(r=>`
    <div class="ev-card${r.resolved?' resolved':''}">
      <div style="flex:1;min-width:0">
        <div class="ev-id">${r.refId||'—'} · ${r.date}${r.pending?' · '+t('pending_lbl'):''}</div>
        <div class="ev-title">${DIS[r.type]||r.type}</div>
        <div class="ev-loc">📍 ${r.location} &nbsp;·&nbsp; ${r.lat.toFixed(4)}, ${r.lng.toFixed(4)}</div>
        <div class="ev-desc" style="margin-top:4px">${r.description.slice(0,100)}${r.description.length>100?'...':''}</div>
        <div class="ev-meta">
          <span class="status-pill" style="background:${SEV_BG[r.severity]};color:${SEV_TC[r.severity]};border:0.5px solid ${SEV_C[r.severity]}60">
            ${RN[r.severity]}: ${SEV_L[r.severity]}
          </span>
          ${r.pending?`<span class="status-pill" style="background:var(--color-background-warning);color:var(--color-text-warning)">${t('pending_lbl')}</span>`:''}
          ${r.resolved?`<span class="status-pill" style="background:#eafaf1;color:#1e8449;border:0.5px solid #27ae6060">✓ ${t('resolved_lbl')}</span>`:''}
        </div>
        ${r.resolved?`<div style="font-size:10px;color:#1e8449;font-family:var(--font-mono);margin-top:5px">✓ ${t('resolved_by')} · ${r.resolvedDate}</div>`:''}
        ${isAdmin&&!r.resolved?`<button onclick="openResolveModal(${r.id})" style="margin-top:8px;padding:5px 12px;font-size:11px;font-family:var(--font-mono);font-weight:500;border:0.5px solid #27ae6060;border-radius:var(--border-radius-md);background:transparent;color:#27ae60;cursor:pointer;transition:all .15s" onmouseover="this.style.background='#eafaf1'" onmouseout="this.style.background='transparent'">✓ ${t('btn_resolve_card')}</button>`:''}
      </div>
      <div style="display:flex;flex-direction:column;gap:6px;flex-shrink:0">
        ${r.image?`<img class="ev-thumb" src="${r.image}" alt="" title="Originalna fotografija">`:''}
        ${r.resolved&&r.resolvedImg?`<img class="resolved-thumb" src="${r.resolvedImg}" alt="" title="${t('resolved_by')}">`:''}
      </div>
    </div>`).join('');
}

async function init(){
  try{const l=localStorage.getItem('dr_lang');if(l&&LANGS[l])currentLang=l;}catch(e){}
  updateNet();
  await loadData();
  updateStats();
  applyLang();
  setTimeout(initLocMap,200);
  setInterval(async()=>{
    if(!navigator.onLine)return;
    const tab=document.querySelector('.nav-tab.active');
    if(!tab)return;
    await loadData();
    updateStats();
    if(tab.dataset.i18n==='tab_list')renderList();
    if(tab.dataset.i18n==='tab_map')refreshMarkers();
  },30000);
}

init();
</script>
