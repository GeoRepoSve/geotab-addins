# Fleet Intelligence MyGeotab Add-in

This repository hosts the **Fleet Intelligence** MyGeotab add-in for GitHub Pages. The add-in displays all available MyGeotab `Device` objects in a searchable vehicle table, lets a user select a vehicle, shows the latest GPS `LogRecord`, and charts speeding-related `ExceptionEvent` records from the last 30 days.

## Files

- `fleet-intelligence/index.html` - Single-page MyGeotab add-in with embedded CSS and application JavaScript.
- `fleet-intelligence/config.json` - MyGeotab add-in configuration file.

## Expected GitHub Pages URLs

After GitHub Pages is enabled, the add-in entry point should be available at:

`https://GeoRepoSve.github.io/geotab-addins/fleet-intelligence/`

Use this configuration URL when registering the add-in in MyGeotab:

`https://GeoRepoSve.github.io/geotab-addins/fleet-intelligence/config.json`

## Enable GitHub Pages

1. Open the repository on GitHub: `https://github.com/GeoRepoSve/geotab-addins`.
2. Go to **Settings**.
3. In the left sidebar, select **Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
5. Set **Branch** to **main**.
6. Set the folder selector to **/** (repository root).
7. Click **Save**.
8. Wait for GitHub Pages to finish deploying before registering the MyGeotab configuration URL.

## MyGeotab Add-in Details

- Add-in namespace: `geotab.addin.fleetIntelligence`
- Lifecycle methods: `initialize(api, state, callback)`, `focus(api, state)`, and `blur(api, state)`
- Support email: `matej@svetkom.si`
- Version: `1.0.0`

## Validation

Before publishing changes, validate the files from the repository root:

```bash
python3 -m json.tool fleet-intelligence/config.json >/tmp/config.valid.json
python3 - <<'PY'
from html.parser import HTMLParser
from pathlib import Path
class Parser(HTMLParser):
    pass
Parser().feed(Path('fleet-intelligence/index.html').read_text())
print('HTML parser completed')
PY
```
