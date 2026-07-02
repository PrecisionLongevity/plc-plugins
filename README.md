# PLC plugins

A Claude Code plugin marketplace for Precision Longevity / Levels. Shareable brand, design, and content tooling — **no infrastructure or sensitive content** (that lives in the separate `infra` marketplace). Add this marketplace once, then install any plugin below.

## Plugins

### `levels-brand`

The Levels design system — color tokens, typography, a component library, and runnable HTML templates for three formats (slide deck, print/PDF report, web doc-site), plus a print-to-PDF workflow. Ships the `levels-design-system` skill, which triggers on requests like "build a Levels deck," "make a Levels PDF report," or "make this look like Levels."

## Install

```
/plugin marketplace add PrecisionLongevity/plc-plugins
/plugin install levels-brand@plc
```

- `plc` is the marketplace name (from `.claude-plugin/marketplace.json`).
- Choose the scope when prompted (user = all your projects; project = one repo).
- Run `/reload-plugins` (or restart Claude Code) if it doesn't appear immediately.
- This repo is private: to install, you must have git access to `PrecisionLongevity/plc-plugins`.

Verify it loaded: ask "build a Levels deck" and confirm the `levels-design-system` skill activates.

## Update

Maintainer: bump `version` in **both** `plugins/levels-brand/.claude-plugin/plugin.json` and the plugin's entry in `.claude-plugin/marketplace.json`, commit, push.

Recipients:

```
/plugin marketplace update plc
/plugin install levels-brand@plc
```

## Repo layout

```
.
├── .claude-plugin/
│   └── marketplace.json          # marketplace manifest (name: "plc")
├── plugins/
│   └── levels-brand/
│       ├── .claude-plugin/
│       │   └── plugin.json        # plugin manifest
│       └── skills/
│           └── levels-design-system/
│               ├── SKILL.md
│               ├── references/     # style-guide.md, components.md
│               └── assets/         # deck / report / doc templates + levels-report.css
└── README.md
```

Skills are auto-discovered from `plugins/<plugin>/skills/` — no declaration needed.
