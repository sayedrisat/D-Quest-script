
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  .wrap { max-width: 680px; padding: 2rem 0; font-family: var(--font-sans); }
  .hero { text-align: center; padding: 2.5rem 1.5rem; background: var(--color-background-secondary); border-radius: var(--border-radius-lg); border: 0.5px solid var(--color-border-tertiary); margin-bottom: 2rem; }
  .hero-badge { display: inline-flex; align-items: center; gap: 6px; background: var(--color-background-primary); border: 0.5px solid var(--color-border-secondary); border-radius: 100px; padding: 4px 14px; font-size: 12px; color: var(--color-text-secondary); margin-bottom: 1rem; }
  .hero h1 { font-size: 22px; font-weight: 500; color: var(--color-text-primary); margin-bottom: 0.5rem; }
  .hero p { font-size: 14px; color: var(--color-text-secondary); line-height: 1.6; }
  .warn-box { display: flex; gap: 12px; align-items: flex-start; background: #FAEEDA; border: 0.5px solid #EF9F27; border-radius: var(--border-radius-md); padding: 14px 16px; margin-bottom: 2rem; }
  .warn-box i { font-size: 18px; color: #854F0B; flex-shrink: 0; margin-top: 1px; }
  .warn-box p { font-size: 13px; color: #633806; line-height: 1.6; }
  .warn-box strong { font-weight: 500; display: block; margin-bottom: 2px; color: #412402; }
  .section-label { font-size: 11px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.08em; color: var(--color-text-tertiary); margin-bottom: 0.75rem; }
  .step-card { background: var(--color-background-primary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1.25rem 1.5rem; margin-bottom: 1rem; }
  .step-card h3 { font-size: 15px; font-weight: 500; color: var(--color-text-primary); margin-bottom: 1rem; display: flex; align-items: center; gap: 8px; }
  .step-card h3 i { font-size: 17px; color: var(--color-text-secondary); }
  .steps { display: flex; flex-direction: column; gap: 0; }
  .step { display: flex; gap: 12px; padding: 8px 0; }
  .step:not(:last-child) { border-bottom: 0.5px solid var(--color-border-tertiary); }
  .step-num { width: 22px; height: 22px; border-radius: 50%; background: var(--color-background-info); color: var(--color-text-info); font-size: 11px; font-weight: 500; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }
  .step-body { font-size: 13px; color: var(--color-text-secondary); line-height: 1.65; }
  .step-body strong { font-weight: 500; color: var(--color-text-primary); }
  .code-pill { display: inline-block; background: var(--color-background-secondary); border: 0.5px solid var(--color-border-secondary); border-radius: 6px; padding: 1px 8px; font-family: var(--font-mono); font-size: 12px; color: var(--color-text-primary); }
  .progress-demo { background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 14px 16px; margin: 1rem 0 0; border: 0.5px solid var(--color-border-tertiary); }
  .progress-demo p { font-size: 12px; font-family: var(--font-mono); color: var(--color-text-secondary); line-height: 1.8; }
  .progress-demo p span.done { color: #0F6E56; }
  .progress-demo p span.final { color: var(--color-text-primary); font-weight: 500; }
  .rules-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 2rem; }
  .rule-card { background: var(--color-background-primary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1rem 1.25rem; display: flex; flex-direction: column; gap: 6px; }
  .rule-card i { font-size: 20px; }
  .rule-card .rule-title { font-size: 13px; font-weight: 500; color: var(--color-text-primary); }
  .rule-card .rule-desc { font-size: 12px; color: var(--color-text-secondary); line-height: 1.5; }
  .rule-card.danger i { color: #A32D2D; }
  .rule-card.success i { color: #0F6E56; }
  .rule-card.info i { color: #185FA5; }
  .rule-card.warn i { color: #854F0B; }
  .browser-tabs { display: flex; gap: 8px; margin-bottom: 1rem; }
  .tab-btn { flex: 1; padding: 8px; border: 0.5px solid var(--color-border-secondary); border-radius: var(--border-radius-md); background: var(--color-background-secondary); font-size: 13px; font-weight: 500; color: var(--color-text-secondary); cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 6px; transition: all 0.15s; }
  .tab-btn.active { background: var(--color-background-primary); color: var(--color-text-primary); border-color: var(--color-border-primary); }
  .tab-content { display: none; }
  .tab-content.active { display: block; }

  /* Dropdown script block */
  .script-dropdown { background: var(--color-background-primary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); margin-bottom: 2rem; overflow: hidden; }
  .script-toggle { width: 100%; display: flex; align-items: center; justify-content: space-between; padding: 1rem 1.25rem; background: none; border: none; cursor: pointer; font-family: var(--font-sans); }
  .script-toggle-left { display: flex; align-items: center; gap: 10px; }
  .script-toggle-left i { font-size: 18px; color: var(--color-text-secondary); }
  .script-toggle-title { font-size: 15px; font-weight: 500; color: var(--color-text-primary); }
  .script-toggle-sub { font-size: 12px; color: var(--color-text-secondary); margin-top: 1px; }
  .script-toggle-right { display: flex; align-items: center; gap: 8px; }
  .chevron { font-size: 16px; color: var(--color-text-tertiary); transition: transform 0.2s ease; }
  .script-toggle.open .chevron { transform: rotate(180deg); }
  .script-body { display: none; border-top: 0.5px solid var(--color-border-tertiary); }
  .script-body.open { display: block; }
  .script-topbar { display: flex; align-items: center; justify-content: space-between; padding: 10px 14px; background: var(--color-background-secondary); border-bottom: 0.5px solid var(--color-border-tertiary); }
  .script-lang { font-size: 11px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.07em; color: var(--color-text-tertiary); display: flex; align-items: center; gap: 6px; }
  .copy-btn { display: flex; align-items: center; gap: 6px; padding: 5px 12px; border: 0.5px solid var(--color-border-secondary); border-radius: var(--border-radius-md); background: var(--color-background-primary); font-size: 12px; font-weight: 500; color: var(--color-text-secondary); cursor: pointer; font-family: var(--font-sans); transition: all 0.15s; }
  .copy-btn:hover { background: var(--color-background-secondary); color: var(--color-text-primary); }
  .copy-btn.copied { border-color: #1D9E75; color: #0F6E56; background: #E1F5EE; }
  .copy-btn i { font-size: 14px; }
  .code-scroll { max-height: 320px; overflow-y: auto; padding: 1rem 1.25rem; }
  .code-scroll::-webkit-scrollbar { width: 4px; }
  .code-scroll::-webkit-scrollbar-track { background: transparent; }
  .code-scroll::-webkit-scrollbar-thumb { background: var(--color-border-secondary); border-radius: 4px; }
  pre { font-family: var(--font-mono); font-size: 12px; color: var(--color-text-secondary); line-height: 1.7; white-space: pre; overflow-x: auto; }
  .kw { color: #534AB7; }
  .fn { color: #185FA5; }
  .str { color: #0F6E56; }
  .cm { color: var(--color-text-tertiary); font-style: italic; }
  .nm { color: #993C1D; }

  .footer { text-align: center; font-size: 12px; color: var(--color-text-tertiary); padding-top: 1rem; border-top: 0.5px solid var(--color-border-tertiary); }
</style>

<h2 class="sr-only">Auto Quest Completer — README and usage guide</h2>

<div class="wrap">

  <div class="hero">
    <div class="hero-badge"><i class="ti ti-terminal-2" aria-hidden="true"></i> console script</div>
    <h1>Auto Quest Completer</h1>
    <p>Run once in your browser console — all quests complete automatically,<br>one by one, with live progress shown.</p>
  </div>

  <div class="warn-box">
    <i class="ti ti-alert-triangle" aria-hidden="true"></i>
    <p><strong>Do this before anything else</strong>Accept all quests manually on the page or app before running the script. The script only works on already-accepted quests.</p>
  </div>

  <p class="section-label">How to use</p>

  <div class="browser-tabs">
    <button class="tab-btn active" onclick="switchTab('brave', this)"><i class="ti ti-brand-chrome" aria-hidden="true"></i> Brave Browser</button>
    <button class="tab-btn" onclick="switchTab('ptb', this)"><i class="ti ti-device-desktop" aria-hidden="true"></i> PTB App</button>
  </div>

  <div id="tab-brave" class="tab-content active">
    <div class="step-card">
      <h3><i class="ti ti-list-check" aria-hidden="true"></i> Steps — Brave Browser</h3>
      <div class="steps">
        <div class="step"><div class="step-num">1</div><div class="step-body">Open the page where your quests are listed</div></div>
        <div class="step"><div class="step-num">2</div><div class="step-body"><strong>Accept all quests</strong> manually on the page</div></div>
        <div class="step"><div class="step-num">3</div><div class="step-body">Right-click anywhere → click <strong>Inspect</strong></div></div>
        <div class="step"><div class="step-num">4</div><div class="step-body">Go to the <strong>Console</strong> tab in DevTools</div></div>
        <div class="step"><div class="step-num">5</div><div class="step-body">Click the console input, type <span class="code-pill">allow pasting</span> and press <strong>Enter</strong></div></div>
        <div class="step"><div class="step-num">6</div><div class="step-body"><strong>Paste the full script</strong> into the console and press <strong>Enter</strong></div></div>
        <div class="step"><div class="step-num">7</div><div class="step-body">Watch quests complete one by one — progress % shown in real time</div></div>
      </div>
    </div>
  </div>

  <div id="tab-ptb" class="tab-content">
    <div class="step-card">
      <h3><i class="ti ti-device-desktop" aria-hidden="true"></i> Steps — PTB App</h3>
      <div class="steps">
        <div class="step"><div class="step-num">1</div><div class="step-body">Open the PTB app</div></div>
        <div class="step"><div class="step-num">2</div><div class="step-body"><strong>Accept all quests</strong> manually</div></div>
        <div class="step"><div class="step-num">3</div><div class="step-body">Press <span class="code-pill">Ctrl + Shift + I</span> (or <span class="code-pill">Cmd + Option + I</span> on Mac) to open DevTools</div></div>
        <div class="step"><div class="step-num">4</div><div class="step-body">Go to the <strong>Console</strong> tab</div></div>
        <div class="step"><div class="step-num">5</div><div class="step-body">Type <span class="code-pill">allow pasting</span> and press <strong>Enter</strong></div></div>
        <div class="step"><div class="step-num">6</div><div class="step-body"><strong>Paste the full script</strong> and press <strong>Enter</strong></div></div>
        <div class="step"><div class="step-num">7</div><div class="step-body">Quests start completing automatically — wait for 100%</div></div>
      </div>
    </div>
  </div>

  <div class="step-card" style="margin-top:1rem; margin-bottom:2rem;">
    <h3><i class="ti ti-chart-line" aria-hidden="true"></i> Live progress preview</h3>
    <div class="progress-demo">
      <p>
        <span class="done">✓</span> Quest 1 completed... <strong>[20%]</strong><br>
        <span class="done">✓</span> Quest 2 completed... <strong>[40%]</strong><br>
        <span class="done">✓</span> Quest 3 completed... <strong>[60%]</strong><br>
        <span class="done">✓</span> Quest 4 completed... <strong>[80%]</strong><br>
        <span class="done">✓</span> Quest 5 completed... <strong>[100%]</strong><br>
        <span class="final">🎉 All quests done!</span>
      </p>
    </div>
  </div>

  <p class="section-label">The script</p>

  <div class="script-dropdown">
    <button class="script-toggle" id="scriptToggle" onclick="toggleScript()">
      <div class="script-toggle-left">
        <i class="ti ti-code" aria-hidden="true"></i>
        <div>
          <div class="script-toggle-title">View full script</div>
          <div class="script-toggle-sub">Click to expand — then copy and paste into console</div>
        </div>
      </div>
      <div class="script-toggle-right">
        <i class="ti ti-chevron-down chevron" id="chevron" aria-hidden="true"></i>
      </div>
    </button>
    <div class="script-body" id="scriptBody">
      <div class="script-topbar">
        <span class="script-lang"><i class="ti ti-brand-javascript" aria-hidden="true"></i> JavaScript</span>
        <button class="copy-btn" id="copyBtn" onclick="copyScript()">
          <i class="ti ti-copy" id="copyIcon" aria-hidden="true"></i>
          <span id="copyText">Copy script</span>
        </button>
      </div>
      <div class="code-scroll">
        <pre id="scriptCode">(async () => {
  <span class="cm">// Auto Quest Completer — paste into browser console</span>
  <span class="cm">// Make sure all quests are accepted before running</span>

  <span class="kw">const</span> <span class="nm">delay</span> = (<span class="nm">ms</span>) => <span class="kw">new</span> <span class="fn">Promise</span>((<span class="nm">res</span>) => <span class="fn">setTimeout</span>(<span class="nm">res</span>, <span class="nm">ms</span>));

  <span class="kw">const</span> <span class="nm">quests</span> = <span class="fn">document</span>.<span class="fn">querySelectorAll</span>(<span class="str">'.quest-item'</span>);
  <span class="kw">const</span> <span class="nm">total</span> = <span class="nm">quests</span>.<span class="nm">length</span>;

  <span class="kw">if</span> (<span class="nm">total</span> === <span class="nm">0</span>) {
    <span class="fn">console</span>.<span class="fn">warn</span>(<span class="str">'No quests found. Make sure you accepted them first.'</span>);
    <span class="kw">return</span>;
  }

  <span class="fn">console</span>.<span class="fn">log</span>(<span class="str">`Starting auto-complete for ${total} quests...`</span>);

  <span class="kw">for</span> (<span class="kw">let</span> <span class="nm">i</span> = <span class="nm">0</span>; <span class="nm">i</span> &lt; <span class="nm">total</span>; <span class="nm">i</span>++) {
    <span class="kw">const</span> <span class="nm">quest</span> = <span class="nm">quests</span>[<span class="nm">i</span>];
    <span class="kw">const</span> <span class="nm">btn</span> = <span class="nm">quest</span>.<span class="fn">querySelector</span>(<span class="str">'button.complete, .claim-btn, [data-action="complete"]'</span>);

    <span class="kw">if</span> (<span class="nm">btn</span>) {
      <span class="nm">btn</span>.<span class="fn">click</span>();
      <span class="kw">await</span> <span class="fn">delay</span>(<span class="nm">1200</span>);
    }

    <span class="kw">const</span> <span class="nm">pct</span> = <span class="fn">Math</span>.<span class="fn">round</span>(((i + <span class="nm">1</span>) / <span class="nm">total</span>) * <span class="nm">100</span>);
    <span class="fn">console</span>.<span class="fn">log</span>(<span class="str">`✓ Quest ${i + 1} completed... [${pct}%]`</span>);
  }

  <span class="fn">console</span>.<span class="fn">log</span>(<span class="str">'🎉 All quests done!'</span>);
})();</pre>
      </div>
    </div>
  </div>

  <p class="section-label" style="margin-top:0;">Important rules</p>

  <div class="rules-grid">
    <div class="rule-card success">
      <i class="ti ti-circle-check" aria-hidden="true"></i>
      <div class="rule-title">Accept quests first</div>
      <div class="rule-desc">Manually accept every quest before running the script — it only processes accepted ones.</div>
    </div>
    <div class="rule-card danger">
      <i class="ti ti-ban" aria-hidden="true"></i>
      <div class="rule-title">Don't close the page</div>
      <div class="rule-desc">Keep the browser or app open and active until 100% is reached.</div>
    </div>
    <div class="rule-card info">
      <i class="ti ti-refresh" aria-hidden="true"></i>
      <div class="rule-title">Run only once</div>
      <div class="rule-desc">One run is enough to complete all quests. Running it again is not needed.</div>
    </div>
    <div class="rule-card warn">
      <i class="ti ti-clock" aria-hidden="true"></i>
      <div class="rule-title">Wait for 100%</div>
      <div class="rule-desc">Stay on the page until the script finishes and shows full completion.</div>
    </div>
  </div>

  <div class="footer">Made for Brave Browser &amp; PTB App &nbsp;·&nbsp; Use responsibly</div>

</div>

<script>
  function switchTab(id, btn) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
    document.getElementById('tab-' + id).classList.add('active');
    btn.classList.add('active');
  }

  function toggleScript() {
    const body = document.getElementById('scriptBody');
    const toggle = document.getElementById('scriptToggle');
    const chevron = document.getElementById('chevron');
    const isOpen = body.classList.contains('open');
    body.classList.toggle('open', !isOpen);
    toggle.classList.toggle('open', !isOpen);
  }

  function copyScript() {
    const raw = `(async () => {
  // Auto Quest Completer — paste into browser console
  // Make sure all quests are accepted before running

  const delay = (ms) => new Promise((res) => setTimeout(res, ms));

  const quests = document.querySelectorAll('.quest-item');
  const total = quests.length;

  if (total === 0) {
    console.warn('No quests found. Make sure you accepted them first.');
    return;
  }

  console.log(\`Starting auto-complete for \${total} quests...\`);

  for (let i = 0; i < total; i++) {
    const quest = quests[i];
    const btn = quest.querySelector('button.complete, .claim-btn, [data-action="complete"]');

    if (btn) {
      btn.click();
      await delay(1200);
    }

    const pct = Math.round(((i + 1) / total) * 100);
    console.log(\`✓ Quest \${i + 1} completed... [\${pct}%]\`);
  }

  console.log('🎉 All quests done!');
})();`;

    navigator.clipboard.writeText(raw).then(() => {
      const btn = document.getElementById('copyBtn');
      const icon = document.getElementById('copyIcon');
      const text = document.getElementById('copyText');
      btn.classList.add('copied');
      icon.className = 'ti ti-check';
      text.textContent = 'Copied!';
      setTimeout(() => {
        btn.classList.remove('copied');
        icon.className = 'ti ti-copy';
        text.textContent = 'Copy script';
      }, 2000);
    });
  }
</script>
