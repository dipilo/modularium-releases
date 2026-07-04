# About this repo

This repo hosts public releases of **Modularium**, and the community plugins directory.

Modularium is *currently* not open source software and this repo **DOES NOT** contain the source code of
Modularium. However, if you wish to contribute to Obsidian, you can easily do so with our extensive plugin system. See
[dipilo/modularium-api](https://github.com/dipilo/modularium-api) for the API and 
[dipilo/modularium-sample-plugin](https://github.com/dipilo/modularium-sample-plugin) for a template.

This repo does not accept issues, if you have questions or issues with plugins, please go to their own repo to file them.

## Files

- `community-plugins.json` — the community plugin directory (see schema below).
- `community-plugins-removed.json` — plugins removed from the directory (e.g. for policy violations).
- `desktop-releases.json` — the latest Modularium desktop release and its installers.

## Submit your plugin

Open a pull request adding one entry to `community-plugins.json`:

```json
{
  "id": "your-plugin-id",
  "name": "Your Plugin",
  "author": "you",
  "description": "One-line summary shown in the browser.",
  "repo": "you/your-plugin-repo"
}
```

Requirements:

- `id` — `[a-z0-9_-]`, unique, and **must match** the `id` in your repo's `modularium-plugin.json`.
- `repo` — a public GitHub repo in `owner/name` form whose **default branch** contains a valid
  `modularium-plugin.json`, the entry file it points to (e.g. `plugin.js`), and a `README.md`.
- Your plugin must comply with the developer policies (no malware, no undisclosed network/telemetry, no
  bundled backdoors). Submissions are reviewed before merge.

## How community plugins are pulled

- Modularium reads the list of plugins in `community-plugins.json`.
- The `name`, `author`, and `description` fields are used for searching.
- When a user opens a plugin's details, Modularium pulls `modularium-plugin.json` and `README.md` from the
  repo's default branch.
- On install/update, Modularium downloads `modularium-plugin.json` and the entry file (e.g. `plugin.js`)
  from the repo's default branch into `%APPDATA%/Modularium/plugins/<id>/`, then enables the plugin.
- Update detection compares the installed `version` against the repo's current `modularium-plugin.json`
  version. `versions.json` (`"plugin-version": "min-modularium-version"`) lets older apps pick a compatible
  version.
