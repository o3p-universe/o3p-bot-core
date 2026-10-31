# Agent guidance

## Local deployment

These notes describe this development environment. Keep machine-specific
deployment instructions out of public README files.

Deployment helpers operate on real services and may commit, push, restart Odoo,
or install/upgrade modules. Run them only when the user explicitly requests
the corresponding action; never use them for validation.

For a manual command-line upgrade after the addon is already available in an
Odoo addons path:

```bash
/opt/odoo20/venv/bin/python3 /opt/odoo20/odoo-bin \
  -c /etc/odoo20.conf \
  -d YOUR_DATABASE \
  -u o3p_bot_core \
  --stop-after-init \
  --workers=0
```

Restart Odoo after installing or upgrading the module.

This repository may contain local deployment helpers such as `upush.sh`,
`fulldeploy.sh`, and `restart_odoo19.sh`. They are intentionally ignored by Git
because they contain machine-specific deployment assumptions.

Before using them on a new host, check:

- the local checkout path
- the Odoo service name
- the Odoo database name
- the Odoo config and binary paths
- whether the remote branch exists

Deployment on this host uses branch `20.0`, service/user `odoo20`,
`/etc/odoo20.conf`, and `/opt/odoo20/o3p-bot-core`. Run `./fulldeploy.sh`
to deploy the local working tree to `persona.standalone.io`, with database,
filestore, and addon backups under `/var/backups/odoo20`. It installs Bot Core
if absent and upgrades it if installed. An optional commit-message argument
also commits/pushes first. `restart_odoo20.sh` only restarts the service;
`restart_odoo19.sh` remains a compatibility wrapper.
