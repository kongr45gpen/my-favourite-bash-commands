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

# Create a new user
useradd -m username

# Copy with a progress bar
gcp -R /directory/1 /directory/2

# Copy many small files over SSH
rsync -Pavzh -e ssh /local/path remoteuser@example.com:/remote/path

# Select a window and see which process it's from
ps -o pid,user,ni,comm,pcpu,pmem,start,args $(xprop -id $(xwininfo | grep "Window id" | awk '{print $4}') | grep _NET_WM_PID | awk '{print $3}')

# Quickly create an HTTP file server on the current directory
python -m SimpleHTTPServer 8000

# Calculate how much time a 3-second task done 2 times a day for 5 years spends in hours
# See https://www.xkcd.com/1205/
units "5 years * 2 / days * 3 seconds" hours

# Test the read speed of a drive
sudo hdparm -Tt /dev/sda
```

## PDF
```bash
# Combine PDFs into a single file
pdftk i1.pdf i2.pdf output combined.pdf

# Keep page range 5-8 from a PDF
pdftk original.pdf cat 5-8 output range.pdf

# Convert SVG to PDF
rsvg-convert -f pdf -o output.pdf input.svg
inkscape input.svg --export-pdf=output.pdf
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

## Storage
```bash
# Mount a ZIP file as a directory
fuse-zip -r file.zip /tmp

# List all connected storage devices
lsblk

# List available space in connected partitions
df -h

# Record ISO file to flash drive
sudo dd if=gparted.iso of=/dev/yourdevice bs=1M status=progress iflag=direct oflag=direct

# Get information about a storage drive
sudo smartctl -A /dev/nvme0
sudo hdparm -I /dev/sda
```

## dpkg/apt packages
```bash
# List installed packages by size
dpkg-query -Wf '${db:Status-Status} ${Installed-Size}\t${Package}\n' | sed -ne 's/^installed //p'|sort -n

# Find which package a file belongs to
apt-file file
```

## Directory and file information
```bash
# Show total duration of MP3 files in a directory
total_seconds=$(( $(mp3info -p '%S + ' *.mp3) 0 )) bash -c 'printf "%02d:%02d:%02d\n" $((total_seconds / 3600)) $(((total_seconds % 3600) / 60)) $((total_seconds % 60))'

# Count files by extension
find . -type f | sed 's/.*\.//' | tr '[:upper:]' '[:lower:]' | sort | uniq -c | sort -n
```

## git
```bash
# Single-line log
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# Remove everything that is untracked by git
git clean -f -d
```

## Serial ports
```bash
# Start minicom on a 115000 baud/s line with some sane defaults
minicom -s -c on -b 3000000 -D /dev/ttyUSB0

# Set serial port baud rate with immediate flushing
stty -F /dev/ttyUSB0 2000000 -icanon

# Dump the serial data in a hexadecimal format
hexdump -ve '1/1 "(0x%01X "' -e '1/1 "%c) "" "' -e '1/0 "\n"' /dev/ttyUSB0
```

### More commands
- [Remove everything from Docker](https://gist.github.com/beeman/aca41f3ebd2bf5efbd9d7fef09eac54d)

### Alias packs & shell utilities
- [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)
- [SCM Breeze](https://github.com/scmbreeze/scm_breeze)
- [Git Extras](https://github.com/tj/git-extras)
- [PyGitUp](https://github.com/msiemens/PyGitUp)
- [.tmux](https://github.com/gpakosz/.tmux)

### Various utilities
- [crontab.guru](https://crontab.guru/)

### Friends
- [Stavrosfil/useful_commands](https://github.com/Stavrosfil/useful_commands)
- [Cool, but obscure unix tools](https://kkovacs.eu/cool-but-obscure-unix-tools)
