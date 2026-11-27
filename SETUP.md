# Set up Bare with Claude Code

This page is written for Claude Code. Paste this line into Claude Code on the Windows PC where you want Bare, and it walks you through everything below:

```
Read https://raw.githubusercontent.com/refaelhal/bare-browser/main/SETUP.md and walk me through setting up Bare, one step at a time.
```

You can also follow it yourself. It takes about 15 minutes.

---

## For Claude: how to run this

You are helping someone switch to Bare, a browser for Windows, so that it becomes the only browser on their PC and everything they had in Chrome still works.

Rules for the whole setup:

1. **Go one step at a time.** Say what the step does in one or two plain sentences, do your part, then wait until the person says it's done before moving on. Talk like a friend helping, not a manual.
2. **Never get around a prompt.** Windows SmartScreen, the installer, User Account Control, Windows Hello, Google's sign-in and every uninstaller ask the person directly. The person answers those, never you. Don't click them, don't use flags, registry edits, scripts or settings that hide, skip or auto-accept them, and don't turn off SmartScreen, UAC, Defender or any other protection. If a step is blocked, explain it and let the person decide.
3. **Never handle secrets.** Don't read, print, copy or move passwords, password files, cookies or browser profile files. Bare does all of that itself.
4. **Check, don't assume.** Before you say a step worked, check it: look at what Bare shows, or ask the person to tell you what they see. If something fails, say so plainly.
5. **Delete nothing until step 9.** No browser is removed before everything in step 8 has passed.
6. If something here doesn't match what the person sees (a button has another name, a step is already done), adapt and say so.

Start by telling the person, in a few lines: what's going to happen (install Bare, bring everything over from Chrome, sign in to Google, check it all works, then remove the other browsers), that it takes about 15 minutes, and that they will click every confirmation themselves. Also say this up front, so there are no surprises:

> Chrome's own sync (bookmarks, history and open tabs shared with your phone and other computers) only works inside Chrome. Google doesn't let other browsers use it. Once Chrome is gone, your phone won't see what you do in Bare, and Bare won't see your phone's tabs. Gmail, YouTube, Drive and the rest of your Google account work in Bare as usual, and your Google passwords come into Bare when you sign in.

Ask if they want to go ahead.

### Step 1. Check the PC

- Confirm it's Windows 10 or 11 (`[Environment]::OSVersion` or `winver`).
- Find which browsers are installed: look under `HKLM\SOFTWARE\Clients\StartMenuInternet`, `HKLM\SOFTWARE\WOW6432Node\Clients\StartMenuInternet` and `HKCU\SOFTWARE\Clients\StartMenuInternet`. Note Chrome, Edge, Firefox, Brave, Opera, Vivaldi and others. Keep this list for step 9.
- If Bare is already installed, skip to step 3 and check it's up to date there.

### Step 2. Install Bare

- Download the installer to the person's Downloads folder:
  `https://github.com/refaelhal/bare-browser/releases/latest/download/Bare-Setup.exe` (about 240 MB).
- Open it with `Start-Process`. Then tell the person:
  - Windows may say "Windows protected your PC". That's because the installer isn't signed yet. If they trust it, they click **More info**, then **Run anyway**. That's their choice, not yours.
  - They pick who it's for and where it goes, then click **Install**.
- Wait until they say it's installed.

### Step 3. Close Chrome, then open Bare

- Ask the person to close Chrome completely, including from the tray by the clock (right-click the Chrome icon, then Exit). Bare can only bring over Chrome's open tabs while Chrome is closed. Check with `Get-Process chrome -ErrorAction SilentlyContinue`; if it's still running, ask them to close it. Don't kill it yourself, because it might have unsaved work.
- Ask them to open Bare.
- Ask them to open ⋯ → Settings → About Bare and tell you the version. It must be **1.6.1 or newer** (older versions try to sign in to Google through Chrome, which Google refuses). If it's older, have them check for an update on that page and restart Bare.

### Step 4. Move everything from Chrome

