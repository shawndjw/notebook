# Find package that contains file on Debian based systems

## Search installed packages
Use dpkg to search installed packages
```
dpkg -S filename-search-pattern
```

## Search package repository
Install `apt-file` to search all repository packages
```
sudo apt-get install -y apt-file
sudo apt-file update
sudo apt-file search filename-search-pattern
```
