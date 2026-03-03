# SportBit Auto Sign-Up

Automatically signs up for CrossFit Hilversum WOD classes on **Monday and Thursday at 20:00** via the SportBit API. Runs daily at midnight (Amsterdam time) through GitHub Actions.

## Setup

1. **Fork or clone this repo**

2. **Add your credentials as GitHub Actions secrets** (Settings > Secrets and variables > Actions > New repository secret):
   - `SPORTBIT_USERNAME` — your SportBit login email/username
   - `SPORTBIT_PASSWORD` — your SportBit password

   Or via CLI:
   ```bash
   gh secret set SPORTBIT_USERNAME
   gh secret set SPORTBIT_PASSWORD
   ```

3. **Test it** — go to the Actions tab > "CrossFit Auto Sign-Up" > "Run workflow" to trigger manually

The workflow runs every night at midnight and signs up for any Mon/Thu 20:00 classes in the next 7 days. If you're already signed up, it skips. Results are visible in the Actions log.

## Local usage

```bash
pip install requests

# Dry run (no sign-ups, just shows what it would do)
SPORTBIT_USERNAME=you@email.com SPORTBIT_PASSWORD=yourpass python3 autosignup.py

# Actually sign up
SPORTBIT_USERNAME=you@email.com SPORTBIT_PASSWORD=yourpass python3 autosignup.py --live
```

### Options

| Flag | Default | Description |
|------|---------|-------------|
| `--live` | off | Actually sign up (default is dry-run) |
| `--days N` | 7 | How many days to look ahead |
| `--time HH:MM` | 20:00 | Target class time |
| `--username` | env var | SportBit username |
| `--password` | env var | SportBit password |

## Customization

To change the target days or time, edit the constants at the top of `autosignup.py`:

```python
TARGET_WEEKDAYS = {0: "Monday", 3: "Thursday"}  # Python weekday numbers
TARGET_TIME = "20:00"
```
