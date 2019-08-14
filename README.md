# my-favourite-bash-commands

## Simple
```bash
# Find the largest files in a directory
ls -lhSr

# Find the largest files+folders in a directory
du -hs | sort -hu

# List all installed fonts
fc-list

# Convert Windows (DOS) newlines to Unix
dos2unix file.txt
# Alternatively, with built-in tools
perl -pi -e 's/\r\n/\n/g' file.txt
vim file.txt -c "set ff=unix" -c ":wq"

# Get information about a UTF-8 character
echo ϛ | uniname

# Create a backup version of a file/directory
cp -R file{,.bak}

# Get the full path to a file
readlink -f file.txt

# Test your speakers
speaker-test -t wav -c 6
```

## Advanced
```bash
# Find out which processes spend more time on boot
systemd-analyze plot > output.svg

# Commands to generate random passwords
head /dev/urandom | tr -dc A-Za-z0-9 | head -c 15 ; echo
head /dev/urandom | tr -dc A-Za-z0-9 | head -c `shuf -i 15-20 -n 1` ; echo
pwgen -s 15 7
grep -v \' /usr/share/dict/words | shuf -n 4 | paste -sd " "

# Mount a drive as a regular user
udisksctl mount -b /dev/sda1

# Get information about what your mouse & keyboard are doing
xev
evtest

# Recursively replace a string on all files in a directory
sed -i 's/old/new/g' `find -type f`

# Find which process is using a network port
sudo netstat -nlp | grep :80
sudo lsof -n -i :80
sudo ss -lptn 'sport = :8080'

# Paste image from the clipboard into a file
xclip -selection clipboard -t image/png -o > file.png

# Clear >1 week old entries from the journal
journalctl --vacuum-time=7d

# Copy many small files over SSH
rsync -avzh --progress -e ssh /local/path remoteuser@example.com:/remote/path

# Select a window and see which process it's from
ps -o pid,user,ni,comm,pcpu,pmem,start,args $(xprop -id $(xwininfo | grep "Window id" | awk '{print $4}') | grep _NET_WM_PID | awk '{print $3}')
```

## PDF
```bash
# Combine PDFs into a single file
pdftk i1.pdf i2.pdf output combined.pdf

# Keep page range 5-8 from a PDF
pdftk original.pdf cat 5-8 output range.pdf
```

## Second screen
```bash
# We assume that "LVDS1" is the original screen, and "VGA1" is an external screen.
# Execute `xrandr` to see the screens connected to your computer and their resolutions.

# Extend screen to the right
xrandr --output LVDS1 --auto --output VGA1 --right-of LVDS1 --auto

# Screen cloning for screens with different aspect ratios
xrandr --output LVDS1 --auto --output VGA1 --auto --same-as LVDS1 --scale 1.33x1

# Scale the screen to a larger resolution
xrandr --output LVDS1 --scale 1.17x1.17 --panning 1600x900

# VNC server the on current desktop
x11vnc -forever -loop -noxdamage -repeat -rfbport 5900 -shared --noxrecord
```

## Archives
```bash
# Mount a ZIP file as a directory
fuse-zip -r file.zip /tmp
```

## dpkg/apt packages
```bash
# List installed packages by size
dpkg-query -Wf '${db:Status-Status} ${Installed-Size}\t${Package}\n' | sed -ne 's/^installed //p'|sort -n

# Find which package a file belongs to
apt-find file
```

## Media
```bash
# Show total duration of MP3 files in a directory
total_seconds=$(( $(mp3info -p '%S + ' *.mp3) 0 )) bash -c 'printf "%02d:%02d:%02d\n" $((total_seconds / 3600)) $(((total_seconds % 3600) / 60)) $((total_seconds % 60))'
```

## git
```bash
# Single-line log
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# Remove everything that is untracked by git
git clean -f -d
```

### More commands
- [Remove everything from Docker](https://gist.github.com/beeman/aca41f3ebd2bf5efbd9d7fef09eac54d)

### Alias packs & utilities
- [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)
- [SCM Breeze](https://github.com/scmbreeze/scm_breeze)
- [Git Extras](https://github.com/tj/git-extras)
- [PyGitUp](https://github.com/msiemens/PyGitUp)
- [.tmux](https://github.com/gpakosz/.tmux)
