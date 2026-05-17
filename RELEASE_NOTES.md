# Strata Framework v1.0.0

First public release of the Strata recipe — a single txAdmin deployment that
stands up a complete Strata roleplay server with the OX ecosystem and the
stock CitizenFX resources.

---

## Quick deploy

In txAdmin:

1. **New deployment → Remote recipe**.
2. Paste the recipe URL:
   ```
   https://raw.githubusercontent.com/StrataFW/strata-recipe/main/recipe.yaml
   ```
3. Provide your MySQL connection string when prompted.
4. After deploy completes, finish setup on the server (see [Post-deploy](#post-deploy)).

---

## What's deployed

| Group       | Source                | Resources                                                                                                       |
|-------------|-----------------------|-----------------------------------------------------------------------------------------------------------------|
| `[cfx]`    | citizenfx/*           | `cfx-server-data` (gameplay / gamemodes / managers / system), `screenshot-basic`                                |
| `[ox]`     | overextended/*        | `oxmysql`, `ox_lib`, `ox_core`, `ox_target`, `ox_inventory`, `ox_banking`, `ox_commands`, `ox_doorlock`, `ox_fuel` |
| `[strata]` | StrataFW/*            | `st_log`, `st_bootstrap`, `st_ipl`, `st_multichar`, `st_spawn`, `st_chat`, `st_apartments`, `st_admin`, `st_appearance` |

Plus the full cfg tree (`server.cfg` + `cfg/identity.cfg`, `runtime.cfg`,
`convars.cfg`, `permissions.cfg`, `resources.cfg`) wired up so the server
boots in one command.

---

## Prerequisites

- **FXServer** artifact `>= 6552` (cerulean).
- **MariaDB / MySQL** with `utf8mb4` default charset.
  - All Strata + OX tables auto-create on first boot.
- **OneSync** enabled in txAdmin's settings page (the recipe sets `$onesync: on`).
- A **Cfx.re license key** — https://keymaster.fivem.net

---

## Post-deploy

The recipe never ships secrets. After it finishes, on the server:

```bash
cd <deploy-path>
cp cfg/secrets.cfg.example    cfg/secrets.cfg
cp cfg/principals.cfg.example cfg/principals.cfg
```

Edit:

- **`cfg/secrets.cfg`** — your `sv_licenseKey` and `mysql_connection_string`.
  Optionally `steam_webApiKey` and the `st:log:webhook` Discord URL.
- **`cfg/principals.cfg`** — add your real-player → staff-tier assignments.
  Tier hierarchy (highest → lowest): `dev > sudo > admin > mod > jrmod`.

Then **Start** the server from txAdmin. `st_bootstrap` shows a branded
loadscreen, `st_log` prints a boot summary card, and you're live.

---

## Optional resources

Two Strata resources are present but **not started by default** — uncomment
them in `cfg/resources.cfg` if you want them:

- `st_discord` — Discord rich presence + role sync
- `st_debug`   — dev-only inspector / overlay

Two paid/third-party slots are stubbed and commented out — drop the asset
into `resources/` and uncomment when ready:

- `kiiya_lapuerta` — La Puerta MLO (required for `st_apartments` zones)
- `[assets_corefx]` — graphics / visual overhaul pack

---

## Updating

Every Strata + OX resource has its own per-resource release. To re-pull the
latest of everything without a full redeploy, the bundle workflow can produce
a known-good frozen `strata-bundle.zip`:

```
Actions → Bundle → Run workflow
```

Leave `tag` blank for an artifact-only run, or set e.g. `2026.05.17` to also
cut a GitHub Release with the bundle attached.

---

## Layout

```
server/
├── server.cfg
├── cfg/
│   ├── identity.cfg
│   ├── runtime.cfg
│   ├── convars.cfg
│   ├── permissions.cfg
│   ├── resources.cfg
│   ├── principals.cfg.example   → copy to principals.cfg
│   └── secrets.cfg.example      → copy to secrets.cfg
└── resources/
    ├── [cfx]/    (stock)
    ├── [ox]/     (overextended)
    └── [strata]/ (StrataFW)
```

---

## Support

- Per-resource issues: open them on the resource repo (e.g. `StrataFW/st_chat`).
- Recipe / deploy issues: open them here.
