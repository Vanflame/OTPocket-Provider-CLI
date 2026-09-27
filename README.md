# OTPocket Provider CLI (otpagent)

Connects a GSM modem pool (16 / 32 / 64 ports) to your OTPocket provider account.
It shows a live dashboard of every SIM and forwards incoming SMS instantly.

## Install: Windows (Command Prompt only)

Close other modem software (e.g. Dangs Modem) first. Then run, one line at a time:

```bat
cd /d %USERPROFILE%\Downloads
curl -L -o otpagent-windows-x64.exe https://github.com/Vanflame/OTPocket-Provider-CLI/releases/latest/download/otpagent-windows-x64.exe
otpagent-windows-x64.exe install
otpagent
```

Enter the 6-character activation code from your provider dashboard
(**Inventory → Register device → Gateway**; leave **Max SIMs** blank to auto-detect the pool size).

> If Windows shows *"Windows protected your PC"*, click **More info → Run anyway**.

## Update

```bat
otpagent update
```
This downloads the latest release, checks it, and swaps it in, keeping your pairing
and settings. Then close and reopen `otpagent`. The dashboard tells you when an
update is available.

> **Coming from v1.0.0?** That version doesn't have `update` yet. Update once by
> re-running the `curl` and `install` lines above (close otpagent first). After that,
> `otpagent update` works.

## Install: Orange Pi / Linux (arm64)

```bash
wget https://github.com/Vanflame/OTPocket-Provider-CLI/releases/latest/download/otpagent-linux-arm64
wget https://github.com/Vanflame/OTPocket-Provider-CLI/releases/latest/download/install.sh
sudo bash install.sh YOURCODE
```
It starts automatically at boot. Run `otpagent` to open the dashboard.

## Dashboard keys

`f` filter SMS · `Esc` clear filter · `r` resync SIMs · `p` unpair · `q` quit

Tiles pulsing **green** are healthy SIMs. **Yellow** means retrying, **red** means
missing, and **magenta** means the SIM has no number stored.

## Uninstall

```bat
otpagent uninstall --purge
```
On Linux, run `sudo bash uninstall.sh`.

## Troubleshooting

| Problem | Fix |
|---|---|
| No SIMs shown | Close other modem software; replug the pool |
| `mqtt RECONNECTING` | Check internet; port 8883 must be allowed |
| "Invalid code" / "already paired" | Re-issue a code on the dashboard |

Logs: `C:\ProgramData\otpagent\agent.log` (Windows), `journalctl -u otpagent -f` (Linux).
