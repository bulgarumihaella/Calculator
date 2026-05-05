# Calculator
<!DOCTYPE html>

<html lang="ro">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>Calculator Macro — MBS®</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

```
body {
  background: #0f0e0c;
  font-family: 'DM Sans', sans-serif;
  min-height: 100vh;
  padding: 28px 18px 48px;
  color: #f5f0e8;
}

.header {
  text-align: center;
  margin-bottom: 28px;
}
.header .brand {
  color: #c9a96e;
  font-size: 10px;
  letter-spacing: 4px;
  text-transform: uppercase;
  margin-bottom: 8px;
}
.header h1 {
  font-family: 'Playfair Display', serif;
  font-size: 26px;
  font-weight: 700;
  color: #f5f0e8;
}
.header .line {
  width: 36px;
  height: 1px;
  background: #c9a96e;
  margin: 10px auto 0;
}

.section-label {
  color: #8a8070;
  font-size: 10px;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  display: block;
  margin-bottom: 8px;
}

.field { margin-bottom: 18px; }

input[type="text"],
input[type="number"] {
  width: 100%;
  background: #1a1916;
  border: 1px solid #2e2c28;
  color: #f5f0e8;
  padding: 13px 16px;
  border-radius: 10px;
  font-size: 16px;
  font-family: 'DM Sans', sans-serif;
  -webkit-appearance: none;
  appearance: none;
  transition: border-color 0.15s;
}
input[type="text"]:focus,
input[type="number"]:focus {
  outline: none;
  border-color: #c9a96e;
}
input[type="number"]::-webkit-inner-spin-button { -webkit-appearance: none; }

.grid-3 {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 10px;
  margin-bottom: 18px;
}
.grid-3 .input-wrap { position: relative; }
.grid-3 input { padding-right: 32px; }
.grid-3 .unit {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  color: #5a5040;
  font-size: 11px;
  pointer-events: none;
}

.activity-list { display: flex; flex-direction: column; gap: 7px; margin-bottom: 18px; }
.activity-btn {
  background: #1a1916;
  border: 1px solid #2e2c28;
  border-radius: 10px;
  padding: 11px 14px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: border-color 0.15s, background 0.15s;
  -webkit-tap-highlight-color: transparent;
}
.activity-btn.active { border-color: #c9a96e; background: rgba(201,169,110,0.10); }
.activity-btn .act-name { color: #d4cfc5; font-size: 14px; font-weight: 500; text-align: left; }
.activity-btn.active .act-name { color: #c9a96e; }
.activity-btn .act-desc { color: #5a5040; font-size: 11px; margin-top: 2px; text-align: left; }
.activity-btn .act-factor { color: #5a5040; font-size: 12px; flex-shrink: 0; margin-left: 8px; }

.goal-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-bottom: 24px; }
.goal-btn {
  background: #1a1916;
  border: 1px solid #2e2c28;
  border-radius: 10px;
  padding: 12px 6px;
  cursor: pointer;
  text-align: center;
  transition: border-color 0.15s, background 0.15s;
  -webkit-tap-highlight-color: transparent;
}
.goal-btn.active { border-color: #c9a96e; background: rgba(201,169,110,0.10); }
.goal-btn .goal-name { color: #d4cfc5; font-size: 13px; font-weight: 500; }
.goal-btn.active .goal-name { color: #c9a96e; }
.goal-btn .goal-desc { color: #5a5040; font-size: 10px; margin-top: 4px; }

.btn-calc {
  width: 100%;
  background: #c9a96e;
  color: #0f0e0c;
  border: none;
  padding: 16px;
  border-radius: 10px;
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 1px;
  cursor: pointer;
  font-family: 'DM Sans', sans-serif;
  transition: background 0.2s;
  -webkit-tap-highlight-color: transparent;
}
.btn-calc:active { background: #b8934a; }

/* RESULTS */
#results { display: none; }

.client-name-result {
  text-align: center;
  color: #8a8070;
  font-size: 13px;
  margin-bottom: 20px;
  letter-spacing: 0.5px;
}
.client-name-result span { color: #c9a96e; }

.stats-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; margin-bottom: 20px; }
.stat-card {
  background: #1a1916;
  border: 1px solid #2e2c28;
  border-radius: 10px;
  padding: 14px 8px;
  text-align: center;
}
.stat-label { color: #5a5040; font-size: 9px; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 6px; }
.stat-value { font-family: 'Playfair Display', serif; font-size: 22px; font-weight: 700; color: #f5f0e8; }
.stat-value.highlight { color: #c9a96e; }
.stat-unit { color: #5a5040; font-size: 10px; margin-top: 3px; }

.divider {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}
.divider .line { flex: 1; height: 1px; background: #2e2c28; }
.divider span { color: #5a5040; font-size: 10px; letter-spacing: 2px; text-transform: uppercase; }

.macro-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; margin-bottom: 16px; }
.macro-card {
  border-radius: 10px;
  padding: 16px 8px;
  text-align: center;
  background: #1a1916;
}
.macro-card.p { border: 1px solid rgba(126,184,160,0.25); }
.macro-card.g { border: 1px solid rgba(232,168,124,0.25); }
.macro-card.c { border: 1px solid rgba(168,197,218,0.25); }
.macro-label { font-size: 9px; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 6px; }
.macro-card.p .macro-label { color: #7eb8a0; }
.macro-card.g .macro-label { color: #e8a87c; }
.macro-card.c .macro-label { color: #a8c5da; }
.macro-value { font-family: 'Playfair Display', serif; font-size: 24px; font-weight: 700; color: #f5f0e8; }
.macro-value span { font-size: 13px; color: #8a8070; font-family: 'DM Sans', sans-serif; }
.macro-kcal { color: #5a5040; font-size: 11px; margin-top: 4px; }

.total-bar {
  background: #1a1916;
  border: 1px solid #2e2c28;
  border-radius: 8px;
  padding: 12px 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.total-bar .lbl { color: #5a5040; font-size: 12px; }
.total-bar .val { color: #c9a96e; font-size: 14px; font-weight: 600; }

.actions { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.btn-copy {
  background: transparent;
  border: 1px solid #c9a96e;
  color: #c9a96e;
  padding: 14px;
  border-radius: 10px;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  font-family: 'DM Sans', sans-serif;
  transition: background 0.15s;
  -webkit-tap-highlight-color: transparent;
}
.btn-copy:active { background: rgba(201,169,110,0.15); }
.btn-reset {
  background: #c9a96e;
  border: none;
  color: #0f0e0c;
  padding: 14px;
  border-radius: 10px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  font-family: 'DM Sans', sans-serif;
  transition: background 0.2s;
  -webkit-tap-highlight-color: transparent;
}
.btn-reset:active { background: #b8934a; }

.footer {
  text-align: center;
  margin-top: 32px;
  color: #3a3830;
  font-size: 10px;
  letter-spacing: 1px;
}

.error-msg {
  color: #c97070;
  font-size: 12px;
  text-align: center;
  margin-top: -8px;
  margin-bottom: 12px;
  display: none;
}
```

  </style>
