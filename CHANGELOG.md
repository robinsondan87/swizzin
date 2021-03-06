# Changelog

## [1.0 Stable]

### November 13th, 2017

### Added
- ruTorrent now ships with a spectrogram plugin for analyzing audio files. Thus, installer now installs sox and applies the correct config for binary location

### Changed
- Default proxy addresses to 127.0.0.1 to avoid DNS resolution errors for localhost
- Fixed flood installer for new build steps
- `box help` is now a bit more helpful

### Fixed
- Subsonic install/reverse proxy issues
- pyLoad install and configuration should now run properly
- Fringe scenarios in which quotas might not apply fstab edits correctly
- rtorrent download folder permissions for subusers
- libfcgi binary wasn't being installed on Debian 9 and newer Ubuntu versions
- `box upgrade plex` -- this command should not be run as root

## [1.0.0 Pre-Stable]

### October 9th, 2017

### Added
- php7.0-mbstring was missing from the nginx installer. This may have caused php errors in ruTorrent under rare circumstances.

### Changed
- Refactored keyserver calls for mono, sonarr and sabnzbd-extras repositories
- Removed python-software-properties in favour of allowing it to be marked for installation automatically with software-properties-common

### Fixed
- Certain do or die commands were missing parenthesis causing the exit to trigger unconditionally. These have been fixed.
- Removed reference to removed function _ruconf in scripts/install/rtorrent.sh
- `box panel fix-disk root/home` will now function properly again (the refactor of quickbox_dashboard left it non-functional)
- Quota installer may have failed due to the installer's inability to match a pattern. Pattern has now been expanded to include tab characters and should fix any issues.

### September 29th, 2017

### Changed
- Disabled HSTS in nginx SSL params. [Why?](https://github.com/liaralabs/swizzin/commit/5f9af8d3dea9ebd06fa072c322f8fa7b54b431b2)
- Moved swizzin PATH variables from bashrc to profile
- Moved panel installation script to nginx directory and left a wrapper in its place
- `box update` will now update the panel as well. In the event that `git reset HEAD --hard` fails to reset the panel repo to a pullable state, a backup and restore function will run.

### Fixed
- Updated Plex repository location
- Flood script cleanup
- box chpasswd was using an incorrect variable to insert the password into deluge-web hostlists
- rTorrent removal script had a syntax error
- Added a github mirror for xmlrpc-c in the event that SourceForge goes down for an extended period again
- Cleaned up the new GUIs function in the installer to ensure that the autodl plugin for ruTorrent installs properly if it should be installed
- Panel: lang_de script attempted to cat its config into the wrong file.
- Other minor fixes

## [1.0.0-RC2]

### September 21st, 2017

### Added
- Flood is now available!
  - If you have nginx installed, you can access it from the web at /flood. Otherwise, flood port will be printed upon install. Please note, SSL is not currently configured for non-proxied configurations. If you need SSL without nginx, you will have to configure it yourself.
  - Flood has a complimentary upgrade script. `box upgrade flood`
  - Please note that there are currently some bugs when using both Flood's authentication and nginx basic authentication. You might need to complete nginx authentication a couple times. Flood authentication will be disabled once the option exists. Until then there is no fix.
- box now has an upgrade function to run scripts in the scripts/upgrade directory
  - Current scripts: deluge, flood, nginx, ombi, plex, rtorrent, rutorrent
- Logoff plugin for ruTorrent

### Changed
- ruTorrent has been decoupled from the rTorrent installation. (run `box upgrade rutorrent` or `touch /install/.rutorrent.lock` if you already have ruTorrent installed.)
  - If you need ruTorrent please be sure to check both nginx and ruTorrent during the initial installation. A web interface will *NOT* be installed by default.
- rTorrent uninstall will now purge *ALL* related packages (ruTorrent and Flood). Be careful!
- Quickbox Dashboard has been rebased with the latest changes
- Made error for usernames with capital letters more noticeable.

### Fixed
- Let's encrypt script now checks for nginx before running
- Master user is now given sudo permission in setup.sh not install/rtorrent.sh (oops!)
- Upstreams in /etc/nginx/conf.d were not being removed if extra users were deleted
- Fixed a bad else statement in xmr-stak-cpu installer

### September 13th, 2017

### Added
- Dynamic Deluge reverse proxies (/deluge)
- Dynamic Deluge and rTorrent download directories for nginx (/rtorrent.downloads & /deluge.downloads)
- Upgrade scripts (these are not tied into box yet. Please run them manually at this time)
  - nginx (resets configurations to swizzin defaults)
  - rtorrent (recompile and change version if wanted; refresh depends)
  - deluge (recompile and change version if wanted)
  - plex ([updateplex](https://github.com/mrworf/plexupdate) by mrworf)
  - ombi
- Compile mktorrent from source for -s flag (19c823362fb69743a5b6178fecbedffb781ace74)
- Add panel fix-disk to box `box panel fix-disk` (for root or home disk widget) (c45f9ae6a269b3a97d9511bca74ac0cea9fab691)

### Changed
- Removed package management from the quickbox panel. Please use box for everything.
- irssi systemd ExecStop method gentler (73f2ca8c19f083e692efef71a0eae69b395dda0b)
- Package sources for ZNC (1fa52d8c3c809fa00527b0760ecea0b8bf40a748)
- Move stop/start functions in nginx configuration scripts to inside the script to support stand-alone install (for example, if you chose to install nginx after your initial install) (4d92eea4443e4d3f84f47e8df71bdc1a582ec27f)
- Under-the-hood improvements for box (475aadadd71d8ab4990607e4493e40ffbbe10423)
- Current subsonic version is now determined automatically (6be077e7fec1b62516086a1fe546a2d9595e8152)

### Fixed
- Overzealous sed function in nzbHydra (9b9635a1083333ec55bd867c185445c172ff6a59)
- box adduser will no longer ask for the rtorrent version when adding a user (98502de5a6e5f0a833729e84e419ebda7f943834)
- Lots of other bugs

## [1.0.0-RC1]

### Added
- pyMedusa package
- netdata package
- shellinabox package
- xmr-stak-cpu package (monero miner or dev donation method)
- php-fpm-cli to allow functions like clearing opcache without needing to disconnect current web sessions

### Changed
- ZNC now uses systemd
- Deluge-web will now automatically connect to the default daemon (you will still need to connect the first time)
- vsftpd intial config (3af310d4d73301a0c896610a412cbcc2adf5ad4c)

### Fixed
- Fix for providers who ship noexec on temp (Leaseweb)
- Ensure scripts which use PPAs install software-properties-common before attempting to add
- Add php directive to ruTorrent to ensure plugins like httprpc are actually functioning for their intended usage (6e4f9c8c697efc838928ba4d0d45dbe9d705659d)
- Nextcloud is functional
- quota installer is more useful
- proxy_redirect will no longer attempt to redirect to localhost
- prevent nested while loops creating infinite loops
- emby install issues

