# WillowsUsefulScripts
Scripts and One-liners, et cetera.

## Git

### Git Log and gitk
1. Print to command line the last -n commits from whatever the most recent one is, one line per commit, branches in color:
   ```powershell
   git log --graph --oneline --all --decorate --color -n 10;
   ```
1. Interactive exploration of git history:
   ```powershell
   gitk --all;
   ```
1. PowerShell function to take all args and turn them into a commit message:
   ```powershell
   function gitmit {Param() begin{} process {$out = ''; foreach ($i in $args) {$out += "$i "}; git commit -m $out } end{}}
   ```

## PowerShell Quality Of Life
```powershell
function newdir {PARAM($Path)  new-item -ItemType Directory -Path $Path }

function newfile {PARAM( [Parameter(Mandatory=$true,Position=0)]$Name,[Parameter(Mandatory=$false,Position=1)]$Value='')  new-item -ItemType File -Path . -Name $Name -Value $Value}

function Get-HistoryWhere {Param([Parameter(Mandatory=$false,Position = 0)][String]$Contains,[Parameter(Mandatory=$false,Position = 1)][Int]$Last) $hist = Get-History; If ($PSBoundParameters.ContainsKey('Last') ) { $hist = $hist | Select-Object -Last $Last } ; If ($PSBoundParameters.ContainsKey('Contains')) {$hist = $hist | where {$_.CommandLine -like "*$Contains*"} }; return $hist}

new-alias import -Value 'import-module'

function Rename-PSWindow {$host.ui.RawUI.WindowTitle = $($args -join ' ')}
```