</head>
<body>

  <div class="header">
    <div class="brand">Mind Body Soul Nutrition®</div>
    <h1>Calculator Macro</h1>
    <div class="line"></div>
  </div>

  <!-- FORM -->

  <div id="form-section">
    <div class="field">
      <span class="section-label">Numele tău</span>
      <input type="text" id="name" placeholder="ex: Maria Ionescu" />
    </div>

```
<span class="section-label">Date personale</span>
<div class="grid-3">
  <div>
    <label class="section-label" style="font-size:9px">Greutate</label>
    <div class="input-wrap">
      <input type="number" id="weight" placeholder="65" />
      <span class="unit">kg</span>
    </div>
  </div>
  <div>
    <label class="section-label" style="font-size:9px">Înălțime</label>
    <div class="input-wrap">
      <input type="number" id="height" placeholder="165" />
      <span class="unit">cm</span>
    </div>
  </div>
  <div>
    <label class="section-label" style="font-size:9px">Vârstă</label>
    <div class="input-wrap">
      <input type="number" id="age" placeholder="35" />
      <span class="unit">ani</span>
    </div>
  </div>
</div>

<span class="section-label">Nivel activitate</span>
<div class="activity-list">
  <button class="activity-btn" data-factor="1.2" onclick="selectActivity(this)">
    <div><div class="act-name">Sedentară</div><div class="act-desc">Birou toată ziua, fără mișcare</div></div>
    <span class="act-factor">×1.2</span>
  </button>
  <button class="activity-btn active" data-factor="1.375" onclick="selectActivity(this)">
    <div><div class="act-name">Ușor activă</div><div class="act-desc">Plimbări ușoare 1–3x/săptămână</div></div>
    <span class="act-factor">×1.375</span>
  </button>
  <button class="activity-btn" data-factor="1.55" onclick="selectActivity(this)">
    <div><div class="act-name">Moderat activă</div><div class="act-desc">Sport 3–5x/săptămână</div></div>
    <span class="act-factor">×1.55</span>
  </button>
  <button class="activity-btn" data-factor="1.725" onclick="selectActivity(this)">
    <div><div class="act-name">Foarte activă</div><div class="act-desc">Sport intens zilnic / muncă fizică</div></div>
    <span class="act-factor">×1.725</span>
  </button>
  <button class="activity-btn" data-factor="1.9" onclick="selectActivity(this)">
    <div><div class="act-name">Extrem activă</div><div class="act-desc">Sport 2x/zi, muncă fizică grea</div></div>
    <span class="act-factor">×1.9</span>
  </button>
</div>

<span class="section-label">Obiectiv</span>
<div class="goal-grid">
  <button class="goal-btn active" data-delta="-400" onclick="selectGoal(this)">
    <div class="goal-name">Slăbire</div>
    <div class="goal-desc">Deficit 300–500 kcal</div>
  </button>
  <button class="goal-btn" data-delta="0" onclick="selectGoal(this)">
    <div class="goal-name">Menținere</div>
    <div class="goal-desc">Exact TDEE</div>
  </button>
  <button class="goal-btn" data-delta="250" onclick="selectGoal(this)">
    <div class="goal-name">Masă musculară</div>
    <div class="goal-desc">Surplus 200–300 kcal</div>
  </button>
</div>

<div class="error-msg" id="error">Te rog completează greutatea, înălțimea și vârsta.</div>
<button class="btn-calc" onclick="calculate()">Calculează →</button>
```

  </div>

  <!-- RESULTS -->

  <div id="results">
    <div class="client-name-result" id="result-name"></div>

