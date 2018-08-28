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

# Get information about a UTF-8 character
echo ϛ | uniname
```

## Intermediate
```bash
# Find out which processes spend more time on boot
systemd-analyze plot > output.svg

# Screen cloning for screens with different aspect ratios
xrandr --output LVDS1 --auto --output VGA1 --auto --same-as LVDS1 --scale 1.33x1

# Commands to generate random passwords
head /dev/urandom | tr -dc A-Za-z0-9 | head -c 15 ; echo
head /dev/urandom | tr -dc A-Za-z0-9 | head -c `shuf -i 15-20 -n 1` ; echo
pwgen -s 15 7
shuf /usr/share/dict/words -n 4 | paste -sd " "

# Mount a drive as a regular user
udisksctl mount -b /dev/sda1
```

## PDF
```bash
# Combine PDFs into a single file
pdftk i1.pdf i2.pdf output combined.pdf

# Keep page range 5-8 from a PDF
pdftk original.pdf cat 5-8 output range.pdf
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
```

## Media
```bash
# Show total duration of MP3 files in a directory
total_seconds=$(( $(mp3info -p '%S + ' *.mp3) 0 )) bash -c 'printf "%02d:%02d:%02d\n" $((total_seconds / 3600)) $(((total_seconds % 3600) / 60)) $((total_seconds % 60))'
```
