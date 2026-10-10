# Frozen graphify for Bach's machines

This repo is a private mirror of upstream `Graphify-Labs/graphify` at tag `v0.9.84` (`2cb81c6`), Apache-2.0 / MIT (see LICENSE, LICENSE-MIT, NOTICE). Nothing here tracks upstream; it changes only when Bach moves the pin after reading the upstream diff.

- `requirements.lock`: every runtime dependency pinned with sha256 hashes, exported from upstream's own `uv.lock` at `2cb81c6` (`uv export --frozen --no-dev --no-emit-project`).
- `graphifyy-0.9.84-py3-none-any.whl`: built once from this commit with `uv build --wheel`, sha256 `6d1dd1ff2aea3c9abe326010a7d3a2f16ab01ea18e2d478473d1d2120162f233`. Installing it needs no build step and fetches no build tools.

## Install (offline-reproducible, hash-checked)

```bash
git clone --depth 1 --branch bach-0.9.84 git@github.com:BachNTran/graphify.git /tmp/graphify-frozen
python3 -m venv ~/.local/share/graphify
~/.local/share/graphify/bin/pip install --require-hashes -r /tmp/graphify-frozen/frozen/requirements.lock
echo "6d1dd1ff2aea3c9abe326010a7d3a2f16ab01ea18e2d478473d1d2120162f233  /tmp/graphify-frozen/frozen/graphifyy-0.9.84-py3-none-any.whl" | sha256sum -c -
~/.local/share/graphify/bin/pip install --no-deps /tmp/graphify-frozen/frozen/graphifyy-0.9.84-py3-none-any.whl
mkdir -p ~/.local/bin && ln -sf ~/.local/share/graphify/bin/graphify ~/.local/bin/graphify
```

Never run `graphify install`, `graphify claude install` or `graphify hook install`: they overwrite the reviewed skill copy in the Skills repo.

## Upgrading
Fetch upstream, read the diff from `v0.9.84` to the new tag, then repeat the export and build on the new tag and add a new `bach-<version>` tag. Update the pin in the Skills repo's `kit/crew/skills/graphify/UPSTREAM.md`.
