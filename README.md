# PREREQUISITES OLD MACHINE

- Backup your Calibre book library following instructions at:
http://blog.calibre-ebook.com/2017/01/how-to-backup-move-and-export-your.html
- Complete a backup of the user's entire home directory
Note: refer to files under ~/rsync/ for reference
- Get a snapshot of all Firefox and Chrome extensions
- Backup the configuration of "auto tab discard" firefox extension
- Get a snapshot of all Gnome extensions
- Backup your FoxyProxy configuration (Firefox/Chrome)
Note: This is checked into github under files/foxyproxy
- Backup bookmarks and settings using Firefox Sync
- Check for new versions of any downloaded packages e.g. bluejeans, vpn clients etc.
- Update this playbook with all of the above wherever possible, and check it in

# PREREQUISITES NEW BUILD

- Install Ansible:
```
sudo dnf install ansible python4-dnf
```

Optional: Add bblasco to sudoers file
```
bblasco	localhost=(root)	NOPASSWD: /usr/bin/vagrant
```

Restore your home directory from the remote source via rsync

# USAGE/EXECUTION AND UPDATES

Add they SSH key for this machine in Github

https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account
https://github.com/settings/keys

```
git clone https://github.com/eraser215/fedoralaptop.git
cd fedoralaptop
ansible-playbook -i hosts build.yml --ask-become-pass --ask-vault-pass --check 
ansible-playbook -i hosts build.yml --ask-become-pass --ask-vault-pass
```

Change the remote URL so you can use your SSH key
https://docs.github.com/en/free-pro-team@latest/github/using-git/changing-a-remotes-url#switching-remote-urls-from-https-to-ssh

```
git remote set-url origin git@github.com:eraser215/fedoralaptop.git
```

# TASKS TO ADD TO THIS PLAYBOOK

Mouse
- [x] Switch mouse to left handed
- [ ] Set mouse speed to maximum
- [ ] Keep track pad right handed

Time
- [ ] Enable automatic time zone

Displays
- [ ] Enable night light

File Manager
- [ ] Sort folders before files
- [ ] Show action to permanently delete files and folders
- [ ] Switch view to list style
- [ ] Arrange by file type
- [ ] Allow you to free type another path into the title bar

Power management
- [ ] Via Gnome Tweaks, ensure closing lid does not put laptop to sleep
- [ ] Blank screen and lock after 15 minutes, rather than 5

Install Gnome extensions
Note that the command below doesn't appear to show all the extensions I have installed.  Why?
Because not all extensions can be installed as RPMs using DNF
It turns out you can sync all your gnome extensions using your google account, as per the instructions here:
https://askubuntu.com/questions/1135175/how-do-i-automatically-reinstall-gnome-shell-extensions-after-reinstalling-ubunt
1. Install the Firefox add-on called "GNOME Shell integration"
2. Have it sync your extensions for you...?
3. Pray

OR install this extension and follow the instructions:
https://github.com/oae/gnome-shell-extensions-sync

My gist location is:
https://gist.github.com/eraser215/251271b1c756e28e4149c2ab63d5838c
My gist token is:
fafbb4f71f99a6633ba4bd950573db742b23d885
This appears to be broken somehow

Current list of Gnome Shell Extensions:
- OBSOLETE https://extensions.gnome.org/extension/15/alternatetab/
- https://blogs.gnome.org/fmuellner/2018/10/11/the-future-of-alternatetab-and-why-you-need-not-worry/
- https://extensions.gnome.org/extension/6/applications-menu/
- https://extensions.gnome.org/extension/779/clipboard-indicator/
- https://extensions.gnome.org/extension/307/dash-to-dock/
- https://extensions.gnome.org/extension/904/disconnect-wifi/
- https://extensions.gnome.org/extension/1036/extensions/
- https://extensions.gnome.org/extension/600/launch-new-instance/
- https://extensions.gnome.org/extension/921/multi-monitors-add-on/
- https://extensions.gnome.org/extension/118/no-topleft-hot-corner/
- https://extensions.gnome.org/extension/8/places-status-indicator/
- https://extensions.gnome.org/extension/19/user-themes/
- BROKEN, and obsolete https://extensions.gnome.org/extension/602/window-list/
- https://extensions.gnome.org/extension/1160/dash-to-panel/ This has an import/export settings option which may be helpful
- https://extensions.gnome.org/extension/906/sound-output-device-chooser/

DONE: In multi monitors add on, disable "show panel on additional monitors"

DONE: Change the default alt-tab behaviour as per the link below:
- https://blogs.gnome.org/fmuellner/2018/10/11/the-future-of-alternatetab-and-why-you-need-not-worry/
- Go to keyboard shortcuts, seach for "swi win" ie "Switch Windows", and replace it with alt-tab, as there is no shortcut currently assigned.
- Alt-tab is normally used for "Switch Applications"

How to open Gnome looking glass
- Alt+F2
- Then type "lg"

Enable Chrome Sync, which should take care of all extensions etc
Install Chrome extensions:
- Bluejeans for Google Calendar: https://chrome.google.com/webstore/detail/bluejeans-for-google-cale/iedelpfmeejalepbpmmfbfnfoeojohpp
- Google Docs Offline: https://chrome.google.com/webstore/detail/google-docs-offline/ghbmnnjooekpmoecnnnilnnbdlolhkhi
- uBlock Origin: https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm
- Bitwarden: https://chrome.google.com/webstore/detail/bitwarden-free-password-m/nngceckbapebfimnlniiiahkandclblb
- Open in Firefox: https://chrome.google.com/webstore/detail/open-in-firefox/lmeddoobegbaiopohmpmmobpnpjifpii
- Privacy Badger: https://chrome.google.com/webstore/detail/privacy-badger/pkehgijcmpdhfbdbbnkijodmdjhbjlgp
- Not in use - KeePass Tusk
- Not in use - Google Keep Chrome Extension
- Not in use - FoxyProxy Standard
- Not in use - Google Calendar

