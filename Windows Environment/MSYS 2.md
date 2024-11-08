#msys2 #windows
[[Wezterm Setup]]
## Slow in AD

To fix do, create files:
```bash
mkpasswd -l -c > /etc/passwd
mkgroup -l -c > /etc/group
```

And configure /etc/nsswitch.conf to read from the files

```properties
# Begin /etc/nsswitch.conf
passwd: files
group: files
db_enum: cache builtin
db_home: cygwin desc
db_shell: cygwin desc
db_gecos: cygwin desc
# End /etc/nsswitch.conf
```

## Enable Anaconda

Add the following to .bash_profile or other sourced file:

```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
eval "$('/c/Users/MyUser/miniconda3/Scripts/conda.exe' 'shell.bash' 'hook')"
# <<< conda initialize <<<
```