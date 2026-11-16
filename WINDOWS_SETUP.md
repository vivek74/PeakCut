# Setting up PeakCut on a Windows PC

This is for this fork, which can use your **Claude subscription** through Claude Code, so you don't need an AI key.
Each step is done once. Type the commands into **PowerShell** (press Start, type `powershell`, press Enter).

## 1. Install the tools

```powershell
winget install Python.Python.3.12
winget install Gyan.FFmpeg
winget install Git.Git
```

Close PowerShell and open it again so the new programs are found. Check them:

```powershell
python --version
ffmpeg -version
git --version
```

Also update your **NVIDIA driver** (GeForce Experience or nvidia.com/drivers). PeakCut uses the graphics card to
make clips several times faster, and needs a recent driver for that.

## 2. Install Claude Code and sign in

```powershell
irm https://claude.ai/install.ps1 | iex
```

Close and reopen PowerShell, then run `claude` once and sign in with your Claude account. Type `/exit` when it
has opened. (If the command above has changed, follow the Windows steps at https://claude.com/claude-code.)

## 3. Get PeakCut

Pick a drive with plenty of room. In this example it is `D:\`:

```powershell
cd D:\
git clone https://github.com/vivek74/PeakCut.git
cd PeakCut
python -m venv .venv
.venv\Scripts\pip install -r requirements.txt
```

## 4. Settings

Make the settings file:

```powershell
copy .env.example .env
notepad .env
```

Change or add these lines, then save:

```ini
PEAKCUT_AI_PROVIDER=claude_code
PEAKCUT_AI_MODELS=sonnet,haiku
PEAKCUT_UPDATE_REPO=vivek74/PeakCut
```

`sonnet` picks better clips. `haiku` is the fallback, and uses less of your Claude limit.

## 5. Start it

```powershell
cd D:\PeakCut
.venv\Scripts\python -m studio.server
```

The first start downloads the speech model (about 480 MB). Then open **http://127.0.0.1:8765** in your browser.
To check that the AI works, go to **Settings, AI** and press **Save and test**.

Leave the PowerShell window open while PeakCut runs. To stop it, press Ctrl+C in that window.

## Keep it safe

- **Don't put the PeakCut folder in OneDrive** or any other synced folder. It holds the sign-ins of your
  connected YouTube, Instagram and TikTok accounts.
- Use a Windows password, and turn on BitLocker if your Windows edition has it.
- Leave `PEAKCUT_HOST` at its default, so only this PC can open the dashboard.
- **Updates:** when the dashboard shows a new version, it means *this fork* was updated. Changes from the original
  author aren't brought into the fork until someone has reviewed them.

## For each clipping campaign

Create one **creator** in the dashboard for each campaign, then fill in that creator's settings:
- **Channels:** the streamer's YouTube, Twitch or Kick channel.
- **Watermark on the video:** the credit the campaign requires, for example `@streamer`.
- **Line added to every post:** a tag or credit in the post text, if the campaign asks for one.
- **Campaign pay per 1,000 views:** used to estimate your earnings.
