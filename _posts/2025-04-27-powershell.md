---
title: I've returned to Linux but I miss Powershell
layout: post
permalink: /powershell/
date: 2025-04-27
---

At my previous job, we all used Windows. At first I insisted on doing everything in Windows Subsystem for Linux (WSL) or Linux-based Docker containers, but eventually I gave in and went native. 

I read [Learn Powershell in a Month of Lunches](https://www.manning.com/books/learn-powershell-in-a-month-of-lunches) so I'd actually understand things instead of cobbling together snippets from search or LLMs. 
 
Then, at a subsequent job, I went back to Linux. I thought I'd feel relieved to be back in my comfort zone of not developing on Windows. But instead, as I went back to the standard Linux shells (bash/zsh), I found myself missing some Powershell features. 
 
These are some features that I miss. 

## Tab completion for free

I still have not bothered to add tab completion to my shell scripts because of the extra steps involved. 

Powershell gives you this for free when you write a "cmdlet" (like a shell function). Here's an example cmdlet:
```powershell
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

```powershell
. Scripts.ps1  # Source it
Test-MyCmdlet -Ar  # Now press tab
Test-MyCmdlet -Argument  # Boom
```

## A debugger

Eventually your spicy one-liner in the CLI will grow out of control and you need to turn it into a script.
Sometimes, you might need to debug that script. 

vscode with the [Powershell](https://marketplace.visualstudio.com/items/?itemName=ms-vscode.PowerShell) extension does this with no extra steps. 

Add a breakpoint: 
![](/assets/powershell/powershell-run.png)

and hit run: 
![](/assets/powershell/powershell-debug.png)

## Editor support

vscode with the Powershell extension has decent autocomplete and linting. 

![](/assets/powershell/powershell-autocomplete.png)

The best bash alternative I've found is [shellcheck](https://www.shellcheck.net) for linting. I haven't found great editor support for bash/zsh script editing. 

## A package manager

`Install-Module` 👌

For example, `NTFSSecurity` eases the pain of dealing with NTFS permissions: 

```powershell
Install-Module NTFSSecurity -Scope CurrentUser
Get-NTFSOwner .
```

I **do not** miss dealing with NTFS permissions on Windows. I **do not** miss inherited permissions. 

## Automatic short commands

Instead of
```powershell
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

In Powershell, it's all baked in to the file, and vscode's autocomplete helps you write it. 

![](/assets/powershell/powershell-autocomplete-help.png)

```powershell
function Test-MyCmdlet {
    <#
    .SYNOPSIS
    This is just a demo cmdlet to show off Powershell. 

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


```
> Get-Help Test-MyCmdlet -Full 

NAME
    Test-MyCmdlet
    
SYNOPSIS
    This is just a demo cmdlet to show off Powershell.
    
    
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
```powershell
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

Everything is an object with named properties, which means you rarely need to use the usual `awk`, `tr`, `cut`, `sed`, etc to parse plaintext. 

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

I personally find this easier to memorize than the bash alternative of bespoke `ps` arguments (which aren't portable): 
```
ps -eo pid,pcpu,pmem,comm --sort=-pcpu | grep '[c]hrome'
```
or sorting on the column index which breaks if you shuffle the columns around and `%cpu` isn't in the 2nd column anymore: 
```
ps -axo pid,%cpu,%mem,command | grep '[c]hrome' | sort -k2 -nr
```

(Also, note the `grep [c]hrome` hack to avoid searching for the grep process itself). 

This is amazing for pipelines. Because all inputs and outputs are objects, Powershell knows the types of things going through a pipeline *before* running anything. For example, suppose I want to filter processes by their commandline arguments but I momentarily forgot the property. 

```powershell
Get-Process | Where-Object Com # Command? Commandline? idk, let's press tab
```
results in: 
```powershell
Get-Process | Where-Object CommandLine
CommandLine  Comments     Company      CompanyName
```

Ah, right, it's `CommandLine`. Now I can finish what I was doing, finding all running processes that Google might be responsible for: 

```powershell
Get-Process | Where-Object CommandLine -Match 'google' 
```

## Type checking

This is a nice sanity check to prevent you from accidentally switching the type of a variable:

```
> [int]$x = 10
> $x="foo"
MetadataError: Cannot convert value "foo" to type "System.Int32". Error: "The input string 'foo' was not in a correct format."
```


## Things I don't miss

* **The Powershell 5.1 and 7 distinction.** Windows ships with Powershell 5.1, but the latest features are in Powershell 7 (currently `7.5.1`). This means you either need to get everyone on your team to install 7 to share scripts, or you don't use the newer features in 7
* **The rest of Windows.** NTFS permissions, path separators are backslashes, there are too many ways to do things (`batch`, `vbscript`, `Powershell`, control panel GUIs), Windows Docker containers don't work. I'd add "vendor lock-in" here but we were already stuck in the walled garden and Powershell happened to be in it. 

## Conclusion

Powershell just seemed more intuitive and consistent than bash or zsh and I found I could do a lot more without asking Google or ChatGPT to remind me how to do things. 

There are newer shells like [fish](https://fishshell.com) which share these design goals. Maybe I should try them. 