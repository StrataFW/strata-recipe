# strata-recipe

Drop-in txAdmin deploy recipe for a Strata FiveM server.

## What it deploys

Three layered resource groups, plus the server's cfg tree:

| Group       | Source                                | Contents                                              |
|-------------|---------------------------------------|-------------------------------------------------------|
| `[cfx]`     | citizenfx/cfx-server-data + screenshot-basic | Stock CitizenFX gameplay/gamemodes/managers/system, screenshot-basic |
| `[ox]`     | overextended/*                        | oxmysql, ox_lib, ox_core, ox_target, ox_inventory, ox_banking, ox_commands, ox_doorlock, ox_fuel |
| `[strata]` | StrataFW/*                            | st_log, st_bootstrap, st_ipl, st_multichar, st_spawn, st_chat, st_apartments, st_admin, st_appearance |

The cfg tree (`server.cfg` + `cfg/*.cfg`) is the same layout the framework uses
in development — entrypoint, identity, runtime, convars, permissions, resources.

## Deploy via txAdmin

1. New deployment → **Remote recipe**.
2. URL:
   ```
   https://raw.githubusercontent.com/StrataFW/strata-recipe/main/recipe.yaml
   ```
3. txAdmin will run the recipe (downloads everything, lays out resources, writes
   the cfg tree).
4. After deploy, copy the secret templates and fill them in:
   ```bash
   cp cfg/secrets.cfg.example    cfg/secrets.cfg
   cp cfg/principals.cfg.example cfg/principals.cfg
   ```
5. Start the server.

## Bundle releases

For environments that don't run recipes (or want a known-good frozen build),
the `Bundle` workflow produces `strata-bundle.zip` — a flat tree containing
everything the recipe would assemble.

- Runs weekly (Monday 06:00 UTC) and uploads an artifact.
- Manual dispatch with a tag publishes a GitHub Release.

```bash
gh workflow run Bundle -f tag=2026.05.17
```

## Layout produced

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

## Updating a single resource

Each Strata resource has its own `release.yml` workflow. Tag a new version in
the resource's standalone repo:

```bash
git tag v1.0.1
git push --tags
```

The bundle workflow picks it up on its next run (or fire it manually).
