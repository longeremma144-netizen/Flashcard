# Recall — your personal flashcard app

No dependencies, subscriptions, build tools, or external libraries. This is a static HTML/CSS/JavaScript PWA. Two small starter decks are included. Import your full decks using the Import deck button.

## 1. Run on your Mac

1. Unzip Recall.zip. Open the Recall folder in VS Code (File > Open Folder).
2. In VS Code choose Terminal > New Terminal. Run `python3 -m http.server 8000`.
3. Open http://localhost:8000 in Safari or Chrome. Leave the terminal running while testing. Ctrl+C stops it.

If Python is not installed, install Python 3 from python.org, or use the VS Code Live Server extension. No npm install is required. Opening index.html directly may show the app, but reliable local storage and offline installation require a proper web origin.

## 2. Install on iPad (free HTTPS hosting)

One option is GitHub Pages. Follow the account/age requirements of the service and ask a parent to help if necessary. Do not upload your personal decks or backups to a public repository.

1. Sign in to github.com and create a new public repository named `recall`.
2. Upload the **contents** of the Recall folder (index.html, style.css, app.js, manifest.json, sw.js and both icons). The files must be at the root of the repository, not inside another folder. README.md is optional.
3. Commit changes. Open Settings > Pages. Select Deploy from a branch, main, / (root), then Save.
4. When Pages displays the published address, open that address on iPad Safari. It normally looks like `https://YOUR-USERNAME.github.io/recall/`.
5. Tap Share > Add to Home Screen (you may have to scroll the share menu). Enable Open as Web App if offered, then Add.
6. Launch the installed app while online. In Settings check that the offline cache is installed. Test by turning on airplane mode, closing and reopening the app. Turn airplane mode off afterwards.

Mac localhost and the hosted iPad app are separate storage locations. If you have already made cards on the Mac, export a complete backup from Settings and restore that file on the installed iPad app. Browser and home-screen storage may also be separate on some iPadOS versions.

## 3. Everyday use

- **Import:** paste a tab-separated deck, one front/back pair per line. Preview, remove incorrect cards, choose a destination, then import. Exact duplicates are skipped. Other accepted separators are spaced `::`, `|`, `—`, and `-`.
- **Folders:** use names such as `Speech/Impromptu` and `Debate/IR`; selecting a parent includes its descendants. Edit a deck to rename it or move it.
- **Review:** open a deck, select mode, direction, due/all and session size. Tap a flashcard to reveal. Swipe left for Again or right for Good on a revealed flashcard. Written recall is self-graded to accommodate paraphrases; multiple choice generates distractors from the same deck, with up to four options.
- **Keyboard:** Space flips flashcards; 1/2/3/4 = Again/Hard/Good/Easy. Left/right arrow = Again/Good on a revealed flashcard. Shortcuts are disabled while typing.
- **Spaced repetition:** a simple interval-based algorithm (not FSRS or Anki SM-2). Again schedules 10 minutes and up to two immediate retries in the current session; Hard uses at least one day or 1.2× prior interval; Good at least one day or 2.2×; Easy at least four days or 3.2×. Intervals cap at 365 days. Both directions share the same schedule. Practising All cards updates scheduling too.
- **Progress:** Good and Easy count as successful recall, Hard and Again do not. Mastery is a scheduling proxy (21+ day interval), not a guarantee of memorization. All attempts including retries are counted.
- **Backup:** Settings > Export complete backup saves decks, schedules, themes and review history as JSON. Restore replaces the current library after confirmation. Individual decks can be exported as TSV (without progress, multiline content flattened).

## 4. Magic import

Offline magic import recognizes simple definitions such as `Cognitive dissonance: discomfort from conflicting beliefs` or `Photosynthesis is the process ...`. It is rule-based, not a language model; check all previews and skipped lines.

For truly unstructured notes, use the AI magic import section: paste notes, click Copy AI prompt + notes, open ChatGPT, paste and send the prompt. Copy the returned tab-separated cards back into Recall and preview. This workflow is online, uses your existing ChatGPT access, and has no embedded key or automated API call. Do not send confidential notes unless appropriate. An integrated one-click AI backend is not included; putting a secret API key in public JavaScript would expose it.

## 5. Files and customization

- index.html: shell and navigation
- style.css: responsive layout, colors, dark mode
- app.js: deck editing, import, study sessions, scheduling, statistics and backups
- manifest.json: install metadata
- sw.js: offline asset cache
- icon-192.png / icon-512.png: app icons

To change colors, edit CSS variables at the top of style.css. When publishing changes, increment `recall-v1` in sw.js (e.g. `recall-v2`) so the installed app refreshes its cache. Close all app tabs/windows and reopen online to activate the update.

## 6. Important limitations

Data is saved in localStorage, which has a browser-dependent quota (often around 5 MB) and can be cleared or evicted. Keep regular JSON backups in Files/iCloud Drive. There is no cloud synchronization, encryption beyond your device/browser protections, or account system. A public hosting repository exposes the app source, not locally entered cards. Battery use has not been benchmarked. JavaScript syntax was checked; browser execution and iPad installation require testing on your device because the build environment blocked browser navigation.
