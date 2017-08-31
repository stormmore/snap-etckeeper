# Overview

etckeeper is a collection of tools to let /etc be stored in a git, mercurial, darcs, or bzr repository. It hooks into apt (and other package managers including yum and pacman-g2) to automatically commit changes made to /etc during package upgrades. It tracks file metadata that revison control systems do not normally support, but that is important for /etc, such as the permissions of /etc/shadow. It's quite modular and configurable, while also being simple to use if you understand the basics of working with revision control.

# Build snap

```
cd <path to cloned repo>
snapcraft cleanbuild
```

# Install snap

```
cd <path to cloned repo>
snap install etckeeper_*.snap --classic --dangerous
```

# Configuration

All the current configuration fields that are configuration options in
etckeeper.conf. To change configuration use the `sudo snap set etckeeper
KEY=VALUE [KEY=VALUE ...]`

Key | Type | Default | Description
----|-------|------------
`vcs` | string | `git` | Version control system to use, options are `git`, `bzr`, `hg`, or `darcs`.
`commit-options` | string | | Flags to pass to the VCS command, selects the correct VCS based on configured VCS. The default for `darcs` is `-a`, and setting this will overwrite the current value
`avoid-daily-autocommits` | int | | Setting this to `1` will disable the daily commits
`avoid-special-file-warning` | int | | Setting this to `1` will disable the special file warning (enabled by cronjob regardless)
`avoid-commit-before-install` | int | | Setting this to `1` will disable the pre-install commit
`highlevel-package-manger` | string | `apt` | The high level package manager that is being used
`lowlevel-package-manager` | string | `dpkg` | The low level package manager that is being used
