# my-favourite-bash-commands

## Simple
```bash
# Find the largest files in a directory
ls -lhSr

# List all installed fonts
fc-list

# Convert Windows (DOS) newlines to Unix
perl -pi -e 's/\r\n/\n/g' file.txt
```

## Intermediate
```bash
# Find out which processes spend more time on boot
systemd-analyze plot > output.svg
```

## PDF
```bash
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
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n
```