```
<div class="stats-grid">
  <div class="stat-card">
    <div class="stat-label">BMR</div>
    <div class="stat-value" id="r-bmr">—</div>
    <div class="stat-unit">kcal</div>
  </div>
  <div class="stat-card">
    <div class="stat-label">TDEE</div>
    <div class="stat-value" id="r-tdee">—</div>
    <div class="stat-unit">kcal</div>
  </div>
  <div class="stat-card">
    <div class="stat-label">Țintă</div>
    <div class="stat-value highlight" id="r-target">—</div>
    <div class="stat-unit">kcal/zi</div>
  </div>
</div>

<div class="divider">
  <div class="line"></div>
  <span>Macro-uri</span>
  <div class="line"></div>
</div>

<div class="macro-grid">
  <div class="macro-card p">
    <div class="macro-label">Proteine</div>
    <div class="macro-value" id="r-protein">—<span>g</span></div>
    <div class="macro-kcal" id="r-protein-kcal">— kcal</div>
  </div>
  <div class="macro-card g">
    <div class="macro-label">Grăsimi</div>
    <div class="macro-value" id="r-fat">—<span>g</span></div>
    <div class="macro-kcal" id="r-fat-kcal">— kcal</div>
  </div>
  <div class="macro-card c">
    <div class="macro-label">Carbohidrați</div>
    <div class="macro-value" id="r-carbs">—<span>g</span></div>
    <div class="macro-kcal" id="r-carbs-kcal">— kcal</div>
  </div>
</div>

<div class="total-bar">
  <span class="lbl">Total calculat</span>
  <span class="val" id="r-total">— kcal</span>
</div>

<div class="actions">
  <button class="btn-copy" onclick="copyResults()" id="btn-copy">Copiază rezultatele</button>
  <button class="btn-reset" onclick="reset()">Clientă nouă →</button>
</div>
```

  </div>

  <div class="footer">MBS® Program 1:1 · mindbodysoulnutrition.com</div>

  <script>
    let selectedFactor = 1.375;
    let selectedDelta = -400;
    let lastResult = null;

    function selectActivity(btn) {
      document.querySelectorAll('.activity-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      selectedFactor = parseFloat(btn.dataset.factor);
    }

    function selectGoal(btn) {
      document.querySelectorAll('.goal-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      selectedDelta = parseFloat(btn.dataset.delta);
    }

    function calculate() {
      const w = parseFloat(document.getElementById('weight').value);
      const h = parseFloat(document.getElementById('height').value);
      const a = parseFloat(document.getElementById('age').value);
      const name = document.getElementById('name').value.trim();
      const err = document.getElementById('error');

      if (!w || !h || !a) {
        err.style.display = 'block';
        return;
      }
      err.style.display = 'none';

      const bmr = Math.round(10 * w + 6.25 * h - 5 * a - 161);
      const tdee = Math.round(bmr * selectedFactor);
      const target = tdee + selectedDelta;
      const protein_g = Math.round(w * 1.8);
      const fat_g = Math.round(w * 1.05);
      const protein_kcal = protein_g * 4;
      const fat_kcal = fat_g * 9;
      const carbs_g = Math.round((target - protein_kcal - fat_kcal) / 4);
      const total = protein_kcal + fat_kcal + carbs_g * 4;

      lastResult = { name, bmr, tdee, target, protein_g, fat_g, carbs_g, total };

      document.getElementById('result-name').innerHTML = name
        ? `Rezultate pentru <span>${name}</span>`
        : 'Rezultatele tale';

      document.getElementById('r-bmr').textContent = bmr;
      document.getElementById('r-tdee').textContent = tdee;
      document.getElementById('r-target').textContent = target;
      document.getElementById('r-protein').innerHTML = `${protein_g}<span>g</span>`;
      document.getElementById('r-fat').innerHTML = `${fat_g}<span>g</span>`;
      document.getElementById('r-carbs').innerHTML = `${carbs_g}<span>g</span>`;
      document.getElementById('r-protein-kcal').textContent = `${protein_kcal} kcal`;
      document.getElementById('r-fat-kcal').textContent = `${fat_kcal} kcal`;
      document.getElementById('r-carbs-kcal').textContent = `${carbs_g * 4} kcal`;
      document.getElementById('r-total').textContent = `${total} kcal`;

      document.getElementById('form-section').style.display = 'none';
      document.getElementById('results').style.display = 'block';
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function copyResults() {
      if (!lastResult) return;
      const r = lastResult;
      const text = `MBS® — ${r.name || 'Clientă'}
━━━━━━━━━━━━━━━━━━━━
BMR: ${r.bmr} kcal
TDEE: ${r.tdee} kcal
Țintă zilnică: ${r.target} kcal
━━━━━━━━━━━━━━━━━━━━
Proteine: ${r.protein_g}g (${r.protein_g * 4} kcal)
Grăsimi: ${r.fat_g}g (${r.fat_g * 9} kcal)
Carbohidrați: ${r.carbs_g}g (${r.carbs_g * 4} kcal)
━━━━━━━━━━━━━━━━━━━━
Total: ${r.total} kcal
Calculator MBS® · mindbodysoulnutrition.com`;

      navigator.clipboard.writeText(text).then(() => {
        const btn = document.getElementById('btn-copy');
        btn.textContent = '✓ Copiat!';
        setTimeout(() => btn.textContent = 'Copiază rezultatele', 2000);
      });
    }

    function reset() {
      document.getElementById('form-section').style.display = 'block';
      document.getElementById('results').style.display = 'none';
      document.getElementById('name').value = '';
      document.getElementById('weight').value = '';
      document.getElementById('height').value = '';
      document.getElementById('age').value = '';
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  </script>

</body>
</html>