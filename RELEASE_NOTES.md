<div align="center">

<img src="https://raw.githubusercontent.com/StrataFW/strata-recipe/main/.github/assets/banner.png" alt="Strata Framework" width="600">

### `v1.0.0` — first public release

A complete, batteries-included FiveM roleplay framework built on `ox_core`.

[**Deploy**](#-deploy-in-30-seconds) · [**What's inside**](#-whats-inside) · [**After deploy**](#-after-deploy) · [**Optional add-ons**](#-optional-add-ons)

</div>

---

## ⚡ Deploy in 30 seconds

In **txAdmin → New deployment → Remote recipe**:

```
https://raw.githubusercontent.com/StrataFW/strata-recipe/main/recipe.yaml
```

Provide your MySQL connection string when prompted. The recipe lays out
`[cfx]` + `[ox]` + `[strata]`, writes the cfg tree, and validates the
database connection. Three minutes, one click, done.

> 💾 Prefer a frozen snapshot? Download **`strata-framework-v1.0.0.zip`**
> from the **Assets** section below and drop it into your FXServer directory.

---

## 📦 What's inside

<table>
<tr><th align="left">Layer</th><th align="left">Source</th><th align="left">Resources</th></tr>
<tr>
  <td>🟢 <code>[cfx]</code></td>
  <td><a href="https://github.com/citizenfx">citizenfx/*</a></td>
  <td><code>cfx-server-data</code> · <code>screenshot-basic</code></td>
</tr>
<tr>
  <td>🔵 <code>[ox]</code></td>
  <td><a href="https://github.com/overextended">overextended/*</a></td>
  <td><code>oxmysql</code> · <code>ox_lib</code> · <code>ox_core</code> · <code>ox_target</code> · <code>ox_inventory</code> · <code>ox_banking</code> · <code>ox_commands</code> · <code>ox_doorlock</code> · <code>ox_fuel</code></td>
</tr>
<tr>
  <td>🟣 <code>[strata]</code></td>
  <td><a href="https://github.com/StrataFW">StrataFW/*</a></td>
  <td><code>st_log</code> · <code>st_bootstrap</code> · <code>st_ipl</code> · <code>st_multichar</code> · <code>st_spawn</code> · <code>st_chat</code> · <code>st_apartments</code> · <code>st_admin</code> · <code>st_appearance</code></td>
</tr>
</table>

Plus a clean cfg tree (`server.cfg` + `cfg/identity.cfg`, `runtime.cfg`,
`convars.cfg`, `permissions.cfg`, `resources.cfg`) wired up so the server
boots in one command.

> 🎨 Every NUI resource ships **with source** — `web/src`, `package.json`,
> `vite.config.ts`, `bun.lock`. Fork, edit, rebuild.

---

## ✅ Prerequisites

|                |                                                       |
|----------------|-------------------------------------------------------|
| 🟦 **FXServer** | artifact `>= 6552` (cerulean)                         |
| 🟧 **Database** | MariaDB / MySQL with `utf8mb4` default charset        |
| 🟨 **OneSync**  | enabled in txAdmin's settings page                    |
| 🔑 **License**  | a Cfx.re key — [keymaster.fivem.net](https://keymaster.fivem.net) |

> ✨ All Strata + OX tables **auto-create on first boot** — no SQL setup step.

---

## 🔧 After deploy

The recipe never ships secrets. On the server, after deploy completes:

```bash
cd <deploy-path>
cp cfg/secrets.cfg.example    cfg/secrets.cfg
cp cfg/principals.cfg.example cfg/principals.cfg
```

Edit:

- 🔐 **`cfg/secrets.cfg`** — `sv_licenseKey` + `mysql_connection_string`.
  Optionally `steam_webApiKey`, `st:log:webhook`.
- 👥 **`cfg/principals.cfg`** — staff assignments.
  Tier hierarchy: `dev > sudo > admin > mod > jrmod`.

Hit **Start** in txAdmin. `st_bootstrap` shows a branded loadscreen,
`st_log` prints a boot summary card, you're live.

---

## 🧩 Optional add-ons

Two Strata resources ship installed but **commented out** in
`cfg/resources.cfg` — uncomment to enable:

- 💬 **`st_discord`** — Discord rich presence + role sync
- 🐞 **`st_debug`** — dev-only inspector / overlay

Two paid / third-party slots are stubbed:

- 🏠 **`kiiya_lapuerta`** — La Puerta MLO (required for `st_apartments` zones)
- 🎬 **`[assets_corefx]`** — graphics / visual overhaul pack

Drop the asset into `resources/` and uncomment the matching line in
`cfg/resources.cfg`.

---

## 🔄 Updating

Every resource has its own per-resource release on the `StrataFW` org.
To refresh everything in one shot, fire the bundle workflow:

```bash
gh workflow run Bundle --repo StrataFW/strata-recipe -f tag=v1.0.1
```

Leave `tag` blank for an artifact-only nightly run, or set a tag to cut a
new GitHub Release.

---

## 📁 Final layout

```
server/
├── server.cfg                       ← entrypoint (execs cfg/* in order)
├── cfg/
│   ├── identity.cfg                 ← hostname, capacity, network
│   ├── runtime.cfg                  ← onesync, game build, console
│   ├── convars.cfg                  ← ox + strata convars
│   ├── permissions.cfg              ← ACE rules + tier hierarchy
│   ├── resources.cfg                ← grouped start order
│   ├── principals.cfg.example       → copy to principals.cfg
│   └── secrets.cfg.example          → copy to secrets.cfg
└── resources/
    ├── [cfx]/                       ← stock citizenfx
    ├── [ox]/                        ← overextended ecosystem
    └── [strata]/                    ← StrataFW resources
```

---

## 🐛 Support

- **Per-resource bugs** → file on the resource repo (e.g. [`StrataFW/st_chat`](https://github.com/StrataFW/st_chat/issues))
- **Recipe / deploy bugs** → [file here](https://github.com/StrataFW/strata-recipe/issues)

---

<div align="center">

Built on `ox_core` by <a href="https://github.com/okIndica">okIndica</a> ⚡

</div>
