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
delete window.$;
let wpRequire = webpackChunkdiscord_app.push([[Symbol()], {}, r => r]);
webpackChunkdiscord_app.pop();

let ApplicationStreamingStore = Object.values(wpRequire.c).find(x => x?.exports?.A?.__proto__?.getStreamerActiveStreamMetadata).exports.A;
let RunningGameStore = Object.values(wpRequire.c).find(x => x?.exports?.Ay?.getRunningGames).exports.Ay;
let QuestsStore = Object.values(wpRequire.c).find(x => x?.exports?.A?.__proto__?.getQuest).exports.A;
let ChannelStore = Object.values(wpRequire.c).find(x => x?.exports?.A?.__proto__?.getAllThreadsForParent).exports.A;
let GuildChannelStore = Object.values(wpRequire.c).find(x => x?.exports?.Ay?.getSFWDefaultChannel).exports.Ay;
let FluxDispatcher = Object.values(wpRequire.c).find(x => x?.exports?.h?.__proto__?.flushWaitQueue).exports.h;
let api = Object.values(wpRequire.c).find(x => x?.exports?.Bo?.get).exports.Bo;

const supportedTasks = ["WATCH_VIDEO", "PLAY_ON_DESKTOP", "STREAM_ON_DESKTOP", "PLAY_ACTIVITY", "WATCH_VIDEO_ON_MOBILE"]
let quests = [...QuestsStore.quests.values()].filter(x => x.userStatus?.enrolledAt && !x.userStatus?.completedAt && new Date(x.config.expiresAt).getTime() > Date.now() && supportedTasks.find(y => Object.keys((x.config.taskConfig ?? x.config.taskConfigV2).tasks).includes(y)))
let isApp = typeof DiscordNative !== "undefined"
if(quests.length === 0) {
	console.log("You don't have any uncompleted quests!")
} else {
	let doJob = function() {
		const quest = quests.pop()
		if(!quest) return

		const pid = Math.floor(Math.random() * 30000) + 1000
		
		const applicationId = quest.config.application.id
		const applicationName = quest.config.application.name
		const questName = quest.config.messages.questName
		const taskConfig = quest.config.taskConfig ?? quest.config.taskConfigV2
		const taskName = supportedTasks.find(x => taskConfig.tasks[x] != null)
		const secondsNeeded = taskConfig.tasks[taskName].target
		let secondsDone = quest.userStatus?.progress?.[taskName]?.value ?? 0

		if(taskName === "WATCH_VIDEO" || taskName === "WATCH_VIDEO_ON_MOBILE") {
			const speed = 7
			const enrolledAt = new Date(quest.userStatus.enrolledAt).getTime()
			let completed = false
			let fn = async () => {			
				while(true) {
					const remaining = Math.min(speed, secondsNeeded - secondsDone)
					await new Promise(resolve => setTimeout(resolve, remaining * 1000))

					const timestamp = secondsDone + speed
					const res = await api.post({url: `/quests/${quest.id}/video-progress`, body: {timestamp: Math.min(secondsNeeded, timestamp + Math.random())}})
					completed = res.body.completed_at != null
					secondsDone = Math.min(secondsNeeded, timestamp)

					if(timestamp >= secondsNeeded) {
						break
					}
				}
				if(!completed) {
					await api.post({url: `/quests/${quest.id}/video-progress`, body: {timestamp: secondsNeeded}})
				}
				console.log("Quest completed!")
				doJob()
			}
			fn()
			console.log(`Spoofing video for ${questName}.`)
		} else if(taskName === "PLAY_ON_DESKTOP") {
			if(!isApp) {
				console.log("This no longer works in browser for non-video quests. Use the discord desktop app to complete the", questName, "quest!")
			} else {
				api.get({url: `/applications/public?application_ids=${applicationId}`}).then(res => {
					const appData = res.body[0]
					const exeName = appData.executables?.find(x => x.os === "win32")?.name?.replace(">","") ?? appData.name.replace(/[\/\\:*?"<>|]/g, "")
					
					const fakeGame = {
						cmdLine: `C:\\Program Files\\${appData.name}\\${exeName}`,
						exeName,
						exePath: `c:/program files/${appData.name.toLowerCase()}/${exeName}`,
						hidden: false,
						isLauncher: false,
						id: applicationId,
						name: appData.name,
						pid: pid,
						pidPath: [pid],
						processName: appData.name,
						start: Date.now(),
					}
					const realGames = RunningGameStore.getRunningGames()
					const fakeGames = [fakeGame]
					const realGetRunningGames = RunningGameStore.getRunningGames
					const realGetGameForPID = RunningGameStore.getGameForPID
					RunningGameStore.getRunningGames = () => fakeGames
					RunningGameStore.getGameForPID = (pid) => fakeGames.find(x => x.pid === pid)
					FluxDispatcher.dispatch({type: "RUNNING_GAMES_CHANGE", removed: realGames, added: [fakeGame], games: fakeGames})
					
					let fn = data => {
						let progress = quest.config.configVersion === 1 ? data.userStatus.streamProgressSeconds : Math.floor(data.userStatus.progress.PLAY_ON_DESKTOP.value)
						console.log(`Quest progress: ${progress}/${secondsNeeded}`)
						
						if(progress >= secondsNeeded) {
							console.log("Quest completed!")
							
							RunningGameStore.getRunningGames = realGetRunningGames
							RunningGameStore.getGameForPID = realGetGameForPID
							FluxDispatcher.dispatch({type: "RUNNING_GAMES_CHANGE", removed: [fakeGame], added: [], games: []})
							FluxDispatcher.unsubscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
							
							doJob()
						}
					}
					FluxDispatcher.subscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
					
					console.log(`Spoofed your game to ${applicationName}. Wait for ${Math.ceil((secondsNeeded - secondsDone) / 60)} more minutes.`)
				})
			}
		} else if(taskName === "STREAM_ON_DESKTOP") {
			if(!isApp) {
				console.log("This no longer works in browser for non-video quests. Use the discord desktop app to complete the", questName, "quest!")
			} else {
				let realFunc = ApplicationStreamingStore.getStreamerActiveStreamMetadata
				ApplicationStreamingStore.getStreamerActiveStreamMetadata = () => ({
					id: applicationId,
					pid,
					sourceName: null
				})
				
				let fn = data => {
					let progress = quest.config.configVersion === 1 ? data.userStatus.streamProgressSeconds : Math.floor(data.userStatus.progress.STREAM_ON_DESKTOP.value)
					console.log(`Quest progress: ${progress}/${secondsNeeded}`)
					
					if(progress >= secondsNeeded) {
						console.log("Quest completed!")
						
						ApplicationStreamingStore.getStreamerActiveStreamMetadata = realFunc
						FluxDispatcher.unsubscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
						
						doJob()
					}
				}
				FluxDispatcher.subscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
				
				console.log(`Spoofed your stream to ${applicationName}. Stream any window in vc for ${Math.ceil((secondsNeeded - secondsDone) / 60)} more minutes.`)
				console.log("Remember that you need at least 1 other person to be in the vc!")
			}
		} else if(taskName === "PLAY_ACTIVITY") {
			const channelId = ChannelStore.getSortedPrivateChannels()[0]?.id ?? Object.values(GuildChannelStore.getAllGuilds()).find(x => x != null && x.VOCAL.length > 0).VOCAL[0].channel.id
			const streamKey = `call:${channelId}:1`
			
			let fn = async () => {
				console.log("Completing quest", questName, "-", quest.config.messages.questName)
				
				while(true) {
					const res = await api.post({url: `/quests/${quest.id}/heartbeat`, body: {stream_key: streamKey, terminal: false}})
					const progress = res.body.progress.PLAY_ACTIVITY.value
					console.log(`Quest progress: ${progress}/${secondsNeeded}`)
					
					await new Promise(resolve => setTimeout(resolve, 20 * 1000))
					
					if(progress >= secondsNeeded) {
						await api.post({url: `/quests/${quest.id}/heartbeat`, body: {stream_key: streamKey, terminal: true}})
						break
					}
				}
				
				console.log("Quest completed!")
				doJob()
			}
			fn()
		}
	}
	doJob()
}
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
