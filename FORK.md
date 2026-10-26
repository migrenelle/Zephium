# Personal Zephium fork

This checkout keeps `origin` pointed at `migrenelle/Zephium` and uses
`zephium-browser/Zephium` only as the read-only `upstream`.

## Run from source

```powershell
corepack pnpm install --frozen-lockfile
corepack pnpm dev
```

Development runs use the `app.zephium.dev` identity and its own
`%APPDATA%\app.zephium.dev` profile.

## Build the personal Windows package

```powershell
corepack pnpm build:fork
```

This produces an optimized release build and NSIS installer under the normal
`app.zephium` identity, so it can use the profile preserved from the previous
install. The package has no update endpoint, so an upstream release cannot
replace the personal build automatically.

## Bring in upstream changes

```powershell
git fetch upstream --prune
git switch main
git merge --no-edit upstream/main
```

Resolve conflicts, run the checks for the affected areas, build the package,
and push `main` to `origin`. The upstream push URL is deliberately set to
`no_push`.
