---
description: Update versions in all plugrn files for specific plugin
arguments: [plugin version]
---

# Simple version updater for skills.

This is a marketplace repository where we ship commands/skills for
users.

It should be backend agnostic and be able to install the plugins for
all AI tools.

Therefore there are several configuration files in the repo with
duplicate information such that all AI tools can install it from
the same repo.

This skills objective is to easily update a version specification
in all configuration files in this repo.

It should do this by locating the current version specification for
the plugin named "$plugin", and update the version to "$version".

# Finalize

Report which files are edited, and what you changed in these files.

Do NOT commit.
