<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
<title>DLTC — Customer Intake</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@600&display=swap" rel="stylesheet">
<style>
:root{--bg:#F5F5F3;--card:#FFFFFF;--primary:#0A3D62;--primary-tint:#E8F0F7;--primary-soft:#F2F7FB;--accent:#D41C1C;--accent-hover:#B71717;--text:#0D0C0A;--muted:#6B7280;--border:#E5E7EB;--border-strong:#D1D5DB;--success:#10B981;--success-bg:#ECFDF5;--radius:12px;--radius-lg:16px}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{-webkit-text-size-adjust:100%}
html,body{margin:0;padding:0;overflow-x:hidden}
body{background:var(--bg);color:var(--text);font-family:'Inter',-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;font-size:16px;line-height:1.5;min-height:100vh;min-height:100dvh;display:flex;flex-direction:column;align-items:center;padding:24px 16px calc(24px + env(safe-area-inset-bottom))}

/* LOADER */
.loader{position:fixed;inset:0;background:var(--bg);z-index:1000;display:grid;place-items:center;padding:24px;animation:loaderOut 500ms ease 2400ms forwards}
@keyframes loaderOut{to{opacity:0;visibility:hidden;pointer-events:none}}
.loader__inner{width:100%;max-width:380px;text-align:center}
.loader__brand{display:inline-flex;align-items:center;gap:10px;margin-bottom:36px;opacity:0;animation:fadeInUp 500ms ease 100ms forwards}
.loader__brand-mark{width:36px;height:36px;border-radius:8px;background:var(--primary);color:#fff;display:grid;place-items:center;font-weight:700;font-size:14px}
.loader__brand-text{font-weight:600;font-size:16px}
.loader__icons{display:flex;justify-content:center;align-items:flex-end;gap:18px;margin-bottom:28px;min-height:76px}
.loader__service{display:flex;flex-direction:column;align-items:center;gap:8px;opacity:0;transform:scale(0.5) translateY(14px);animation:servicePop 700ms cubic-bezier(0.34,1.56,0.64,1) forwards,serviceFloat 1600ms ease-in-out infinite}
.loader__service:nth-child(1){animation-delay:200ms,1100ms}
.loader__service:nth-child(2){animation-delay:450ms,1350ms}
.loader__service:nth-child(3){animation-delay:700ms,1600ms}
.loader__service:nth-child(4){animation-delay:950ms,1850ms}
@keyframes servicePop{0%{opacity:0;transform:scale(0.5) translateY(14px)}60%{opacity:1;transform:scale(1.15) translateY(-4px)}100%{opacity:1;transform:scale(1) translateY(0)}}
@keyframes serviceFloat{0%,100%{transform:translateY(0)}50%{transform:translateY(-3px)}}
.loader__icon{width:44px;height:44px;border-radius:10px;background:var(--primary-soft);color:var(--primary);display:grid;place-items:center;box-shadow:0 4px 10px rgba(10,61,98,0.08)}
.loader__icon svg{width:26px;height:26px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
.loader__service-label{font-size:10px;font-weight:600;color:var(--muted);letter-spacing:0.04em;text-transform:uppercase}
.loader__tagline{font-size:15px;color:var(--text);font-weight:500;margin-bottom:16px;opacity:0;animation:fadeInUp 500ms ease 1100ms forwards}
.loader__bar{width:140px;height:4px;background:var(--border);border-radius:999px;overflow:hidden;margin:0 auto;opacity:0;animation:fadeInUp 400ms ease 1300ms forwards}
.loader__bar-fill{display:block;height:100%;background:var(--primary);border-radius:999px;width:0;animation:barFill 1100ms ease 1300ms forwards}
@keyframes barFill{to{width:100%}}
@keyframes fadeInUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
@media(prefers-reduced-motion:reduce){.loader,.loader *{animation-duration:1ms !important;animation-delay:0ms !important}}

/* PAGE */
.page{width:100%;max-width:480px;display:flex;flex-direction:column;gap:16px;opacity:0;animation:pageIn 400ms ease 2400ms forwards}
@keyframes pageIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.brand{display:flex;align-items:center;gap:10px;padding:4px 0 8px}
.brand__mark{width:32px;height:32px;border-radius:8px;background:var(--primary);color:#fff;display:grid;place-items:center;font-weight:700;font-size:14px}
.brand__name{font-weight:600;font-size:14px}
.brand__sub{font-size:13px;color:var(--muted);margin-left:auto}
.card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius-lg);padding:28px 22px;box-shadow:0 1px 2px rgba(13,12,10,0.04)}
.card__head h1{font-size:22px;font-weight:700;line-height:1.25;margin:0 0 6px;letter-spacing:-0.01em}
.card__head p{margin:0 0 22px;color:var(--muted);font-size:15px}

/* OPTIONS */
.options{border:none;padding:0;margin:0 0 24px;display:flex;flex-direction:column;gap:10px}
.option{position:relative;display:flex;gap:14px;padding:16px 14px;border:1.5px solid var(--border);border-radius:var(--radius);background:#fff;cursor:pointer;transition:border-color 120ms ease,background 120ms ease;min-height:64px}
.option:hover{border-color:var(--border-strong)}
.option__radio{flex-shrink:0;width:20px;height:20px;border-radius:50%;border:2px solid var(--border-strong);margin-top:2px;display:grid;place-items:center;transition:border-color 120ms ease,background 120ms ease}
.option__radio svg{width:12px;height:12px;color:#fff;opacity:0;transform:scale(0.6);transition:opacity 120ms ease,transform 120ms ease}
.option__body{flex:1;min-width:0}
.option__label{font-weight:600;font-size:15px;margin:0 0 2px}
.option__desc{font-size:13.5px;color:var(--muted);margin:0;line-height:1.4}
.option__code{position:absolute;top:14px;right:14px;font-size:11px;font-weight:500;color:var(--muted);font-family:'JetBrains Mono',monospace;letter-spacing:0.04em}
.option input[type="radio"]{position:absolute;opacity:0;pointer-events:none}
.option.is-selected{border-color:var(--primary);background:var(--primary-tint)}
.option.is-selected .option__radio{border-color:var(--primary);background:var(--primary)}
.option.is-selected .option__radio svg{opacity:1;transform:scale(1)}
.option:focus-within{outline:2px solid var(--primary);outline-offset:2px}

/* DETAILS */
.details{border-top:1px solid var(--border);padding-top:22px;margin-bottom:22px}
.details__title{font-size:13px;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:0.06em;margin:0 0 14px}
.field{display:flex;flex-direction:column;margin-bottom:14px}
.field:last-child{margin-bottom:0}
.field label{font-size:13px;font-weight:500;margin-bottom:6px}
.input{width:100%;border:1.5px solid var(--border);border-radius:10px;background:#fff;padding:0 14px;height:48px;font:inherit;font-size:16px;color:var(--text);transition:border-color 120ms ease,box-shadow 120ms ease}
.input::placeholder{color:#9CA3AF}
.input:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 3px rgba(10,61,98,0.12)}
.input-group{display:flex;align-items:center;width:100%;border:1.5px solid var(--border);border-radius:10px;background:#fff;overflow:hidden;transition:border-color 120ms ease,box-shadow 120ms ease}
.input-group:focus-within{border-color:var(--primary);box-shadow:0 0 0 3px rgba(10,61,98,0.12)}
.input-group__prefix{padding:0 12px 0 14px;height:48px;display:grid;place-items:center;background:#FAFAF9;border-right:1px solid var(--border);font-weight:500;font-size:16px}
.input-group .input{border:none;flex:1;height:46px;box-shadow:none}
.input-group .input:focus{box-shadow:none}

/* SEGMENT */
.segment{display:grid;grid-template-columns:repeat(3,1fr);gap:4px;background:#F3F4F6;border-radius:10px;padding:4px;margin-bottom:0}
.segment__option{position:relative;display:flex;align-items:center;justify-content:center;gap:6px;height:40px;border-radius:8px;font-size:13.5px;font-weight:500;color:var(--muted);cursor:pointer;transition:background 140ms ease,color 140ms ease}
.segment__option input{position:absolute;opacity:0;pointer-events:none}
.segment__option svg{width:14px;height:14px}
.segment__option.is-active{background:#fff;color:var(--primary);font-weight:600;box-shadow:0 1px 3px rgba(0,0,0,0.06)}
.field--hidden{display:none}

/* BUTTON */
.btn{width:100%;min-height:48px;border:none;border-radius:10px;font:inherit;font-size:16px;font-weight:600;cursor:pointer;transition:background 120ms ease,transform 80ms ease;display:inline-flex;align-items:center;justify-content:center;gap:8px}
.btn--primary{background:var(--accent);color:#fff}
.btn--primary:hover{background:var(--accent-hover)}
.btn--primary:active{transform:scale(0.99)}
.btn--primary:disabled{background:#E5E7EB;color:#9CA3AF;cursor:not-allowed}
.help{text-align:center;color:var(--muted);font-size:13px;padding:8px 0;margin:0}

/* SUCCESS */
.success{text-align:center;padding:12px 4px 0}
.success__icon{width:72px;height:72px;margin:4px auto 20px;border-radius:50%;background:var(--success-bg);display:grid;place-items:center;color:var(--success);animation:pop 360ms cubic-bezier(0.34,1.56,0.64,1) both}
.success__icon svg{width:36px;height:36px}
@keyframes pop{0%{transform:scale(0.4);opacity:0}100%{transform:scale(1);opacity:1}}
.success__title{font-size:22px;font-weight:700;margin:0 0 8px;letter-spacing:-0.01em}
.success__lead{font-size:15px;color:var(--muted);margin:0 0 22px}
.ref{font-family:'JetBrains Mono',monospace;font-size:26px;font-weight:600;color:var(--primary);letter-spacing:0.06em;background:var(--primary-tint);border:1.5px dashed rgba(10,61,98,0.3);border-radius:12px;padding:18px 16px;margin:0 0 22px;user-select:all}
.success__msg{font-size:15px;margin:0 0 24px;line-height:1.55}
.success__divider{height:1px;background:var(--border);margin:0 -22px 18px}
.success__footer{font-size:14px;color:var(--muted);margin:0}
.fade-in{animation:fadeIn 280ms ease both}
@keyframes fadeIn{from{opacity:0;transform:translateY(4px)}to{opacity:1;transform:translateY(0)}}
@media(max-width:360px){.card{padding:22px 16px}.card__head h1{font-size:20px}.ref{font-size:22px}.segment__option{font-size:12.5px}.loader__icons{gap:12px}.loader__icon{width:40px;height:40px}.loader__icon svg{width:22px;height:22px}}
</style>
</head>
<body>

<!-- LOADER -->
<div class="loader" id="loader" aria-hidden="true">
  <div class="loader__inner">
    <div class="loader__brand"><span class="loader__brand-mark">DL</span><span class="loader__brand-text">DLTC Intake</span></div>
    <div class="loader__icons">
      <div class="loader__service"><div class="loader__icon"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="2.2"/><path d="M12 9.8 V4.5"/><path d="M10.2 13.6 6 18"/><path d="M13.8 13.6 18 18"/></svg></div><span class="loader__service-label">Driver</span></div>
      <div class="loader__service"><div class="loader__icon"><svg viewBox="0 0 24 24"><rect x="4" y="4" width="16" height="16" rx="2.5"/><path d="M9 8 V16 H15"/></svg></div><span class="loader__service-label">Learner</span></div>
      <div class="loader__service"><div class="loader__icon"><svg viewBox="0 0 24 24"><path d="M2 16 V7 a1 1 0 0 1 1-1 H14 V16"/><path d="M14 9 H18 l3 3.5 V16 H14"/><circle cx="7" cy="17" r="1.8"/><circle cx="17" cy="17" r="1.8"/></svg></div><span class="loader__service-label">PDP</span></div>
      <div class="loader__service"><div class="loader__icon"><svg viewBox="0 0 24 24"><path d="M4 16 V12 l2-4 a2 2 0 0 1 1.8-1.2 H16.2 a2 2 0 0 1 1.8 1.2 L20 12 V16"/><path d="M4 12 H20"/><circle cx="7.5" cy="17" r="1.6"/><circle cx="16.5" cy="17" r="1.6"/></svg></div><span class="loader__service-label">Vehicle</span></div>
    </div>
    <p class="loader__tagline">Welcome — let's get you in and out.</p>
    <div class="loader__bar"><span class="loader__bar-fill"></span></div>
  </div>
</div>

<!-- MAIN -->
<main class="page">
  <header class="brand">
    <div class="brand__mark" aria-hidden="true">DL</div>
    <div class="brand__name">DLTC Intake</div>
    <div class="brand__sub">Department of Transport</div>
  </header>

  <section class="card fade-in" id="step-1">
    <div class="card__head">
      <h1>What brings you in today?</h1>
      <p>Select the option that best describes your visit.</p>
    </div>
    <form id="intake-form" novalidate>
      <fieldset class="options" aria-label="Purpose of visit">
        <label class="option"><input type="radio" name="purpose" value="01"/><span class="option__code">-01</span><span class="option__radio"><svg viewBox="0 0 12 12" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="2 6.5 5 9 10 3"/></svg></span><span class="option__body"><span class="option__label">Driver's Licence</span><span class="option__desc">New application, renewal, or replacement</span></span></label>
        <label class="option"><input type="radio" name="purpose" value="02"/><span class="option__code">-02</span><span class="option__radio"><svg viewBox="0 0 12 12" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="2 6.5 5 9 10 3"/></svg></span><span class="option__body"><span class="option__label">Learner's Licence</span><span class="option__desc">First-time or re-test application</span></span></label>
        <label class="option"><input type="radio" name="purpose" value="03"/><span class="option__code">-03</span><span class="option__radio"><svg viewBox="0 0 12 12" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="2 6.5 5 9 10 3"/></svg></span><span class="option__body"><span class="option__label">Professional Driving Permit</span><span class="option__desc">Commercial or professional licence (PDP)</span></span></label>
        <label class="option"><input type="radio" name="purpose" value="04"/><span class="option__code">-04</span><span class="option__radio"><svg viewBox="0 0 12 12" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="2 6.5 5 9 10 3"/></svg></span><span class="option__body"><span class="option__label">Vehicle Registration</span><span class="option__desc">Roadworthy, registration, or disc renewal</span></span></label>
      </fieldset>

      <div class="details">
        <p class="details__title">Your details</p>

        <div class="field">
          <label for="firstName">First name</label>
          <input class="input" type="text" id="firstName" name="firstName" autocomplete="given-name" placeholder="Thandi" required/>
        </div>

        <div class="field">
          <label>Send my reference via</label>
          <div class="segment" role="radiogroup" aria-label="Delivery method">
            <label class="segment__option is-active"><input type="radio" name="channel" value="whatsapp" checked/><svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2a10 10 0 0 0-8.5 15.2L2 22l4.9-1.5A10 10 0 1 0 12 2Zm5.4 14.2c-.2.6-1.2 1.2-1.7 1.2-.4.1-1 .1-1.6-.1-.4-.1-.9-.3-1.5-.5-2.6-1.1-4.3-3.7-4.4-3.9-.1-.2-1-1.4-1-2.7 0-1.3.7-1.9.9-2.2.2-.2.5-.3.7-.3h.5c.2 0 .4 0 .6.5.2.6.7 1.9.7 2 .1.1.1.3 0 .5l-.3.4c-.1.2-.3.3-.4.5-.1.1-.3.3-.1.6.2.3.7 1.1 1.5 1.8 1 .9 1.8 1.2 2.1 1.3.3.1.4.1.6-.1l.7-.8c.2-.2.4-.2.6-.1l1.6.8c.2.1.4.2.5.3 0 .2 0 .9-.2 1.4Z"/></svg>WhatsApp</label>
            <label class="segment__option"><input type="radio" name="channel" value="email"/><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="5" width="18" height="14" rx="2"/><polyline points="3 7 12 13 21 7"/></svg>Email</label>
            <label class="segment__option"><input type="radio" name="channel" value="both"/>Both</label>
          </div>
        </div>

        <div class="field" id="field-whatsapp" style="margin-top:14px">
          <label for="whatsapp">WhatsApp number</label>
          <div class="input-group">
            <span class="input-group__prefix">+27</span>
            <input class="input" type="tel" id="whatsapp" name="whatsapp" inputmode="numeric" autocomplete="tel-national" placeholder="82 123 4567"/>
          </div>
        </div>

        <div class="field field--hidden" id="field-email" style="margin-top:14px">
          <label for="email">Email address</label>
          <input class="input" type="email" id="email" name="email" autocomplete="email" placeholder="thandi@example.co.za"/>
        </div>
      </div>

      <button type="submit" class="btn btn--primary" id="submit-btn" disabled>Continue</button>
    </form>
  </section>

  <section class="card" id="step-2" hidden>
    <div class="success">
      <div class="success__icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="4 12.5 10 18.5 20 6.5"/></svg></div>
      <h2 class="success__title">You're all set, <span id="successName">there</span>.</h2>
      <p class="success__lead">Your reference number is:</p>
      <div class="ref" id="refNumber" aria-label="Your reference number">256557-01</div>
      <p class="success__msg" id="successMsg">We've sent your reference and next steps to your WhatsApp number.</p>
      <div class="success__divider"></div>
      <p class="success__footer">Need help? Speak to a DLTC official.</p>
    </div>
  </section>

  <p class="help">Protected by POPIA. Your details are used only for your DLTC visit.</p>
</main>

<script>
(function(){
  setTimeout(function(){var l=document.getElementById('loader');if(l)l.style.display='none';},3200);

  var form=document.getElementById('intake-form');
  var submitBtn=document.getElementById('submit-btn');
  var step1=document.getElementById('step-1');
  var step2=document.getElementById('step-2');
  var successName=document.getElementById('successName');
  var successMsg=document.getElementById('successMsg');
  var refNumber=document.getElementById('refNumber');
  var firstName=document.getElementById('firstName');
  var whatsapp=document.getElementById('whatsapp');
  var email=document.getElementById('email');
  var fieldWhats=document.getElementById('field-whatsapp');
  var fieldEmail=document.getElementById('field-email');

  form.querySelectorAll('input[name="purpose"]').forEach(function(r){
    r.addEventListener('change',function(){
      form.querySelectorAll('.option').forEach(function(o){o.classList.remove('is-selected');});
      r.closest('.option').classList.add('is-selected');
      validate();
    });
  });

  form.querySelectorAll('input[name="channel"]').forEach(function(c){
    c.addEventListener('change',function(){
      form.querySelectorAll('.segment__option').forEach(function(s){s.classList.remove('is-active');});
      c.closest('.segment__option').classList.add('is-active');
      applyChannelVisibility();
      validate();
    });
  });

  function selectedChannel(){
    var c=form.querySelector('input[name="channel"]:checked');
    return c?c.value:'whatsapp';
  }
  function applyChannelVisibility(){
    var ch=selectedChannel();
    fieldWhats.classList.toggle('field--hidden',ch==='email');
    fieldEmail.classList.toggle('field--hidden',ch==='whatsapp');
  }
  applyChannelVisibility();

  [firstName,whatsapp,email].forEach(function(el){el.addEventListener('input',validate);});

  function selectedPurpose(){var c=form.querySelector('input[name="purpose"]:checked');return c?c.value:null;}
  function validEmail(v){return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v.trim());}

  function validate(){
    var hasPurpose=!!selectedPurpose();
    var hasName=firstName.value.trim().length>=2;
    var ch=selectedChannel();
    var phoneOk=whatsapp.value.replace(/\D/g,'').length===9;
    var emailOk=validEmail(email.value);
    var contactOk=(ch==='whatsapp'&&phoneOk)||(ch==='email'&&emailOk)||(ch==='both'&&phoneOk&&emailOk);
    submitBtn.disabled=!(hasPurpose&&hasName&&contactOk);
  }

  function genPrefix(){return String(Math.floor(100000+Math.random()*900000));}

  form.addEventListener('submit',function(e){
    e.preventDefault();
    if(submitBtn.disabled)return;
    var name=firstName.value.trim().split(/\s+/)[0];
    var code=selectedPurpose();
    var ch=selectedChannel();
    var ref=genPrefix()+'-'+code;
    successName.textContent=name;
    refNumber.textContent=ref;
    var msg='';
    if(ch==='whatsapp'){msg="We've sent your reference and next steps to your WhatsApp number.";}
    else if(ch==='email'){msg="We've sent your reference and next steps to your email.";}
    else{msg="We've sent your reference and next steps to your WhatsApp and email.";}
    successMsg.textContent=msg;
    step1.hidden=true;
    step2.hidden=false;
    step2.classList.add('fade-in');
    window.scrollTo({top:0,behavior:'smooth'});
  });
})();
</script>
</body>
</html>
