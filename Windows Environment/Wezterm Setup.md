#msys2 #windows #wezterm
[[MSYS 2]]
## Setting Up WSL

```lua
config.wsl_domains = {
  {
    -- The name of this specific domain.  Must be unique amonst all types
    -- of domain in the configuration file.
    name = 'WSL:Ubuntu',
    
    -- The name of the distribution.  This identifies the WSL distribution.
    -- It must match a valid distribution from your `wsl -l -v` output in
    -- order for the domain to be useful.
	distribution = 'Ubuntu-22.04',
  },
}
```


## Setting Up Powershell and VCVarsAll and MSYS2

```lua
if wezterm.target_triple == 'x86_64-pc-windows-msvc' then
  table.insert(launch_menu, {
    label = 'PowerShell',
    args = { 'C:/Program Files/PowerShell/7/pwsh.exe', '-NoLogo' },
	domain = { DomainName = 'local' },
  })
  table.insert(launch_menu, {
    label = 'MSYS2',
    args = { 
	"C:\\msys64\\usr\\bin\\env.exe",
    "MSYS=enable_pcon", -- Enable pseudo console API for msys (maybe not needed under wezterm?) Actually, needed - without it, Ctrl-D does not close the terminal!
    "MSYSTEM=UCRT64",
    "/bin/bash", "--login",
	},
	domain = { DomainName = 'local' },
  })
  for _, vsvers in
    ipairs(
      wezterm.glob('Microsoft Visual Studio/20*', 'C:/Program Files (x86)')
    )
  do
    local year = vsvers:gsub('Microsoft Visual Studio/', '')
    table.insert(launch_menu, {
      label = 'x64 Native Tools VS ' .. year,
      args = {
        'cmd.exe',
        '/k',
        'C:/Program Files (x86)/'
          .. vsvers
          .. '/BuildTools/VC/Auxiliary/Build/vcvars64.bat',
      },
	  domain = { DomainName = 'local'},
    })
  end
end
```