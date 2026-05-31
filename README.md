<div align="center">

<br>

# 🤖 Auto Quest Completer

**Run once in your browser console — all quests complete automatically, one by one, with live progress shown.**

<br>

![Brave](https://img.shields.io/badge/Brave_Browser-FB542B?style=for-the-badge&logo=brave&logoColor=white)
![PTB](https://img.shields.io/badge/PTB_App-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

</div>

---

## ⚠️ Before You Start

> **Accept all quests manually first** before running the script.
> The script will not work if quests are not accepted beforehand.

---

## 🚀 How to Use

<details>
<summary><b>🦁 Brave Browser — Click to expand steps</b></summary>

<br>

| Step | Action |
|------|--------|
| **1** | Open the page where your quests are listed |
| **2** | Accept **all quests** manually on the page |
| **3** | Right-click anywhere → click **Inspect** |
| **4** | Go to the **Console** tab in DevTools |
| **5** | Type `allow pasting` in the console and press **Enter** |
| **6** | Paste the full script and press **Enter** |
| **7** | Watch quests complete one by one with live progress |

</details>

<details>
<summary><b>🖥️ PTB App (Desktop) — Click to expand steps</b></summary>

<br>

| Step | Action |
|------|--------|
| **1** | Open the PTB app |
| **2** | Accept **all quests** manually |
| **3** | Press `Ctrl + Shift + I` (or `Cmd + Option + I` on Mac) to open DevTools |
| **4** | Go to the **Console** tab |
| **5** | Type `allow pasting` in the console and press **Enter** |
| **6** | Paste the full script and press **Enter** |
| **7** | Quests start completing automatically — wait for 100% |

</details>

---

## 📊 Progress Tracking

While the script runs, you will see live updates in the console:

```
Starting auto-complete for 5 quests...
✓ Quest 1 completed... [20%]
✓ Quest 2 completed... [40%]
✓ Quest 3 completed... [60%]
✓ Quest 4 completed... [80%]
✓ Quest 5 completed... [100%]
🎉 All quests done!
```

---

## 📜 The Script

<details>
<summary><b>👆 Click to expand — copy and paste into console</b></summary>

<br>

```javascript
(async () => {
  // Auto Quest Completer — paste into browser console
  // Make sure all quests are accepted before running

  const delay = (ms) => new Promise((res) => setTimeout(res, ms));

  const quests = document.querySelectorAll('.quest-item');
  const total = quests.length;

  if (total === 0) {
    console.warn('No quests found. Make sure you accepted them first.');
    return;
  }

  console.log(`Starting auto-complete for ${total} quests...`);

  for (let i = 0; i < total; i++) {
    const quest = quests[i];
    const btn = quest.querySelector('button.complete, .claim-btn, [data-action="complete"]');

    if (btn) {
      btn.click();
      await delay(1200);
    }

    const pct = Math.round(((i + 1) / total) * 100);
    console.log(`✓ Quest ${i + 1} completed... [${pct}%]`);
  }

  console.log('🎉 All quests done!');
})();
```

</details>

---

## ❗ Important Rules

| | Rule | Why |
|-|------|-----|
| ✅ | Accept all quests **before** running | Script only completes accepted quests |
| 🚫 | Do **not** close the page or app while running | Closing mid-run will stop the process |
| 🔁 | Run the script **only once** | Running it again is unnecessary once done |
| ⏳ | Wait for **100%** before leaving | Let it finish fully before navigating away |

---

## 💡 Tips

- Keep the browser/app window **active and visible** while the script runs
- If something goes wrong, refresh the page, re-accept quests, and try again
- Only use this script on your own account

---

<div align="center">

Made for **Brave Browser** & **PTB App** &nbsp;·&nbsp; Use responsibly

</div>
