# my-favourite-bash-commands

## Simple
```bash
# Find the largest files in a directory
ls -lhSr

# List all installed fonts
fc-list
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