- On first start, Bare shows one button: **Move everything from Chrome**. If they already closed that screen, it's at the top of ⋯ → Settings → Import.
- Ask them to click it. Bookmarks, history, open tabs, addresses, cards, extensions and the search engine come over in about a minute. Chrome itself isn't changed.
- If they used another browser instead of Chrome (Edge, Firefox, Brave and others), the button names that one.
- When it finishes, ask what the done screen says, so you both know how many things came over.

### Step 5. Bring over Chrome's passwords

Chrome locks most saved passwords to itself, so Chrome has to hand them over.

- On Bare's done screen there's a button that opens Chrome's password page. If it doesn't open the right page, ask them to open Chrome and go to `chrome://password-manager/settings` themselves.
- They click **Export passwords** there. Windows asks for their PIN, face or fingerprint. That's Windows checking it's really them.
- They save the file to Downloads. Bare finds it, brings the passwords in, and deletes the file. Don't open, read or move the file yourself.
- Ask them to check ⋯ → Settings → Passwords in Bare. Bare asks Windows Hello before showing a password. The count should roughly match what Chrome had.
- If they use Bitwarden, 1Password or another password manager extension, it came over in step 4. Ask them to unlock it once in Bare.

### Step 6. Sign in to Google

- Ask them to go to `https://accounts.google.com` in Bare and sign in.
- Google doesn't accept a password typed straight into Bare, so Bare shows a panel with **Sign in with Firefox**. They click it. Bare opens a clean Firefox window (their own Firefox if they have it, or a private copy Bare gets from Mozilla). They sign in there, including any 2-step check on their phone. Firefox then closes by itself and Bare is signed in.
- If instead they see a Chrome window saying "This browser or app may not be secure", their Bare is older than 1.6.1. Go back to step 3 and update.
- After sign-in, Bare also brings in the passwords saved in their Google account.

### Step 7. Make Bare the default browser

- Open the default apps page: `Start-Process ms-settings:defaultapps`.
- Ask them to find Bare, open it and click **Set default**. Windows only lets the person do this, so don't try to change it with the registry.

### Step 8. Check that everything works

Ask the person to check each of these in Bare and tell you what they see. Only mark one passed when they confirm it.

1. **Gmail**: `https://mail.google.com` opens their inbox, already signed in.
2. **YouTube**: `https://youtube.com` shows their profile picture top right, and a video plays with sound.
3. **Bookmarks**: the bookmarks button at the top of the sidebar shows their Chrome bookmarks.
4. **Passwords**: a site they log in to often fills the password.
5. **Extensions**: the Extensions button in the bottom bar lists the ones they use.
6. **Open tabs**: the tabs they had open in Chrome are in the sidebar.
7. **A link from another app**: click a link in an email or a chat app. It opens in Bare.

If anything fails, help fix it before going on. If it can't be fixed, tell them honestly and suggest keeping Chrome for now.

### Step 9. Remove the other browsers

Only once step 8 has passed. Before starting, say this:

> When Chrome asks "Also delete your browsing data?", leave it **unticked**. Your data is already in Bare, but keeping Chrome's copy costs nothing and means you can move it again later if needed.

Then, for each browser found in step 1:

- Open Installed apps: `Start-Process ms-settings:appsfeatures`. The person searches for the browser, clicks ⋯ → **Uninstall**, and answers its prompts. Use only the browser's own uninstaller this way. Don't uninstall with scripts, `winget` silent flags, or by deleting folders.
- **Firefox**: fine to remove. Bare keeps its own private copy for Google sign-in and gets it again if it ever needs to.
- **Microsoft Edge** is part of Windows. Most PCs don't offer an Uninstall button for it, and forcing it off with scripts can break Windows features, so don't. If Windows offers Uninstall (some countries in Europe), they can use it. Otherwise it stays, and with Bare as the default it won't open on its own.
- **Never remove "Microsoft Edge WebView2 Runtime".** It isn't a browser. Many Windows apps need it to work.

When they're done, check with the step 1 registry keys which browsers are left, and tell them.

### Step 10. Wrap up

Tell the person, briefly:

- Bare is now their browser, and it updates itself in the background.
- What came over (from steps 4 to 6) and anything that didn't.
- The honest gap again: phone sync is Chrome-only, so the phone and Bare don't share tabs or history.
- Passwords saved in Bare stay behind Windows Hello, on this PC.
