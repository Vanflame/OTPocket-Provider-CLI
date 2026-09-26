# OTPocket Provider CLI (otpagent)

Connects a GSM modem pool (16 / 32 / 64 ports) to your OTPocket provider account.
It shows a live dashboard of every SIM and forwards incoming SMS instantly.

## Install: Windows

1. Download **`otpagent-windows-x64.exe`** from the [latest release](../../releases/latest).
2. Open **Command Prompt** in your Downloads folder and run:
   ```bat
   otpagent-windows-x64.exe install
   ```
3. Close any other modem software (e.g. Dangs Modem), then run:
   ```bat
   otpagent
   ```
4. Enter the 6-character activation code from your provider dashboard
   (**Inventory → Register device → Gateway**, set **Max SIMs** to your port count).

> If Windows shows *"Windows protected your PC"*, click **More info → Run anyway**.
> This happens with new releases until Microsoft has reviewed them.

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
