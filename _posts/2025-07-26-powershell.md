---
title: I've returned to Linux but I miss PowerShell
layout: post
permalink: /PowerShell/
date: 2025-07-26
---

At my previous job, we all used Windows. At first I insisted on doing everything in Windows Subsystem for Linux (WSL) or Linux-based Docker containers, but eventually I gave in and went native. 

I read [Learn PowerShell in a Month of Lunches](https://www.manning.com/books/learn-PowerShell-in-a-month-of-lunches) so I'd actually understand things instead of cobbling together snippets from search or LLMs. 
 
Then, at a subsequent job, I went back to Linux. I thought I'd feel relieved to be back in my comfort zone of not developing on Windows. But instead, as I went back to the standard Linux shells[^1] (bash/zsh), I found myself missing some PowerShell features. 

These are some features that I miss. 

## Tab completion for free

I still have not bothered to add tab completion to my shell scripts because of the extra steps involved. I am lazy. 

PowerShell gives you this for free when you write a "cmdlet" (like a shell function). Here's an example cmdlet:
```PowerShell
function Test-MyCmdlet {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory = $true)]
        [string]$Argument
    )

    Write-Output $Argument
}
```
Save it to `Scripts.ps1`, then: 

```PowerShell
. Scripts.ps1
Test-MyCmdlet -Ar  # Press tab
Test-MyCmdlet -Argument
```

## vscode's debugger

Eventually your spicy one-liner in the CLI will grow out of control and you need to turn it into a script.
Sometimes, you might need to debug that script. 

vscode with the [PowerShell](https://marketplace.visualstudio.com/items/?itemName=ms-vscode.PowerShell) extension does this with no extra steps. 

Add a breakpoint: 
![](/assets/PowerShell/PowerShell-run.png)
and hit run: 
![](/assets/PowerShell/PowerShell-debug.png)
[Bash Debug](https://marketplace.visualstudio.com/items?itemName=rogalmic.bash-debug) is a close second. Its main limitation is it doesn't seem to be aware of variables scopes. Whereas most debuggers can show you local variables like gdb's `info locals`, `bashdb`'s `info variables` shows way too much. 

To debug bash scripts I usually use `set -x` which is good enough. 

## vscode editing

vscode with the PowerShell extension has decent autocomplete and linting. 

![](/assets/PowerShell/PowerShell-autocomplete.png)
I haven't seen a bash/zsh script editor with this kind of autocomplete and I'm not sure how feasible it would be to make this work, considering current shell completions reflect they system they run on and not strictly the command syntax. 

For example, 
```
systemctl is-act
```
tab-completing to 
```
systemctl is-active
```

is fine for scripting, but 
```bash
systemctl is-active Netwo
```
tab-completing to
```bash
systemctl is-active NetworkManager.service
```
would be deceptive because it only works on systems where `NetworkManager` is installed. 

I will say [shellcheck](https://www.shellcheck.net) is quite good for linting. 

## A package manager

`Install-Module` 👌

For example, `NTFSSecurity` eases the pain of dealing with NTFS permissions: 

```PowerShell
Install-Module NTFSSecurity -Scope CurrentUser
Get-NTFSOwner .
```


## Automatic short commands

Instead of
```PowerShell
Test-MyCmdlet -Argument
```

you can do any of
```
Test-MyCmdlet -A
Test-MyCmdlet -Ar
Test-MyCmdlet -Arg
```
assuming there is no conflicting argument that would match. 

## Easy man pages

In PowerShell, it's all baked in to the file, and vscode's autocomplete helps you write it. 

For example, this cmdlet has the argument `Argument` and vscode autocompletes it as I write the documentation: 
![](/assets/PowerShell/PowerShell-autocomplete-help.png)
Then with a docstring that looks like this:
```PowerShell
function Test-MyCmdlet {
    <#
    .SYNOPSIS
    This is just a demo cmdlet to show off PowerShell. 

    .PARAMETER Argument
    A piece of text to demonstrate a commandline arg, e.g. "hello world". 
    
    #>

    [CmdletBinding()]
    param(
        [Parameter(Mandatory = $true)]
        [string]$Argument
    )

    Write-Output $Argument
}
```

the help page looks like this: 
```
> Get-Help Test-MyCmdlet -Full 

NAME
    Test-MyCmdlet
    
SYNOPSIS
    This is just a demo cmdlet to show off PowerShell.
    
    
SYNTAX
    Test-MyCmdlet [-Argument] <String> [<CommonParameters>]
    
    
DESCRIPTION
    

PARAMETERS
    -Argument <String>
        A piece of text to demonstrate a commandline arg, e.g. "hello world".
        
        Required?                    true
        Position?                    1
        Default value                
        Accept pipeline input?       false
        Accept wildcard characters?  false
        
    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216). 
    

```

## Command naming consistency

At first this seemed annoying and verbose. `Get-ChildItem` instead of `ls`? 

But then I noticed I could find the command I wanted faster than asking Google/ChatGPT. 

For example, I knew of `Get-Process`, which is like `ps` and shows all running processes, but how would I stop a process? Easy, find all commands whose verb operates on the noun `Process`:
```PowerShell
Get-Command -Noun Process
```
which returns: 
```
Debug-Process
Get-Process
Start-Process
Stop-Process
Wait-Process
```
`Stop-Process` it is. 

## Objects, not plaintext

Everything is an object with named properties, which I find much easier than `awk`, `tr`, `cut`, `sed`, etc to parse plaintext. 

For example, to see how much CPU each `chrome` process is using, then sort by most-to-least, we use the fact that `Get-Process` objects have `ProcessName`, `CPU` properties: 

```
Get-Process | where ProcessName -Match 'chrome'  | sort CPU -Descending

 NPM(K)    PM(M)      WS(M)     CPU(s)      Id  SI ProcessName
 ------    -----      -----     ------      --  -- -----------
     53    46.45     152.30       5.02    9084   1 chrome
     23    15.75      37.97       0.81    7980   1 chrome
     22    33.06     108.33       0.81    9556   1 chrome
     22    30.45      76.10       0.53    8496   1 chrome
     22    21.66      61.98       0.30    6808   1 chrome
     19    13.48      28.31       0.06    8824   1 chrome
     13     7.88      18.79       0.03    9188   1 chrome
     10     6.40       8.62       0.02    9984   1 chrome
```

I personally find this easier to memorize than the bash alternative of all those `ps` arguments, which don't generalize to other commands: 
```
ps -eo pid,pcpu,pmem,comm --sort=-pcpu | grep '[c]hrome'
```

(Also, note the `grep [c]hrome` hack to avoid searching for the grep process itself). 

This is amazing for pipelines. Because all inputs and outputs are objects, PowerShell knows the types of things going through a pipeline *before* running anything. For example, suppose I want to filter processes by their commandline arguments but I momentarily forgot the property. 

```PowerShell
Get-Process | Where-Object Com # Command? Commandline? idk, let's press tab
```
results in: 
```PowerShell
Get-Process | Where-Object CommandLine
CommandLine  Comments     Company      CompanyName
```

Ah, right, it's `CommandLine`. Now I can finish what I was doing, finding all running processes that Google might be responsible for: 

```PowerShell
Get-Process | Where-Object CommandLine -Match 'google' 
```

## Type checking

This is a nice sanity check to prevent you from accidentally switching the type of a variable:

```
> [int]$x = 10
> $x="foo"
MetadataError: Cannot convert value "foo" to type "System.Int32". Error: "The input string 'foo' was not in a correct format."
```

## Tab-completing your way around JSON or XML

Have you ever had a blob of JSON or XML lying around and found yourself repeatedly querying bits of it? 

PowerShell lets you turn JSON or XML into an object and you can tab-complete your way to glory. 

For example, given this in `sample.json`
```json
{
  "name": "John Doe",
  "age": 30,
  "isActive": true,
  "address": {
    "city": "New York",
    "coordinates": [40.7128, -74.0060]
  },
  "hobbies": ["reading", "coding"],
  "score": 95.5,
  "lastLogin": null
}

```

turn it in to an object: 
```powershell
$j=(Get-Content ./sample.json | ConvertFrom-Json)
```

then query its properties (with tab completion) like any other PowerShell object:
```
pwsh> $j.name
John Doe
pwsh> $j.address

city     coordinates
----     -----------
New York {40.7128, -74.006}

pwsh> $j.address.city
New York
pwsh> $j.hobbies
reading
coding
pwsh> $j.hobbies.Length
2
```

The same works for XML:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<person>
  <name>John Doe</name>
  <age>30</age>
  <isActive>true</isActive>
  <address>
    <city>New York</city>
    <coordinates>40.7128</coordinates>
    <coordinates>-74.0060</coordinates>
  </address>
  <hobbies>reading</hobbies>
  <hobbies>coding</hobbies>
  <score>95.5</score>
  <lastLogin></lastLogin>
</person>
```

```
pwsh> $x=[xml](Get-Content ./sample.xml)
pwsh> $x.person.name
John Doe
pwsh> $x.person.address

city     coordinates
----     -----------
New York {40.7128, -74.0060}

pwsh> $x.person.address.city
New York
pwsh> $x.person.hobbies
reading
coding
pwsh> $x.person.hobbies.Length
2
```

This is really nice for playing around with the result of a REST request. 

## Things I don't miss

**The PowerShell 5.1 and 7 distinction.** Windows ships with PowerShell 5.1, but the latest features are in PowerShell 7. This means you either need to get everyone on your team to install 7 to share scripts, or you don't use the newer features in 7. 

**No universal 'fail fast' mode**. In bash, exit code 0 is success, anything else is fail. `set -e` tells your script to fail fast and exit when it sees a nonzero code which is great for cutting down on debugging time. PowerShell sort of has this with 
```PowerShell
$ErrorActionPreference = 'Stop'
```

but it only works on programs that use PowerShell's exception mechanisms, like `Write-Error` and not on programs that use exit codes. For example:
```powershell
$ErrorActionPreference = 'Stop'

pwsh -Command "exit 1"
if($LASTEXITCODE -eq 1) {
    Write-Host "The last command failed but ErrorActionPreference doesn't apply here"
}

Write-Error "This will trigger a failure"
Write-Host "This won't run"
```

```
pwsh> ./sample.ps1
The last command failed but ErrorActionPreference doesn't apply here
Write-Error: This will trigger a failure
```


**The rest of Windows.** Such as: NTFS permissions (inherited permissions aren't fun), path separators are backslashes, there are too many ways to do things (`batch`, `vbscript`, `PowerShell`, multiple control panel GUIs), and Windows Docker containers are awkward. I'd add "vendor lock-in" here but we were already stuck in the walled garden and PowerShell happened to be in it. 

## Conclusion

PowerShell just seemed more intuitive and consistent than bash or zsh and I found I could do a lot more without asking Google/Kagi/ChatGPT to remind me how to do things. 

I had high hopes for [fish](https://fishshell.com) as the successor to bash but its [lack of a fail-fast mode](https://github.com/fish-shell/fish-shell/issues/510) is a dealbreaker. bash's `set -e` and PowerShell's `$ErrorActionPreference = 'Stop'` may not be perfect but they're way more convenient than checking return codes after every single instruction. 

[^1]: I realize PowerShell is cross-platform (I wrote this on macOS) but good luck evangelizing it to teams used to Linux. 