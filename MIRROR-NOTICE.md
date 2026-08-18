# Mirror notice

This repository is a fork of [`tauri-apps/global-hotkey`](https://github.com/tauri-apps/global-hotkey).

## Why this fork exists

The branch **`bolt-unified-wayland`** carries Wayland support for `global-hotkey`, implemented on
top of the [XDG Desktop Portal `GlobalShortcuts`](https://flatpak.github.io/xdg-desktop-portal/docs/doc-org.freedesktop.portal.GlobalShortcuts.html)
interface. Upstream `global-hotkey` is still X11-only on Linux as of **v0.8.0** (2026-05-01).

**That Wayland work is not ours.** It was written by **[@0-don](https://github.com/0-don)
(`don.cryptus@gmail.com`)** on the `unified-wayland` branch of `0-don/global-hotkey`.

That repository — and the entire `0-don` GitHub account — **no longer exists**. It was found
missing on **2026-08-18**:

```
fatal: repository 'https://github.com/0-don/global-hotkey/' not found
```

A GitHub-wide code search for `unified-wayland` at that time returned no surviving copy of the
branch anywhere. The commits here were recovered from a cached bare git database and republished
so that projects depending on this work can keep building.

**We are hosting this because the original vanished. We are not claiming it.** The original
author and committer metadata on every commit has been preserved unchanged, and the upstream
Apache-2.0 / MIT licensing (`LICENSE-APACHE`, `LICENSE-MIT`, `LICENSE.spdx`) is intact and
unmodified. If @0-don would like these branches taken down, renamed, or moved, please open an
issue and we will comply.

## Branches

| Branch | Contents |
|---|---|
| `bolt-unified-wayland` | @0-don's two `unified-wayland` commits (`dc57a82`, `83f5cf5`) **rebased onto upstream `global-hotkey-v0.8.0`** (`2a620bf`). This is the branch consumed downstream. |
| `archive/0-don-unified-wayland-83f5cf55` | The recovered `unified-wayland` branch exactly as pinned by downstream consumers, unmodified: tip `83f5cf55a80111b29805eae453fd63b20b781a53`. |
| `archive/0-don-unified-wayland-tip-d001a97` | The recovered branch at its **final** state, tip `d001a97` (2026-07-03). @0-don force-pushed the branch after `83f5cf55`, so this line is *not* a descendant of it — it contains three further commits (portal-restart reconnect, XF86 key mapping, optional hotkey descriptions). Preserved verbatim; not yet evaluated. |
| `dev` | Untouched mirror of upstream `tauri-apps/global-hotkey`. |

The rebase onto v0.8.0 introduces **no behavioural change to the Wayland or X11 code**. Diffing
the rebased tree against the original `83f5cf55` tree yields only the upstream v0.8.0 delta:
the version bump, the CHANGELOG entry, the consumed `.changes/` files, and upstream
[#178](https://github.com/tauri-apps/global-hotkey/pull/178) (Windows: sleep 50 ms in the
release-detection loop instead of burning a CPU core for the hold duration).

## Upstream status

Wayland support is **not** merged upstream. The live upstream effort is
[PR #162](https://github.com/tauri-apps/global-hotkey/pull/162) by
[@Adamskye](https://github.com/Adamskye), open since 2025-09-14, tracking
[issue #28](https://github.com/tauri-apps/global-hotkey/issues/28) (open since 2022-03-01).
Note that #162 takes a different approach — a separate `wl_register_all` API — whereas the
branch here dispatches transparently inside the existing `register()`, which is what makes it a
drop-in under `tauri-plugin-global-shortcut`.

This fork should be dropped in favour of upstream once Wayland support lands there.
