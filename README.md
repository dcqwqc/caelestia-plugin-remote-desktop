# RemoteDesktop

A two-way Moonlight/Sunshine desktop link between configured hosts, in the
Caelestia bar.

Both machines serve and both consume, so the panel asks "is this the other one?"
rather than "is this the machine that streams?". Each host row reports whether a
session is up and which way it points — *connected* when your client is on their
screen, *viewing this screen* when theirs is on yours — and offers connect,
leave, wake and SSH exactly where each is possible.

Hosts come from `~/.config/kagami/hosts.conf`, never from a list in the code, and
Wake appears only where a MAC is configured, because Tailscale does not expose
them.

## Requires

`moonlight-qt` and `sunshine` on both ends, `tailscale`, `jq`, and the
`kagami-remote` helper from [kagami](https://github.com/dcqwqc/kagami).

## Settings

From the Plugins page: bitrate (zero derives it from the streamed resolution),
frame rate, how long the remote workspace may sit unwatched before the client is
dropped, whether the streamed host adopts your keyboard layout, and whether
system shortcuts are sent to the remote.

That last one matters more than it looks. Moonlight locks the pointer while its
window has focus, so a focus change is the only way out of a session — capturing
shortcuts takes away the keys that do it. `never` is the default for that reason.

`kagami-remote` reads the same settings, so a session started from the bar and
one started from a keybind behave identically.

## Status

Caelestia's plugin loader is not released yet — it lives on upstream's unmerged
`feat/plugins` branch, and the Plugins page there is still a mockup rendering
four fake cards. Nothing here can load until that lands.

It is built against the real schema rather than a guess at it: manifest keys and
the entry point type strings are taken from that branch's parser, so this should
need renaming rather than rewriting when the API ships.

## Install

Clone into Caelestia's plugin directory:

    git clone https://github.com/dcqwqc/caelestia-plugin-remote-desktop ~/.local/share/caelestia/plugins/remote-desktop

Or clone anywhere and add the parent to `path` in
`~/.config/caelestia/plugins.json`.

## Licence

GPL-3.0-or-later, matching Caelestia.
