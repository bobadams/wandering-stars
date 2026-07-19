# The Wandering Stars

Standalone geocentric planetary ephemeris wheel.
Served at https://slamad.ong/planets.html (nginx: location = /planets.html,
root ~/Sites/wandering-stars).

Single self-contained file, no build step. Shareable ?t=<ms> permalinks
encode the displayed moment.

## Deploy

Pushing to `main` is the deploy. A launchd agent on the mac mini
(`~/Library/LaunchAgents/ong.slamad.wandering-stars-deploy.plist`, running
`~/.local/bin/wandering-stars-autodeploy.sh` every 2 min) fetches origin/main
and fast-forwards the served checkout at `~/Sites/wandering-stars`. It is
fast-forward-only, so a dirty or diverged checkout is left untouched rather
than clobbered. Log: `~/Library/Logs/wandering-stars-deploy.log`.

Force an immediate deploy instead of waiting for the poll:
`launchctl kickstart -k gui/$(id -u)/ong.slamad.wandering-stars-deploy`.