Enable Offline mail in your gmail settings (not possible in Firefox)

Install GMail addons for Chrome/Firefox
- Trello
- Others?

Restore bookmarks and settings using Firefox Sync
Install Firefox extensions
- Firstly, login and sync.  It should download the extensions for you
- Open the Container tabs extension and allow it to sync
- Restore the list of auto tab discard exceptions (auto-tab-discard-preferences.json)
- Restore the Tree Style Tabs config (configs-treestyletab@piro.sakura.ne.jp.json)

Reference list of Firefox extensions/add ons
- Auto Tab Discard https://add0n.com/tab-discard.html
- BitWarden https://bitwarden.com/
- Facebook Containers https://github.com/mozilla/contain-facebook
- Firefox Multi Account Containers https://github.com/mozilla/multi-account-containers#readme
- FoxyProxy Standard https://getfoxyproxy.org/
- Gnome Shell Integration https://wiki.gnome.org/Projects/GnomeShellIntegrationForChrome
- KeePass Tusk https://subdavis.com/Tusk
- Open in Chrome http://add0n.com/open-in.html?from=chrome
- Tab Mover https://code.guido-berhoerster.org/addons/firefox-addons/tab-mover/
- Tree Style Tabs http://piro.sakura.ne.jp/xul/_treestyletab.html.en
- uBlock Origin http://piro.sakura.ne.jp/xul/_treestyletab.html.en
- Honey https://www.joinhoney.com/
- KeePass Tusk https://subdavis.com/Tusk
- Open in Chrome http://add0n.com/open-in.html?from=chrome
- Tab Mover https://code.guido-berhoerster.org/addons/firefox-addons/tab-mover/
- Tree Style Tabs http://piro.sakura.ne.jp/xul/_treestyletab.html.en
- uBlock Origin addons://detail/uBlock0@raymondhill.net
- Joplin Web Clipper https://addons.mozilla.org/en-US/firefox/addon/joplin-web-clipper/
- Containerise https://addons.mozilla.org/en-US/firefox/addon/containerise/
- Privacy Badger https://www.eff.org/privacybadger
- Intention https://addons.mozilla.org/en-US/firefox/addon/intention/
- enhanced-h264ify: https://addons.mozilla.org/en-US/firefox/addon/enhanced-h264ify/
- Bypass Paywalls: https://github.com/iamadamdev/bypass-paywalls-chrome

Disable ctrl-q shortcut in Firefox as per https://superuser.com/questions/1318336/how-to-disable-ctrlq-shortcut-in-firefox-on-linux
about:config
browser.sessionstore.warnOnQuit true
browser.warnOnQuit true

Log in to your Pocket account
Configure Multi Account containers to use the appropriate container for each tab

Configure Joplin
Tell it to use Dropbox and authenticate it to synchronise
Change the default date format
Switch default editor to vi mode

Configure Evernote
Tools->Sync, then log in to your account

Install cockpit
dnf install cockpit
systemctl enable cockpit.socket
systemctl start cockpit
then connect to localhost:9090

DONE: Configure Terminator to use Putty style paste
Note: If you do this, use Shift+F10 to access the menus

# QUESTIONS/UPDATES REQUIRED

Try IDM integration as per:
https://mojo.redhat.com/docs/DOC-1199178
(See Engineering Server - non-fresh RHEL 7, non-fresh RHEL 8 or RHEL 5 or 6)

NOTES ON SOME OF THE TASKS COMPLETED

MANUAL TASKS THAT MAY NOT BE POSSIBLE TO AUTOMATE

- Change display position of second screen relative to laptop screen

Configure SpiderOak backups
https://redhat.service-now.com/help?id=kb_article&sys_id=c09f0e372b66b8004c71dc0e59da15ff
https://redhat.service-now.com/help?id=kb_article&sysparm_article=KB0000771
http://hdn.corp.redhat.com/rhel7-csb-stage/repoview/SpiderOakGroups.html

Connect to Wifi
https://redhat.service-now.com/help?id=kb_article&sysparm_article=KB0001616
or just grab the files for the SSIDs you want from /etc/sysconfig/network-scripts/
```
[bblasco@bblasco_fedora cloudfedora30]$ nmcli conn show --order type
NAME                UUID                                  TYPE      DEVICE
...
Red Hat Guest       0ccfd13b-5920-4fda-924d-059d0178993c  wifi      --
WiFi-6FE7           26e5b1fc-3171-4964-be2a-5fc283c1db28  wifi      --
eraser215           27e8eeb8-46b9-4cc6-8acd-a139711e2fa2  wifi      --
WiFi-6FE7-5G        3b94cd43-0f68-485b-a220-2d6fb657c54a  wifi      --
TelstraC083AB       5d30249a-c8a9-44bf-9763-8f087339cf99  wifi      --
Red Hat             916403a9-1bd7-4386-b1d9-7034396dac40  wifi      wlp4s0
Yarra               931b30d6-330d-440e-82e0-b7be4c5e731d  wifi      --
eraser215op6        a8598908-f3d3-45e0-ad29-df92c6ed2558  wifi      --
```
