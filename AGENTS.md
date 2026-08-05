# AGENTS.md

## Source of truth

- The production source of truth is:
  `fleet-intelligence/index.html` on branch `main`.
- Before making changes, read the complete current file.
- Never regenerate the add-in from scratch unless explicitly requested.
- Modify the existing implementation in place.
- Preserve all working behavior unless the task explicitly changes it.

## Required Geotab references

For MyGeotab Add-In work, follow the implementation guidance from:

- `fhoffa/geotab-vibe-guide/AGENT_SUMMARY.md`
- `fhoffa/geotab-vibe-guide/skills/geotab/SKILL.md`
- `fhoffa/geotab-vibe-guide/skills/geotab/references/ADDINS.md`

Load only the references needed for the current task.

## MyGeotab lifecycle

Preserve this global registration:

`window.geotab.addin.fleetIntelligence = function () { ... };`

The add-in must return:

- `initialize(api, state, callback)`
- `focus(api, state)`
- `blur(api, state)`

Rules:

- Always invoke `callback()` in `initialize`, including failure paths.
- Do not immediately invoke the add-in registration function.
- Use `api.call(method, params, successCallback, errorCallback)`.
- Preserve safe API error handling.
- Perform data refreshes in `focus`.
- Avoid duplicate event listeners across repeated focus calls.

## Compatibility

- Use ES5-compatible JavaScript inside the add-in:
  `var`, classic `function`, and string concatenation.
- Do not introduce arrow functions, template literals, optional chaining,
  or other syntax that may fail in older MyGeotab contexts.
- Do not place external script tags or stylesheet links in `<head>`.
- Preserve the working project-specific pattern:
  the complete `<style>` block is immediately after `<body>`.
- Load external libraries dynamically in JavaScript.
- Preserve dynamic Chart.js and Leaflet loading.
- Do not replace the current styling strategy with external CSS unless
  explicitly requested and tested inside MyGeotab.

## Existing functionality that must remain working

Preserve:

- Device table and vehicle search
- vehicle selection
- latest LogRecord GPS location
- OpenStreetMap and Leaflet marker
- speeding Rule discovery
- ExceptionEvent loading
- Chart.js speeding chart
- loading, success, and error states
- Slovenian UI labels

## API and data safety

- Never hardcode credentials.
- Do not add authentication secrets to the repository.
- Use MyGeotab's provided `api` object.
- Handle empty and missing API results safely.
- Avoid unbounded rendering of large result sets.
- Show a loading state before longer API calls.

## Change workflow

Before editing:

1. Confirm the current branch.
2. Confirm the latest commit.
3. Read the complete current `fleet-intelligence/index.html`.
4. Read `fleet-intelligence/config.json`.
5. Confirm the existing add-in namespace and lifecycle methods.

After editing:

1. Validate HTML parsing.
2. Validate `config.json`.
3. Show `git diff --stat`.
4. Show the relevant diff.
5. Confirm that unrelated files were not changed.
6. Increment the config version.
7. Update the cache-busting URL to the same version.
8. Commit to a new feature branch.
9. Do not merge to `main` without review.

## Deployment

GitHub Pages deploys from `main`.

After merge:

- confirm the Pages deployment succeeded,
- verify the public HTML source,
- verify the new version query in `config.json`,
- hard refresh MyGeotab if the old version remains cached.
