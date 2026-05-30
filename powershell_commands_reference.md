# ⚡ PowerShell Commands Reference
> Complete cmdlet & alias reference

**314 commands** across **21 categories** — Generated May 30, 2026

---

## Table of Contents

- [Navigation](#navigation) `6`
- [File System](#file-system) `21`
- [Text & String](#text--string) `29`
- [Objects & Pipeline](#objects--pipeline) `20`
- [Variables & Data](#variables--data) `21`
- [Processes](#processes) `13`
- [Services](#services) `9`
- [Network](#network) `16`
- [System Info](#system-info) `18`
- [Registry](#registry) `10`
- [Security](#security) `12`
- [Users & Groups](#users--groups) `13`
- [Modules & Packages](#modules--packages) `16`
- [Remoting](#remoting) `11`
- [CIM & WMI](#cim--wmi) `12`
- [Scheduling](#scheduling) `10`
- [Error Handling](#error-handling) `10`
- [Scripting & Flow](#scripting--flow) `16`
- [Environment](#environment) `11`
- [Formatting & Output](#formatting--output) `12`
- [Misc](#misc) `28`

---

## Navigation

### `Set-Location` <sub>cd / sl / chdir</sub>

Change working directory

**Syntax**

```bash
Set-Location [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Path` | destination |
| `-PassThru` | return new loc |
| `-LiteralPath` | no wildcards |
| `~` | home dir (PS 6+) |

---

### `Get-Location` <sub>pwd / gl</sub>

Print current directory

**Syntax**

```bash
Get-Location
```

**Options**

| Flag | Description |
|------|-------------|
| `-PSProvider` | filter provider |
| `-PSDrive` | filter drive |
| `-Stack` | from location stack |
| `-StackName` | named stack |

---

### `Push-Location` <sub>pushd</sub>

Push location to stack

**Syntax**

```bash
Push-Location [path]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Path` | directory |
| `-StackName` | named stack |
| `-PassThru` | return loc |

---

### `Pop-Location` <sub>popd</sub>

Pop location from stack

**Syntax**

```bash
Pop-Location
```

**Options**

| Flag | Description |
|------|-------------|
| `-StackName` | named stack |
| `-PassThru` | return loc |

---

### `Get-ChildItem` <sub>ls / dir / gci</sub>

List directory contents

**Syntax**

```bash
Get-ChildItem [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | recurse dirs |
| `-Force` | include hidden |
| `-Filter` | glob filter |
| `-Include` | include pattern |
| `-Exclude` | exclude pattern |
| `-Depth` | limit depth |
| `-File` | files only |
| `-Directory` | dirs only |
| `-Name` | names only |
| `-LiteralPath` | no wildcards |

---

### `Get-Item` <sub>gi</sub>

Get file/dir/reg item

**Syntax**

```bash
Get-Item [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Path` | with wildcards |
| `-LiteralPath` | exact path |
| `-Force` | include hidden |
| `-Stream` | NTFS stream |

---


## File System

### `Copy-Item` <sub>cp / copy / cpi</sub>

Copy files or directories

**Syntax**

```bash
Copy-Item [-Path] <src> [-Destination] <dst>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | recursive |
| `-Force` | overwrite |
| `-Container` | preserve dirs |
| `-PassThru` | return item |
| `-Filter` | glob |
| `-Exclude` | -Include |
| `-Confirm` | -WhatIf |

---

### `Move-Item` <sub>mv / move / mi</sub>

Move or rename items

**Syntax**

```bash
Move-Item [-Path] <src> [-Destination] <dst>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | overwrite |
| `-PassThru` | return item |
| `-Filter` | -Include  -Exclude |
| `-Confirm` | -WhatIf |

---

### `Remove-Item` <sub>rm / del / ri / rd / erase</sub>

Delete items

**Syntax**

```bash
Remove-Item [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | recursive |
| `-Force` | hidden/read-only |
| `-Confirm` | prompt |
| `-WhatIf` | dry run |
| `-Filter` | -Include  -Exclude |
| `-Stream` | delete NTFS stream |

---

### `New-Item` <sub>ni</sub>

Create file, directory, etc.

**Syntax**

```bash
New-Item [-Path] <path> -ItemType <type>
```

**Options**

| Flag | Description |
|------|-------------|
| `-ItemType` | File/Directory/SymbolicLink/HardLink |
| `-Value` | initial content |
| `-Force` | overwrite / create path |
| `-Confirm` | -WhatIf |

---

### `Rename-Item` <sub>ren / rni</sub>

Rename a file or directory

**Syntax**

```bash
Rename-Item [-Path] <path> [-NewName] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -PassThru |
| `-Confirm` | -WhatIf |

---

### `Get-Content` <sub>cat / gc / type</sub>

Read file contents

**Syntax**

```bash
Get-Content [-Path] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-TotalCount` | / -Head N lines |
| `-Tail` | N last lines |
| `-Raw` | single string |
| `-Encoding` | UTF8/ASCII/etc |
| `-Delimiter` | line sep |
| `-Wait` | follow mode |
| `-Filter` | -Include  -Exclude |
| `-Stream` | NTFS stream |

---

### `Set-Content` <sub>sc</sub>

Write to file (replace)

**Syntax**

```bash
Set-Content [-Path] <file> [-Value] <val>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Encoding` | UTF8/ASCII/etc |
| `-Force` | overwrite read-only |
| `-NoNewline` | skip newline |
| `-Confirm` | -WhatIf |
| `-PassThru` | return val |

---

### `Add-Content` <sub>ac</sub>

Append to file

**Syntax**

```bash
Add-Content [-Path] <file> [-Value] <val>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Encoding` | -Force |
| `-NoNewline` | -PassThru |
| `-Confirm` | -WhatIf |

---

### `Clear-Content` <sub>clc</sub>

Clear file contents

**Syntax**

```bash
Clear-Content [-Path] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -Filter |
| `-Confirm` | -WhatIf |

---

### `Test-Path`

Test if path exists

**Syntax**

```bash
Test-Path [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-PathType` | Container/Leaf/Any |
| `-LiteralPath` | exact |
| `-IsValid` | check syntax only |
| `-Filter` | -Include  -Exclude |

---

### `Resolve-Path` <sub>rvpa</sub>

Resolve wildcards in path

**Syntax**

```bash
Resolve-Path [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Relative` | relative paths |
| `-LiteralPath` | -ProviderPath |

---

### `Split-Path`

Get part of a path

**Syntax**

```bash
Split-Path [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Parent` | parent dir (default) |
| `-Leaf` | filename |
| `-LeafBase` | name without ext |
| `-Extension` | extension |
| `-Qualifier` | drive |
| `-IsAbsolute` | test |
| `-NoQualifier` | no drive |

---

### `Join-Path`

Combine path components

**Syntax**

```bash
Join-Path <parent> <child>
```

**Options**

| Flag | Description |
|------|-------------|
| `-AdditionalChildPath` | extra segments |
| `-Resolve` | resolve result |

---

### `Convert-Path` <sub>cvpa</sub>

Convert PS path to provider path

**Syntax**

```bash
Convert-Path [-Path] <path>
```

---

### `Get-Acl`

Get security descriptor (ACL)

**Syntax**

```bash
Get-Acl [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Audit` | include SACL |
| `-Filter` | -Include  -Exclude |
| `-LiteralPath` | — |

---

### `Set-Acl`

Apply security descriptor

**Syntax**

```bash
Set-Acl [-Path] <path> -AclObject <acl>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Confirm` | -WhatIf |
| `-ClearCentralAccessPolicy` | — |
| `-PassThru` | — |

---

### `Get-FileHash`

Compute file hash

**Syntax**

```bash
Get-FileHash [-Path] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Algorithm` | SHA256/SHA512/MD5/SHA1 |
| `-LiteralPath` | -InputStream |

---

### `Compress-Archive`

Create ZIP archive

**Syntax**

```bash
Compress-Archive -Path <src> -DestinationPath <zip>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Update` | add to existing |
| `-Force` | overwrite |
| `-CompressionLevel` | Optimal/Fastest/NoCompression |

---

### `Expand-Archive`

Extract ZIP archive

**Syntax**

```bash
Expand-Archive -Path <zip> -DestinationPath <dir>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | overwrite |
| `-PassThru` | return items |

---

### `Copy-ItemWithProgress`

Copy with progress (custom)

**Syntax**

```bash
(use Robocopy for native progress)
```

---

### `Invoke-Item` <sub>ii</sub>

Open item with default app

**Syntax**

```bash
Invoke-Item [-Path] <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Filter` | -Include  -Exclude |
| `-Confirm` | -WhatIf |

---


## Text & String

### `Select-String` <sub>sls</sub>

Search text in files/strings

**Syntax**

```bash
Select-String [-Pattern] <re> [-Path] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-CaseSensitive` | — |
| `-SimpleMatch` | literal |
| `-AllMatches` | all per line |
| `-NotMatch` | invert |
| `-Quiet` | return bool |
| `-List` | first match per file |
| `-Encoding` | -Include  -Exclude |
| `-Context` | N lines before/after |
| `-LiteralPath` | — |

---

### `Get-Content` <sub>cat</sub>

Read file content

**Syntax**

```bash
Get-Content <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Raw` | whole file |
| `-Tail` | N |
| `(see` | File System) |

---

### `Out-String`

Render objects as string

**Syntax**

```bash
cmd | Out-String
```

**Options**

| Flag | Description |
|------|-------------|
| `-Stream` | line by line |
| `-Width` | line width |

---

### `ConvertTo-Json`

Convert to JSON

**Syntax**

```bash
obj | ConvertTo-Json
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | N (default 2) |
| `-Compress` | no whitespace |
| `-EnumsAsStrings` | — |
| `-AsArray` | force array |

---

### `ConvertFrom-Json`

Parse JSON string

**Syntax**

```bash
json | ConvertFrom-Json
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | N |
| `-AsHashtable` | — |
| `-NoEnumerate` | — |

---

### `ConvertTo-Csv`

Convert to CSV

**Syntax**

```bash
obj | ConvertTo-Csv
```

**Options**

| Flag | Description |
|------|-------------|
| `-Delimiter` | -NoTypeInformation |
| `-UseQuotes` | Always/Never/AsNeeded |

---

### `ConvertFrom-Csv`

Parse CSV string

**Syntax**

```bash
csv | ConvertFrom-Csv
```

**Options**

| Flag | Description |
|------|-------------|
| `-Delimiter` | -Header custom headers |
| `-UseCulture` | — |

---

### `Import-Csv` <sub>ipcsv</sub>

Import CSV file as objects

**Syntax**

```bash
Import-Csv [-Path] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Delimiter` | -Header |
| `-Encoding` | -UseCulture |

---

### `Export-Csv` <sub>epcsv</sub>

Export objects to CSV

**Syntax**

```bash
obj | Export-Csv -Path <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Delimiter` | -NoTypeInformation |
| `-Append` | -Force |
| `-Encoding` | -UseCulture |

---

### `ConvertTo-Xml`

Convert to XML

**Syntax**

```bash
obj | ConvertTo-Xml
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | N |
| `-As` | Document/Fragment/String |
| `-NoTypeInformation` | — |

---

### `ConvertFrom-StringData`

Parse key=value string

**Syntax**

```bash
str | ConvertFrom-StringData
```

**Options**

| Flag | Description |
|------|-------------|
| `-Delimiter` | -StringData |

---

### `Split-String / -split`

Split string

**Syntax**

```bash
'a,b,c' -split ','
```

**Options**

| Flag | Description |
|------|-------------|
| `Regex` | or literal split |
| `N` | max splits (neg = right) |
| `'str'` | -split 're' N opt |

---

### `-join operator`

Join array to string

**Syntax**

```bash
$arr -join ','
```

**Options**

| Flag | Description |
|------|-------------|
| `or` | -join $arr (prefix) |
| `or` | [string]::Join(',',@()) |

---

### `-replace operator`

Regex replace in string

**Syntax**

```bash
'text' -replace 'pat','rep'
```

**Options**

| Flag | Description |
|------|-------------|
| `-ireplace` | case insensitive |
| `-creplace` | case sensitive |
| `Use` | $1 $2 for groups |

---

### `-match / -like / -contains`

String comparison operators

**Syntax**

```bash
'text' -match 'pattern'
```

**Options**

| Flag | Description |
|------|-------------|
| `-match` | regex |
| `-like` | glob (* ?) |
| `'a'` | -in @('a','b') in array |
| `-contains` | array contains value |
| `-eq` | / -ne / -lt / -gt |
| `-cmatch` | case sensitive match |

---

### `Format-List` <sub>fl</sub>

Format as property list

**Syntax**

```bash
obj | Format-List [props]
```

**Options**

| Flag | Description |
|------|-------------|
| `*` | all properties |
| `-GroupBy` | group by prop |
| `-AutoSize` | — |

---

### `Format-Table` <sub>ft</sub>

Format as table

**Syntax**

```bash
obj | Format-Table [props]
```

**Options**

| Flag | Description |
|------|-------------|
| `-AutoSize` | -Wrap |
| `-HideTableHeaders` | — |
| `-GroupBy` | group by prop |
| `-Property` | @{} custom |

---

### `Format-Wide` <sub>fw</sub>

Format as wide list

**Syntax**

```bash
obj | Format-Wide
```

**Options**

| Flag | Description |
|------|-------------|
| `-Column` | N columns |
| `-Property` | prop to show |

---

### `Out-GridView` <sub>ogv</sub>

Display in GUI table

**Syntax**

```bash
obj | Out-GridView
```

**Options**

| Flag | Description |
|------|-------------|
| `-Title` | window title |
| `-PassThru` | return selected |
| `-OutputMode` | Single/Multiple/None |

---

### `Write-Host`

Write to console (no pipeline)

**Syntax**

```bash
Write-Host message
```

**Options**

| Flag | Description |
|------|-------------|
| `-ForegroundColor` | — |
| `-BackgroundColor` | — |
| `-NoNewline` | — |
| `-Separator` | — |

---

### `Write-Output` <sub>echo / write</sub>

Write to pipeline

**Syntax**

```bash
Write-Output value
```

**Options**

| Flag | Description |
|------|-------------|
| `-NoEnumerate` | — |

---

### `Write-Verbose`

Verbose message

**Syntax**

```bash
Write-Verbose message
```

**Options**

| Flag | Description |
|------|-------------|
| `requires` | -Verbose or $VerbosePreference |

---

### `Write-Warning`

Warning message

**Syntax**

```bash
Write-Warning message
```

---

### `Write-Error`

Error message

**Syntax**

```bash
Write-Error message
```

**Options**

| Flag | Description |
|------|-------------|
| `-Category` | -ErrorId |
| `-TargetObject` | -RecommendedAction |

---

### `Write-Information`

Info stream message

**Syntax**

```bash
Write-Information message
```

**Options**

| Flag | Description |
|------|-------------|
| `-Tags` | tag array |

---

### `Write-Debug`

Debug message

**Syntax**

```bash
Write-Debug message
```

**Options**

| Flag | Description |
|------|-------------|
| `requires` | -Debug or $DebugPreference |

---

### `Write-Progress`

Progress bar

**Syntax**

```bash
Write-Progress -Activity name
```

**Options**

| Flag | Description |
|------|-------------|
| `-Status` | text |
| `-PercentComplete` | 0-100 |
| `-CurrentOperation` | detail |
| `-Id` | -ParentId |
| `-Completed` | close bar |

---

### `Clear-Host` <sub>clear / cls</sub>

Clear terminal screen

**Syntax**

```bash
Clear-Host
```

---

### `Read-Host`

Prompt for user input

**Syntax**

```bash
Read-Host [-Prompt] <text>
```

**Options**

| Flag | Description |
|------|-------------|
| `-AsSecureString` | mask input |
| `-MaskInput` | (PS 7.1+) |

---


## Objects & Pipeline

### `Select-Object` <sub>select</sub>

Select properties / slice

**Syntax**

```bash
obj | Select-Object [props]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Property` | prop list |
| `-ExcludeProperty` | — |
| `-ExpandProperty` | unwrap |
| `-First` | N  -Last N |
| `-Skip` | N  -SkipLast N |
| `-Unique` | deduplicate |
| `-Wait` | pipeline wait |
| `-Index` | N items |

---

### `Where-Object` <sub>where / ?</sub>

Filter objects

**Syntax**

```bash
obj | Where-Object {condition}
```

**Options**

| Flag | Description |
|------|-------------|
| `{` | $_.Prop -eq 'val' } |
| `-Property` | -eq Value shorthand |
| `-EQ` | -NE -GT -LT -GE -LE |
| `-Like` | -Match -In -Contains |
| `-Not` | negate condition |

---

### `ForEach-Object` <sub>foreach / %</sub>

Process each object

**Syntax**

```bash
obj | ForEach-Object {block}
```

**Options**

| Flag | Description |
|------|-------------|
| `-Begin` | init block |
| `-Process` | per-item block |
| `-End` | cleanup block |
| `-Parallel` | PS7+ parallel |
| `-ThrottleLimit` | PS7+ |
| `-MemberName` | method/property |

---

### `Sort-Object` <sub>sort</sub>

Sort objects

**Syntax**

```bash
obj | Sort-Object [prop]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Descending` | — |
| `-Unique` | remove dups |
| `-Property` | @{} expr |
| `-CaseSensitive` | — |
| `-Stable` | preserve order |
| `-Top` | N  -Bottom N |

---

### `Group-Object` <sub>group</sub>

Group objects by property

**Syntax**

```bash
obj | Group-Object [prop]
```

**Options**

| Flag | Description |
|------|-------------|
| `-AsHashTable` | — |
| `-AsString` | — |
| `-CaseSensitive` | — |
| `-NoElement` | no members |

---

### `Measure-Object` <sub>measure</sub>

Calculate statistics

**Syntax**

```bash
obj | Measure-Object [prop]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Sum` | -Average |
| `-Maximum` | -Minimum |
| `-StandardDeviation` | — |
| `-AllStats` | -Line  -Word  -Character |

---

### `Compare-Object` <sub>diff / compare</sub>

Compare two sets

**Syntax**

```bash
Compare-Object <ref> <diff>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Property` | props to compare |
| `-IncludeEqual` | show same |
| `-ExcludeDifferent` | hide diffs |
| `-PassThru` | return originals |
| `-SyncWindow` | for sorted |

---

### `Tee-Object` <sub>tee</sub>

Fork pipeline to file

**Syntax**

```bash
obj | Tee-Object -FilePath <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-FilePath` | write to file |
| `-LiteralPath` | — |
| `-Variable` | write to variable |
| `-Append` | append file |

---

### `Get-Unique` <sub>gu</sub>

Unique items from sorted list

**Syntax**

```bash
obj | Get-Unique
```

**Options**

| Flag | Description |
|------|-------------|
| `-AsString` | compare as string |
| `-OnType` | unique types only |

---

### `Out-File` <sub>of</sub>

Redirect output to file

**Syntax**

```bash
obj | Out-File [-FilePath] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Encoding` | UTF8/ASCII/etc |
| `-Append` | -Force |
| `-NoClobber` | no overwrite |
| `-Width` | line width |
| `-NoNewline` | — |
| `-WhatIf` | -Confirm |

---

### `Out-Null`

Discard output

**Syntax**

```bash
obj | Out-Null
```

---

### `Out-Host` <sub>oh</sub>

Send to console

**Syntax**

```bash
obj | Out-Host
```

**Options**

| Flag | Description |
|------|-------------|
| `-Paging` | pause per screen |

---

### `Out-Printer` <sub>lp</sub>

Send to printer

**Syntax**

```bash
obj | Out-Printer
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | printer name |

---

### `Out-GridView` <sub>ogv</sub>

Interactive grid (GUI)

**Syntax**

```bash
obj | Out-GridView
```

**Options**

| Flag | Description |
|------|-------------|
| `-PassThru` | -Title |
| `-OutputMode` | — |

---

### `New-Object`

Create .NET/COM object

**Syntax**

```bash
New-Object -TypeName <type>
```

**Options**

| Flag | Description |
|------|-------------|
| `-TypeName` | fully qualified |
| `-ArgumentList` | ctor args |
| `-ComObject` | COM ProgID |
| `-Property` | hashtable |

---

### `Add-Member`

Add property/method to object

**Syntax**

```bash
obj | Add-Member -NotePropertyName n -NotePropertyValue v
```

**Options**

| Flag | Description |
|------|-------------|
| `-MemberType` | NoteProperty/ScriptMethod/ScriptProperty/AliasProperty |
| `-Force` | overwrite |
| `-PassThru` | -InputObject |
| `-Name` | -Value |

---

### `Get-Member` <sub>gm</sub>

Inspect object members

**Syntax**

```bash
obj | Get-Member
```

**Options**

| Flag | Description |
|------|-------------|
| `-MemberType` | Property/Method/etc |
| `-Name` | filter name |
| `-Force` | include hidden |
| `-Static` | static members |
| `-InputObject` | — |

---

### `ConvertTo-Html`

Convert to HTML table

**Syntax**

```bash
obj | ConvertTo-Html
```

**Options**

| Flag | Description |
|------|-------------|
| `-Property` | -Head CSS/JS |
| `-Title` | page title |
| `-Body` | additional HTML |
| `-As` | Table/List |
| `-PreContent` | -PostContent |
| `-Fragment` | no HTML wrapper |

---

### `[pscustomobject]`

Create custom object

**Syntax**

```bash
[pscustomobject]@{Name='x';Val=1}
```

**Options**

| Flag | Description |
|------|-------------|
| `or` | New-Object PSObject -Property @{} |

---

### `$_  /  $PSItem`

Current pipeline object

**Syntax**

```bash
... | ForEach-Object { $_ }
```

---


## Variables & Data

### `Get-Variable` <sub>gv</sub>

Get variable(s)

**Syntax**

```bash
Get-Variable [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | wildcard ok |
| `-Scope` | current/global/local/N |
| `-ValueOnly` | return value |
| `-Include` | -Exclude |

---

### `Set-Variable` <sub>sv / set</sub>

Set variable value

**Syntax**

```bash
Set-Variable -Name n -Value v
```

**Options**

| Flag | Description |
|------|-------------|
| `-Scope` | -Option ReadOnly/Constant/Private/AllScope |
| `-Description` | -Force |
| `-PassThru` | -Confirm |

---

### `New-Variable` <sub>nv</sub>

Create new variable

**Syntax**

```bash
New-Variable -Name n -Value v
```

**Options**

| Flag | Description |
|------|-------------|
| `-Scope` | -Option  -Description |
| `-Force` | -Visibility Public/Private |
| `-PassThru` | -Confirm |

---

### `Remove-Variable` <sub>rv / del</sub>

Delete variable

**Syntax**

```bash
Remove-Variable -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Scope` | -Force |
| `-Include` | -Exclude |
| `-Confirm` | — |

---

### `Clear-Variable` <sub>clv</sub>

Clear variable value (keep var)

**Syntax**

```bash
Clear-Variable -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Scope` | -Force |
| `-Include` | -Exclude |

---

### `$null`

Null value

**Syntax**

```bash
$var = $null
```

---

### `$true / $false`

Boolean literals

**Syntax**

```bash
if ($true) { }
```

---

### `$env:VAR`

Access environment variable

**Syntax**

```bash
$env:PATH  $env:USERNAME
```

---

### `[int] [string] [bool]`

Type cast / accelerators

**Syntax**

```bash
[int]'42'   [string]123
```

**Options**

| Flag | Description |
|------|-------------|
| `[datetime]` | [xml]  [regex] |
| `[hashtable]` | [array]  [psobject] |
| `[System.IO.FileInfo]` | etc |

---

### `@() array operator`

Create array

**Syntax**

```bash
$a = @(1, 2, 3)
```

**Options**

| Flag | Description |
|------|-------------|
| `$a` | += item  add element |
| `$a.Count` | length |
| `$a[0]` | index |
| `$a[-1]` | last |
| `$a[1..3]` | range slice |

---

### `@{} hashtable`

Create hashtable

**Syntax**

```bash
$h = @{Key='val'; N=1}
```

**Options**

| Flag | Description |
|------|-------------|
| `$h.Key` | or  $h['Key'] |
| `$h.Add(k,v)` | $h.Remove(k) |
| `$h.Keys` | $h.Values |
| `$h.ContainsKey(k)` | — |
| `[ordered]@{}` | ordered dict |

---

### `$args`

Positional script arguments

**Syntax**

```bash
function f { $args[0] }
```

---

### `$PSBoundParameters`

Named bound params

**Syntax**

```bash
param($a,$b); $PSBoundParameters
```

---

### `$MyInvocation`

Current invocation info

**Syntax**

```bash
$MyInvocation.MyCommand
```

**Options**

| Flag | Description |
|------|-------------|
| `.ScriptName` | .Line  .BoundParameters |

---

### `$?`

Last command success

**Syntax**

```bash
if ($?) { 'ok' }
```

---

### `$LASTEXITCODE`

Last native exit code

**Syntax**

```bash
cmd.exe; $LASTEXITCODE
```

---

### `$Error`

Error history array

**Syntax**

```bash
$Error[0]
```

**Options**

| Flag | Description |
|------|-------------|
| `$Error.Clear()` | — |

---

### `$PID`

Current process ID

**Syntax**

```bash
$PID
```

---

### `$PSVersionTable`

PowerShell version info

**Syntax**

```bash
$PSVersionTable
```

**Options**

| Flag | Description |
|------|-------------|
| `.PSVersion` | .OS  .Platform |

---

### `$PROFILE`

Profile script paths

**Syntax**

```bash
$PROFILE.CurrentUserCurrentHost
```

**Options**

| Flag | Description |
|------|-------------|
| `.AllUsersAllHosts` | — |
| `.CurrentUserAllHosts` | — |

---

### `$HOME / $PWD / $PSHome`

Home, working dir, PS install

**Syntax**

```bash
$HOME  $PWD.Path  $PSHome
```

---


## Processes

### `Get-Process` <sub>ps / gps</sub>

List running processes

**Syntax**

```bash
Get-Process [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | filter name (wildcard) |
| `-Id` | filter by PID |
| `-IncludeUserName` | — |
| `-FileVersionInfo` | — |
| `-Module` | loaded modules |
| `-ComputerName` | remote |

---

### `Start-Process` <sub>start / saps</sub>

Start a new process

**Syntax**

```bash
Start-Process [-FilePath] <exe>
```

**Options**

| Flag | Description |
|------|-------------|
| `-ArgumentList` | args |
| `-WorkingDirectory` | — |
| `-Credential` | run as user |
| `-Verb` | RunAs (elevate) |
| `-WindowStyle` | Hidden/Min/Max/Normal |
| `-Wait` | block until done |
| `-PassThru` | return process obj |
| `-NoNewWindow` | — |
| `-RedirectStandardOutput/Input/Error` | — |
| `-LoadUserProfile` | — |

---

### `Stop-Process` <sub>kill / spps</sub>

Stop process(es)

**Syntax**

```bash
Stop-Process [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Id` | by PID |
| `-Force` | forceful kill |
| `-Confirm` | -WhatIf |
| `-PassThru` | return obj |

---

### `Wait-Process`

Wait for process to exit

**Syntax**

```bash
Wait-Process [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Id` | by PID |
| `-Timeout` | seconds |
| `-PassThru` | — |

---

### `Get-Job` <sub>gjb</sub>

List background jobs

**Syntax**

```bash
Get-Job
```

**Options**

| Flag | Description |
|------|-------------|
| `-Id` | -Name  -State |
| `-IncludeChildJob` | — |
| `-ChildJobState` | — |
| `-HasMoreData` | — |

---

### `Start-Job` <sub>sajb</sub>

Start background job

**Syntax**

```bash
Start-Job -ScriptBlock { }
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -ArgumentList |
| `-InitializationScript` | — |
| `-Credential` | -PSVersion |
| `-WorkingDirectory` | (PS7+) |

---

### `Stop-Job` <sub>spjb</sub>

Stop background job

**Syntax**

```bash
Stop-Job [-Id] N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -State  -Force |
| `-Confirm` | -WhatIf |
| `-PassThru` | — |

---

### `Receive-Job` <sub>rcjb</sub>

Get job output

**Syntax**

```bash
Receive-Job [-Id] N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Keep` | don't flush |
| `-Wait` | block until done |
| `-AutoRemoveJob` | -Force |
| `-WriteEvents` | -WriteJobInResults |

---

### `Remove-Job` <sub>rjb</sub>

Delete background job

**Syntax**

```bash
Remove-Job [-Id] N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -Confirm  -WhatIf |

---

### `Wait-Job` <sub>wjb</sub>

Wait for job to finish

**Syntax**

```bash
Wait-Job [-Id] N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Timeout` | seconds |
| `-Any` | first job |
| `-Force` | — |

---

### `Start-ThreadJob`

Lightweight thread-based job

**Syntax**

```bash
Start-ThreadJob -ScriptBlock { }
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -ArgumentList |
| `-InitializationScript` | — |
| `-StreamingHost` | — |
| `-ThrottleLimit` | — |
| `-InputObject` | — |

---

### `ForEach-Object -Parallel`

Parallel pipeline processing

**Syntax**

```bash
1..10 | ForEach-Object -Parallel { }
```

**Options**

| Flag | Description |
|------|-------------|
| `-ThrottleLimit` | N (default 5) |
| `-TimeoutSeconds` | — |
| `-AsJob` | — |

---

### `Invoke-Command` <sub>icm</sub>

Run command remotely/locally

**Syntax**

```bash
Invoke-Command -ScriptBlock { } -ComputerName host
```

**Options**

| Flag | Description |
|------|-------------|
| `-ComputerName` | -Session |
| `-Credential` | -AsJob |
| `-ArgumentList` | -HideComputerName |
| `-ThrottleLimit` | — |
| `-FilePath` | -InDisconnectedSession |

---


## Services

### `Get-Service` <sub>gsv</sub>

List services

**Syntax**

```bash
Get-Service [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | wildcard ok |
| `-DisplayName` | — |
| `-DependentServices` | — |
| `-RequiredServices` | — |
| `-ComputerName` | (PS5) |

---

### `Start-Service` <sub>sasv</sub>

Start a service

**Syntax**

```bash
Start-Service [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-DisplayName` | -InputObject |
| `-PassThru` | -Confirm  -WhatIf |

---

### `Stop-Service` <sub>spsv</sub>

Stop a service

**Syntax**

```bash
Stop-Service [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -NoWait |
| `-PassThru` | -Confirm  -WhatIf |

---

### `Restart-Service`

Restart a service

**Syntax**

```bash
Restart-Service [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -PassThru |
| `-Confirm` | -WhatIf |

---

### `Suspend-Service`

Pause a service

**Syntax**

```bash
Suspend-Service [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-PassThru` | -Confirm  -WhatIf |

---

### `Resume-Service`

Resume a paused service

**Syntax**

```bash
Resume-Service [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-PassThru` | -Confirm  -WhatIf |

---

### `Set-Service`

Modify service config

**Syntax**

```bash
Set-Service [-Name] <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Status` | Running/Stopped/Paused |
| `-StartupType` | Automatic/Disabled/Manual/AutomaticDelayedStart |
| `-DisplayName` | -Description |
| `-Credential` | -PassThru |

---

### `New-Service`

Create a Windows service

**Syntax**

```bash
New-Service -Name n -BinaryPathName path
```

**Options**

| Flag | Description |
|------|-------------|
| `-DisplayName` | -Description |
| `-StartupType` | -Credential |
| `-DependsOn` | -PassThru |

---

### `Remove-Service`

Delete a service (PS6+)

**Syntax**

```bash
Remove-Service -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Confirm` | -WhatIf |

---


## Network

### `Test-Connection`

Ping / connectivity test

**Syntax**

```bash
Test-Connection -TargetName host
```

**Options**

| Flag | Description |
|------|-------------|
| `-Count` | N pings |
| `-Delay` | seconds between |
| `-BufferSize` | bytes |
| `-DontFragment` | -IPv4  -IPv6 |
| `-Quiet` | return bool |
| `-ResolveDestination` | — |
| `-Source` | source computer |
| `-TimeoutSeconds` | — |
| `-MTUSizeDetect` | -Traceroute |

---

### `Test-NetConnection`

TCP port / route test

**Syntax**

```bash
Test-NetConnection host
```

**Options**

| Flag | Description |
|------|-------------|
| `-Port` | TCP port |
| `-InformationLevel` | Quiet/Detailed |
| `-TraceRoute` | -DiagnoseRouting |
| `-ConstrainInterface` | — |
| `-CommonTCPPort` | HTTP/SMB/RDP/WINRM |

---

### `Invoke-WebRequest` <sub>iwr / wget / curl</sub>

HTTP request

**Syntax**

```bash
Invoke-WebRequest -Uri <url>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Method` | GET/POST/PUT/etc |
| `-Body` | -Headers @{} |
| `-ContentType` | -OutFile |
| `-Credential` | -UseBasicParsing |
| `-SessionVariable` | -WebSession |
| `-Authentication` | Bearer/Basic |
| `-Token` | -SkipCertificateCheck (PS7+) |
| `-FollowRelLink` | -MaximumFollowRelLink |
| `-Form` | -TimeoutSec |

---

### `Invoke-RestMethod` <sub>irm</sub>

REST API call

**Syntax**

```bash
Invoke-RestMethod -Uri <url>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Method` | -Body  -Headers @{} |
| `-ContentType` | application/json |
| `-Authentication` | -Token |
| `-Credential` | -OutFile |
| `-SkipCertificateCheck` | (PS7+) |
| `-SessionVariable` | -WebSession |
| `-FollowRelLink` | -TimeoutSec |

---

### `Get-NetAdapter`

Network adapters

**Syntax**

```bash
Get-NetAdapter [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -InterfaceDescription |
| `-Physical` | -IncludeHidden |
| `-SkipProfiles` | — |

---

### `Get-NetIPAddress`

IP addresses

**Syntax**

```bash
Get-NetIPAddress
```

**Options**

| Flag | Description |
|------|-------------|
| `-IPAddress` | -InterfaceAlias |
| `-InterfaceIndex` | — |
| `-AddressFamily` | IPv4/IPv6 |
| `-PrefixOrigin` | -SuffixOrigin |

---

### `Get-NetIPConfiguration` <sub>gip</sub>

IP config summary

**Syntax**

```bash
Get-NetIPConfiguration
```

**Options**

| Flag | Description |
|------|-------------|
| `-InterfaceAlias` | -InterfaceIndex |
| `-Detailed` | -AllCompartments |

---

### `Get-NetRoute`

Routing table

**Syntax**

```bash
Get-NetRoute
```

**Options**

| Flag | Description |
|------|-------------|
| `-DestinationPrefix` | -InterfaceAlias |
| `-AddressFamily` | — |
| `-PolicyStore` | — |

---

### `Get-NetTCPConnection`

TCP connections

**Syntax**

```bash
Get-NetTCPConnection
```

**Options**

| Flag | Description |
|------|-------------|
| `-LocalPort` | -RemotePort |
| `-LocalAddress` | -RemoteAddress |
| `-State` | Established/Listen/TimeWait/etc |
| `-OwningProcess` | PID |

---

### `Get-NetUDPEndpoint`

UDP endpoints

**Syntax**

```bash
Get-NetUDPEndpoint
```

**Options**

| Flag | Description |
|------|-------------|
| `-LocalPort` | -LocalAddress |
| `-OwningProcess` | — |

---

### `Resolve-DnsName`

DNS lookup

**Syntax**

```bash
Resolve-DnsName <name>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Type` | A/AAAA/MX/NS/TXT/CNAME/SOA/PTR |
| `-Server` | DNS server |
| `-NoHostsFile` | -DnsOnly |
| `-NetbiosOnly` | -CacheOnly |
| `-DnssecOk` | -DnssecCd |

---

### `Set-NetIPAddress`

Configure IP address

**Syntax**

```bash
Set-NetIPAddress -InterfaceAlias eth0
```

**Options**

| Flag | Description |
|------|-------------|
| `-IPAddress` | -PrefixLength |
| `-DefaultGateway` | — |

---

### `New-NetFirewallRule`

Create firewall rule

**Syntax**

```bash
New-NetFirewallRule -DisplayName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Direction` | Inbound/Outbound |
| `-Protocol` | TCP/UDP/Any |
| `-LocalPort` | -RemotePort |
| `-Action` | Allow/Block/DontConfigure |
| `-Profile` | Domain/Private/Public/Any |
| `-Enabled` | True/False |

---

### `Get-NetFirewallRule`

List firewall rules

**Syntax**

```bash
Get-NetFirewallRule
```

**Options**

| Flag | Description |
|------|-------------|
| `-DisplayName` | -Name |
| `-Direction` | -Enabled |
| `-Action` | -Profile |

---

### `Enable/Disable-NetFirewallRule`

Toggle firewall rule

**Syntax**

```bash
Enable-NetFirewallRule -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-DisplayName` | -Group |
| `-Direction` | -Profile |

---

### `Get-NetNeighbor`

ARP / NDP table

**Syntax**

```bash
Get-NetNeighbor
```

**Options**

| Flag | Description |
|------|-------------|
| `-IPAddress` | -InterfaceAlias |
| `-AddressFamily` | -State Reachable/Stale/etc |

---


## System Info

### `Get-ComputerInfo`

Comprehensive system info

**Syntax**

```bash
Get-ComputerInfo
```

**Options**

| Flag | Description |
|------|-------------|
| `-Property` | filter properties |

---

### `Get-Host`

PowerShell host info

**Syntax**

```bash
Get-Host
```

---

### `$PSVersionTable`

PowerShell version details

**Syntax**

```bash
$PSVersionTable
```

---

### `Get-WmiObject` <sub>gwmi</sub>

WMI query (legacy PS5)

**Syntax**

```bash
Get-WmiObject -Class Win32_X
```

**Options**

| Flag | Description |
|------|-------------|
| `-Class` | Win32_ComputerSystem/Win32_OS/etc |
| `-Property` | -Filter  -Query |
| `-ComputerName` | -Namespace |

---

### `Get-CimInstance` <sub>gcim</sub>

CIM query (modern)

**Syntax**

```bash
Get-CimInstance -ClassName Win32_X
```

**Options**

| Flag | Description |
|------|-------------|
| `-ClassName` | -Filter |
| `-Property` | -Query |
| `-ComputerName` | -CimSession |
| `-Namespace` | — |

---

### `Get-HotFix`

Installed Windows updates

**Syntax**

```bash
Get-HotFix
```

**Options**

| Flag | Description |
|------|-------------|
| `-Id` | -Description |
| `-ComputerName` | -Credential |

---

### `Get-Disk`

Physical disks

**Syntax**

```bash
Get-Disk
```

**Options**

| Flag | Description |
|------|-------------|
| `-Number` | -FriendlyName |
| `-SerialNumber` | -UniqueId |

---

### `Get-Volume`

Disk volumes

**Syntax**

```bash
Get-Volume
```

**Options**

| Flag | Description |
|------|-------------|
| `-DriveLetter` | -FileSystemLabel |
| `-ObjectId` | -Path |

---

### `Get-Partition`

Disk partitions

**Syntax**

```bash
Get-Partition
```

**Options**

| Flag | Description |
|------|-------------|
| `-DiskNumber` | -PartitionNumber |
| `-DriveLetter` | -DiskId |

---

### `Get-PSDrive` <sub>gdr</sub>

List PS provider drives

**Syntax**

```bash
Get-PSDrive
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -PSProvider |
| `-Scope` | -LiteralName |

---

### `Get-PSProvider`

List PS providers

**Syntax**

```bash
Get-PSProvider
```

**Options**

| Flag | Description |
|------|-------------|
| `-PSProvider` | name |

---

### `Get-EventLog`

Read event log (PS5)

**Syntax**

```bash
Get-EventLog -LogName Application
```

**Options**

| Flag | Description |
|------|-------------|
| `-LogName` | System/Application/Security/etc |
| `-Newest` | N |
| `-EntryType` | Error/Warning/Info |
| `-Source` | -EventId |
| `-Message` | -After  -Before |
| `-UserName` | -ComputerName |

---

### `Get-WinEvent`

Read Windows event logs (modern)

**Syntax**

```bash
Get-WinEvent -LogName Application
```

**Options**

| Flag | Description |
|------|-------------|
| `-LogName` | -ListLog |
| `-FilterHashtable` | @{LogName=...;Id=...;Level=...;StartTime=...} |
| `-FilterXPath` | -MaxEvents N |
| `-ComputerName` | -Credential |
| `-Oldest` | -ProviderName |

---

### `Get-Counter`

Performance counters

**Syntax**

```bash
Get-Counter '\Processor(*)% Processor Time'
```

**Options**

| Flag | Description |
|------|-------------|
| `-SampleInterval` | seconds |
| `-MaxSamples` | N |
| `-Continuous` | -ComputerName |
| `-ListSet` | -Counter |

---

### `Measure-Command`

Time a command

**Syntax**

```bash
Measure-Command { cmd }
```

---

### `Get-Uptime`

System uptime (PS6+)

**Syntax**

```bash
Get-Uptime
```

**Options**

| Flag | Description |
|------|-------------|
| `-Since` | return start datetime |

---

### `Stop-Computer`

Shut down computer

**Syntax**

```bash
Stop-Computer
```

**Options**

| Flag | Description |
|------|-------------|
| `-ComputerName` | -Credential |
| `-Force` | -Confirm  -WhatIf |

---

### `Restart-Computer`

Restart computer

**Syntax**

```bash
Restart-Computer
```

**Options**

| Flag | Description |
|------|-------------|
| `-ComputerName` | -Force |
| `-Wait` | -Timeout  -For |
| `-Delay` | -Credential |
| `-Confirm` | -WhatIf |

---


## Registry

### `Get-Item HKLM:\...`

Read registry key

**Syntax**

```bash
Get-Item 'HKLM:\Software\...'
```

**Options**

| Flag | Description |
|------|-------------|
| `HKLM:` | HKCU:  HKCR:  HKU:  HKCC: |

---

### `Get-ItemProperty` <sub>gp</sub>

Read registry values

**Syntax**

```bash
Get-ItemProperty -Path 'HKLM:\...' -Name val
```

**Options**

| Flag | Description |
|------|-------------|
| `-Path` | -LiteralPath |
| `-Name` | specific value |
| `-Filter` | -Include  -Exclude |

---

### `Set-ItemProperty` <sub>sp</sub>

Set registry value

**Syntax**

```bash
Set-ItemProperty -Path 'HKLM:\...' -Name val -Value data
```

**Options**

| Flag | Description |
|------|-------------|
| `-Type` | String/DWord/QWord/Binary/MultiString/ExpandString |
| `-Force` | -PassThru |
| `-Confirm` | -WhatIf |

---

### `New-ItemProperty`

Create new registry value

**Syntax**

```bash
New-ItemProperty -Path 'HKLM:\...' -Name n -Value v -PropertyType type
```

**Options**

| Flag | Description |
|------|-------------|
| `-PropertyType` | String/DWord/QWord/Binary/MultiString/ExpandString |
| `-Force` | -PassThru |

---

### `Remove-ItemProperty` <sub>rp</sub>

Delete registry value

**Syntax**

```bash
Remove-ItemProperty -Path 'HKLM:\...' -Name val
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -Confirm  -WhatIf |

---

### `New-Item -Path HKLM:\...`

Create registry key

**Syntax**

```bash
New-Item -Path 'HKLM:\...' -Name KeyName
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -Value default val |

---

### `Remove-Item HKLM:\...`

Delete registry key

**Syntax**

```bash
Remove-Item -Path 'HKLM:\...'
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | -Force |
| `-Confirm` | -WhatIf |

---

### `Test-Path HKLM:\...`

Test if registry key exists

**Syntax**

```bash
Test-Path 'HKLM:\...'
```

**Options**

| Flag | Description |
|------|-------------|
| `-PathType` | Container/Leaf |

---

### `Copy-Item HKLM:\...`

Copy registry key

**Syntax**

```bash
Copy-Item 'HKLM:\...' 'HKCU:\...'
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | -Force |

---

### `Get-ChildItem HKLM:\...`

List sub-keys

**Syntax**

```bash
Get-ChildItem 'HKLM:\Software'
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | -Depth N |

---


## Security

### `Get-Credential`

Prompt for credentials

**Syntax**

```bash
$cred = Get-Credential
```

**Options**

| Flag | Description |
|------|-------------|
| `-UserName` | pre-fill name |
| `-Message` | custom prompt |
| `-Title` | (PS7.1+) |

---

### `ConvertTo-SecureString`

Create secure string

**Syntax**

```bash
ConvertTo-SecureString 'pass' -AsPlainText -Force
```

**Options**

| Flag | Description |
|------|-------------|
| `-AsPlainText` | plain text input |
| `-Force` | required with -AsPlainText |
| `-Key` | -SecureKey encrypt |

---

### `ConvertFrom-SecureString`

Export secure string

**Syntax**

```bash
$ss | ConvertFrom-SecureString
```

**Options**

| Flag | Description |
|------|-------------|
| `-Key` | -SecureKey |
| `-AsPlainText` | (PS7+) |

---

### `New-SelfSignedCertificate`

Create self-signed cert

**Syntax**

```bash
New-SelfSignedCertificate -DnsName name
```

**Options**

| Flag | Description |
|------|-------------|
| `-CertStoreLocation` | Cert:\... |
| `-DnsName` | -Subject |
| `-KeyUsage` | -KeyAlgorithm |
| `-NotAfter` | -FriendlyName |
| `-TextExtension` | -Type |

---

### `Get-Certificate`

Get certificates

**Syntax**

```bash
Get-Certificate
```

**Options**

| Flag | Description |
|------|-------------|
| `-Template` | -Url  -Credential |
| `-SubjectName` | -DnsName |
| `-CertStoreLocation` | — |

---

### `Get-PfxCertificate`

Get PFX cert info

**Syntax**

```bash
Get-PfxCertificate -FilePath file.pfx
```

**Options**

| Flag | Description |
|------|-------------|
| `-Password` | -NoPromptForPassword |

---

### `Get-ChildItem Cert:\`

Browse certificate store

**Syntax**

```bash
Get-ChildItem Cert:\CurrentUser\My
```

**Options**

| Flag | Description |
|------|-------------|
| `-Recurse` | -CodeSigningCert |
| `-DnsName` | -EKU  -ExpiringInDays |

---

### `Set-ExecutionPolicy`

Set script execution policy

**Syntax**

```bash
Set-ExecutionPolicy Unrestricted
```

**Options**

| Flag | Description |
|------|-------------|
| `-ExecutionPolicy` | Restricted/AllSigned/RemoteSigned/Unrestricted/Bypass/Undefined |
| `-Scope` | MachinePolicy/UserPolicy/Process/CurrentUser/LocalMachine |
| `-Force` | -Confirm |

---

### `Get-ExecutionPolicy`

Get execution policy

**Syntax**

```bash
Get-ExecutionPolicy
```

**Options**

| Flag | Description |
|------|-------------|
| `-List` | show all scopes |
| `-Scope` | — |

---

### `Unblock-File`

Unblock downloaded file

**Syntax**

```bash
Unblock-File [-Path] <file>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Confirm` | -WhatIf |

---

### `Get-Acl`

Get file/reg ACL

**Syntax**

```bash
Get-Acl -Path <path>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Audit` | include SACL |

---

### `Set-Acl`

Set file/reg ACL

**Syntax**

```bash
Set-Acl -Path <path> -AclObject <acl>
```

---


## Users & Groups

### `Get-LocalUser`

List local users

**Syntax**

```bash
Get-LocalUser [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | wildcard ok |
| `-SID` | filter by SID |

---

### `New-LocalUser`

Create local user

**Syntax**

```bash
New-LocalUser -Name n -Password (ConvertTo-SecureString ...)
```

**Options**

| Flag | Description |
|------|-------------|
| `-FullName` | -Description |
| `-AccountExpires` | -Disabled |
| `-PasswordNeverExpires` | — |
| `-UserMayNotChangePassword` | — |
| `-NoPassword` | — |

---

### `Set-LocalUser`

Modify local user

**Syntax**

```bash
Set-LocalUser -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Password` | -FullName |
| `-Description` | -AccountExpires |
| `-PasswordNeverExpires` | — |
| `-UserMayNotChangePassword` | -Confirm |

---

### `Remove-LocalUser`

Delete local user

**Syntax**

```bash
Remove-LocalUser -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-SID` | -Confirm  -WhatIf |

---

### `Enable-LocalUser`

Enable local user

**Syntax**

```bash
Enable-LocalUser -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-SID` | -Confirm  -WhatIf |

---

### `Disable-LocalUser`

Disable local user

**Syntax**

```bash
Disable-LocalUser -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-SID` | -Confirm  -WhatIf |

---

### `Get-LocalGroup`

List local groups

**Syntax**

```bash
Get-LocalGroup [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -SID |

---

### `New-LocalGroup`

Create local group

**Syntax**

```bash
New-LocalGroup -Name n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Description` | — |

---

### `Add-LocalGroupMember`

Add user to group

**Syntax**

```bash
Add-LocalGroupMember -Group grp -Member user
```

**Options**

| Flag | Description |
|------|-------------|
| `-Confirm` | -WhatIf |

---

### `Remove-LocalGroupMember`

Remove user from group

**Syntax**

```bash
Remove-LocalGroupMember -Group grp -Member user
```

**Options**

| Flag | Description |
|------|-------------|
| `-Confirm` | -WhatIf |

---

### `Get-LocalGroupMember`

List group members

**Syntax**

```bash
Get-LocalGroupMember -Group grp
```

**Options**

| Flag | Description |
|------|-------------|
| `-Member` | -SID |

---

### `whoami`

Current user (native)

**Syntax**

```bash
whoami
```

**Options**

| Flag | Description |
|------|-------------|
| `/user` | /groups  /priv  /all |

---

### `[System.Security.Principal.WindowsIdentity]::GetCurrent()`

Current Windows identity

**Syntax**

```bash
[Security.Principal.WindowsIdentity]::GetCurrent()
```

---


## Modules & Packages

### `Get-Module` <sub>gmo</sub>

List loaded/available modules

**Syntax**

```bash
Get-Module [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-ListAvailable` | all on PSModulePath |
| `-All` | include nested |
| `-Name` | -FullyQualifiedName |
| `-Refresh` | -PSEdition |
| `-SkipEditionCheck` | — |

---

### `Import-Module` <sub>ipmo</sub>

Load a module

**Syntax**

```bash
Import-Module [-Name] <mod>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | reimport |
| `-NoClobber` | no overwrite |
| `-Global` | -Prefix |
| `-Verbose` | -PassThru |
| `-SkipEditionCheck` | -UseWindowsPowerShell |

---

### `Remove-Module` <sub>rmo</sub>

Unload a module

**Syntax**

```bash
Remove-Module [-Name] <mod>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -Verbose |
| `-Confirm` | -WhatIf |

---

### `Find-Module`

Search PSGallery

**Syntax**

```bash
Find-Module [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -Repository |
| `-RequiredVersion` | -MinimumVersion  -MaximumVersion |
| `-AllVersions` | -Tag  -Filter |
| `-Command` | -DscResource |
| `-Includes` | — |

---

### `Install-Module`

Install from PSGallery

**Syntax**

```bash
Install-Module [-Name] <mod>
```

**Options**

| Flag | Description |
|------|-------------|
| `-Repository` | -RequiredVersion |
| `-MinimumVersion` | -MaximumVersion |
| `-Scope` | CurrentUser/AllUsers |
| `-Force` | -AllowClobber |
| `-SkipPublisherCheck` | -AcceptLicense |
| `-AllowPrerelease` | — |

---

### `Update-Module`

Update installed module

**Syntax**

```bash
Update-Module [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-RequiredVersion` | -MaximumVersion |
| `-Force` | -AcceptLicense |
| `-AllowPrerelease` | -Confirm |

---

### `Uninstall-Module`

Remove installed module

**Syntax**

```bash
Uninstall-Module [-Name] <mod>
```

**Options**

| Flag | Description |
|------|-------------|
| `-RequiredVersion` | -MinimumVersion  -MaximumVersion |
| `-AllVersions` | -Force  -Confirm |

---

### `Publish-Module`

Publish to PSGallery

**Syntax**

```bash
Publish-Module -Name mod -NuGetApiKey key
```

**Options**

| Flag | Description |
|------|-------------|
| `-Path` | -Repository |
| `-RequiredVersion` | -ReleaseNotes |
| `-Tags` | -ProjectUri |

---

### `Get-Command` <sub>gcm</sub>

Find commands

**Syntax**

```bash
Get-Command [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | wildcard ok |
| `-CommandType` | Cmdlet/Function/Alias/Script/Application/All |
| `-Module` | filter by module |
| `-Verb` | -Noun |
| `-ParameterName` | -ParameterType |
| `-TotalCount` | -Syntax |
| `-ShowCommandInfo` | — |

---

### `Get-Alias` <sub>gal</sub>

List aliases

**Syntax**

```bash
Get-Alias [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -Definition  -Scope |

---

### `Set-Alias` <sub>sal</sub>

Create alias

**Syntax**

```bash
Set-Alias -Name n -Value cmd
```

**Options**

| Flag | Description |
|------|-------------|
| `-Option` | ReadOnly/Constant/Private/AllScope |
| `-Scope` | -Force  -PassThru |

---

### `New-Alias` <sub>nal</sub>

Create new alias

**Syntax**

```bash
New-Alias -Name n -Value cmd
```

**Options**

| Flag | Description |
|------|-------------|
| `-Option` | -Scope  -Force |
| `-Description` | -PassThru |

---

### `Export-Alias` <sub>epal</sub>

Export aliases to file

**Syntax**

```bash
Export-Alias -Path file
```

**Options**

| Flag | Description |
|------|-------------|
| `-As` | Csv/Script |
| `-Append` | -Force |
| `-NoClobber` | -PassThru |

---

### `Import-Alias` <sub>ipal</sub>

Import aliases from file

**Syntax**

```bash
Import-Alias -Path file
```

**Options**

| Flag | Description |
|------|-------------|
| `-Scope` | -Force  -PassThru |

---

### `winget`

Windows Package Manager

**Syntax**

```bash
winget [cmd] [pkg]
```

**Options**

| Flag | Description |
|------|-------------|
| `install` | uninstall  upgrade |
| `search` | show  list |
| `import` | export  source |
| `settings` | features |

---

### `choco`

Chocolatey package manager

**Syntax**

```bash
choco [cmd] [pkg]
```

**Options**

| Flag | Description |
|------|-------------|
| `install` | uninstall  upgrade |
| `search` | list  info |
| `outdated` | pin |
| `source` | feature |

---


## Remoting

### `Enable-PSRemoting`

Enable PS remoting

**Syntax**

```bash
Enable-PSRemoting
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -SkipNetworkProfileCheck |
| `-Confirm` | -WhatIf |

---

### `Disable-PSRemoting`

Disable PS remoting

**Syntax**

```bash
Disable-PSRemoting
```

**Options**

| Flag | Description |
|------|-------------|
| `-Force` | -Confirm  -WhatIf |

---

### `Enter-PSSession` <sub>etsn</sub>

Interactive remote session

**Syntax**

```bash
Enter-PSSession -ComputerName host
```

**Options**

| Flag | Description |
|------|-------------|
| `-ComputerName` | -Session |
| `-Credential` | -Port |
| `-UseSSL` | -Authentication |
| `-ConfigurationName` | -VMName  -ContainerId |

---

### `Exit-PSSession` <sub>exsn</sub>

Exit remote session

**Syntax**

```bash
Exit-PSSession
```

---

### `New-PSSession` <sub>nsn</sub>

Create persistent session

**Syntax**

```bash
New-PSSession -ComputerName host
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -Credential |
| `-Port` | -UseSSL |
| `-Authentication` | -ConfigurationName |
| `-SessionOption` | -VMName  -ContainerId |

---

### `Get-PSSession` <sub>gsn</sub>

List PS sessions

**Syntax**

```bash
Get-PSSession
```

**Options**

| Flag | Description |
|------|-------------|
| `-ComputerName` | -Id  -Name |
| `-State` | -InstanceId |
| `-ContainerId` | -VMName |

---

### `Remove-PSSession` <sub>rsn</sub>

Close and remove session

**Syntax**

```bash
Remove-PSSession [-Id] N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -Session  -Confirm |

---

### `Invoke-Command` <sub>icm</sub>

Run command on remote hosts

**Syntax**

```bash
Invoke-Command -ScriptBlock {} -ComputerName host
```

**Options**

| Flag | Description |
|------|-------------|
| `-ComputerName` | -Session |
| `-Credential` | -AsJob |
| `-FilePath` | -ArgumentList |
| `-ThrottleLimit` | -HideComputerName |
| `-InDisconnectedSession` | -ConfigurationName |

---

### `New-PSSessionOption`

Configure session options

**Syntax**

```bash
$opt = New-PSSessionOption
```

**Options**

| Flag | Description |
|------|-------------|
| `-IdleTimeout` | -OpenTimeout |
| `-OperationTimeout` | -MaximumReceivedDataSizePerCommand |
| `-SkipCACheck` | -SkipCNCheck |
| `-SkipRevocationCheck` | — |

---

### `Connect-PSSession` <sub>cnsn</sub>

Reconnect to disconnected session

**Syntax**

```bash
Connect-PSSession -Id N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -ComputerName |
| `-Session` | -Credential |

---

### `Disconnect-PSSession` <sub>dnsn</sub>

Disconnect session (keep running)

**Syntax**

```bash
Disconnect-PSSession -Id N
```

**Options**

| Flag | Description |
|------|-------------|
| `-IdleTimeoutSec` | -OutputBufferingMode |

---


## CIM & WMI

### `Get-CimInstance` <sub>gcim</sub>

Query CIM/WMI

**Syntax**

```bash
Get-CimInstance -ClassName Win32_X
```

**Options**

| Flag | Description |
|------|-------------|
| `-ClassName` | -Namespace |
| `-Filter` | -Query |
| `-Property` | -KeyOnly |
| `-ComputerName` | -CimSession |
| `-Shallow` | -OperationTimeoutSec |

---

### `New-CimSession`

Create CIM session

**Syntax**

```bash
New-CimSession -ComputerName host
```

**Options**

| Flag | Description |
|------|-------------|
| `-Credential` | -Authentication |
| `-SessionOption` | -Port |
| `-OperationTimeoutSec` | — |

---

### `Invoke-CimMethod`

Invoke WMI method

**Syntax**

```bash
Invoke-CimMethod -ClassName class -MethodName method
```

**Options**

| Flag | Description |
|------|-------------|
| `-Arguments` | @{} |
| `-InputObject` | -CimSession |
| `-Namespace` | -QueryDialect |

---

### `Set-CimInstance`

Modify CIM instance

**Syntax**

```bash
Get-CimInstance ... | Set-CimInstance -Property @{}
```

**Options**

| Flag | Description |
|------|-------------|
| `-Property` | @{} hashtable |
| `-Query` | -Namespace |
| `-CimSession` | -PassThru |

---

### `Remove-CimInstance`

Delete CIM instance

**Syntax**

```bash
Get-CimInstance ... | Remove-CimInstance
```

**Options**

| Flag | Description |
|------|-------------|
| `-CimSession` | -Namespace |
| `-Confirm` | -WhatIf |

---

### `Get-CimClass`

Browse CIM classes

**Syntax**

```bash
Get-CimClass -ClassName Win32_*
```

**Options**

| Flag | Description |
|------|-------------|
| `-ClassName` | wildcard |
| `-Namespace` | -OperationTimeoutSec |
| `-MethodName` | -PropertyName |
| `-QualifierName` | — |

---

### `Register-CimIndicationEvent`

Subscribe to WMI event

**Syntax**

```bash
Register-CimIndicationEvent -Query wql -Action {}
```

**Options**

| Flag | Description |
|------|-------------|
| `-Query` | -Namespace |
| `-SourceIdentifier` | -Action {} |
| `-CimSession` | -Forward |

---

### `Win32_ComputerSystem`

System info class

**Syntax**

```bash
Get-CimInstance Win32_ComputerSystem
```

**Options**

| Flag | Description |
|------|-------------|
| `Name` | Manufacturer  Model |
| `TotalPhysicalMemory` | NumberOfProcessors |
| `Domain` | Username  SystemType |

---

### `Win32_OperatingSystem`

OS info class

**Syntax**

```bash
Get-CimInstance Win32_OperatingSystem
```

**Options**

| Flag | Description |
|------|-------------|
| `Caption` | Version  OSArchitecture |
| `LastBootUpTime` | FreePhysicalMemory |
| `BuildNumber` | ServicePackMajorVersion |

---

### `Win32_Process`

Processes via WMI

**Syntax**

```bash
Get-CimInstance Win32_Process
```

**Options**

| Flag | Description |
|------|-------------|
| `Name` | ProcessId  ParentProcessId |
| `CommandLine` | ExecutablePath |
| `WorkingSetSize` | CreationDate |

---

### `Win32_Service`

Services via WMI

**Syntax**

```bash
Get-CimInstance Win32_Service
```

**Options**

| Flag | Description |
|------|-------------|
| `Name` | State  StartMode |

---

### `Win32_LogicalDisk`

Logical disks via WMI

**Syntax**

```bash
Get-CimInstance Win32_LogicalDisk
```

**Options**

| Flag | Description |
|------|-------------|
| `DeviceID` | Size  FreeSpace |
| `FileSystem` | VolumeName |
| `DriveType` | — |

---


## Scheduling

### `Get-ScheduledTask`

List scheduled tasks

**Syntax**

```bash
Get-ScheduledTask [name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-TaskName` | wildcard ok |
| `-TaskPath` | -CimSession |

---

### `Register-ScheduledTask`

Create scheduled task

**Syntax**

```bash
Register-ScheduledTask -TaskName n -Action a -Trigger t
```

**Options**

| Flag | Description |
|------|-------------|
| `-TaskName` | -Action  -Trigger |
| `-Settings` | -Principal |
| `-Description` | -RunLevel Highest |
| `-Force` | -CimSession |

---

### `New-ScheduledTaskAction`

Define task action

**Syntax**

```bash
New-ScheduledTaskAction -Execute exe
```

**Options**

| Flag | Description |
|------|-------------|
| `-Execute` | path |
| `-Argument` | args |
| `-WorkingDirectory` | — |

---

### `New-ScheduledTaskTrigger`

Define task trigger

**Syntax**

```bash
New-ScheduledTaskTrigger -Daily -At 9am
```

**Options**

| Flag | Description |
|------|-------------|
| `-Once` | -Daily  -Weekly  -AtStartup  -AtLogOn |
| `-At` | time  -DaysInterval |
| `-WeeksInterval` | -DaysOfWeek |
| `-User` | -RepetitionInterval |

---

### `Start-ScheduledTask`

Run task immediately

**Syntax**

```bash
Start-ScheduledTask -TaskName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-CimSession` | -Confirm  -WhatIf |

---

### `Stop-ScheduledTask`

Stop running task

**Syntax**

```bash
Stop-ScheduledTask -TaskName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-CimSession` | -Confirm  -WhatIf |

---

### `Disable-ScheduledTask`

Disable a task

**Syntax**

```bash
Disable-ScheduledTask -TaskName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-CimSession` | -Confirm  -WhatIf |

---

### `Enable-ScheduledTask`

Enable a task

**Syntax**

```bash
Enable-ScheduledTask -TaskName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-CimSession` | -Confirm  -WhatIf |

---

### `Unregister-ScheduledTask`

Delete a scheduled task

**Syntax**

```bash
Unregister-ScheduledTask -TaskName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-Confirm` | -WhatIf  -CimSession |

---

### `Get-ScheduledTaskInfo`

Task last run / next run info

**Syntax**

```bash
Get-ScheduledTaskInfo -TaskName n
```

**Options**

| Flag | Description |
|------|-------------|
| `-TaskPath` | -CimSession |

---


## Error Handling

### `try / catch / finally`

Structured error handling

**Syntax**

```bash
try { } catch [type] { } finally { }
```

**Options**

| Flag | Description |
|------|-------------|
| `catch` | { $_.Exception.Message } |
| `catch` | [System.IO.IOException] { } |
| `$_.Exception.GetType().FullName` | — |
| `throw` | re-throw  throw 'msg' new |

---

### `$ErrorActionPreference`

Default error action

**Syntax**

```bash
$ErrorActionPreference = 'Stop'
```

**Options**

| Flag | Description |
|------|-------------|
| `Stop` | Continue  SilentlyContinue |
| `Inquire` | Ignore (PS3+)  Suspend |

---

### `-ErrorAction`

Per-command error action

**Syntax**

```bash
cmd -ErrorAction Stop
```

**Options**

| Flag | Description |
|------|-------------|
| `Stop` | Continue  SilentlyContinue |
| `Inquire` | Ignore  Suspend |
| `-EA` | shorthand |

---

### `-ErrorVariable`

Capture errors to var

**Syntax**

```bash
cmd -ErrorVariable ev
```

**Options**

| Flag | Description |
|------|-------------|
| `-ev` | shorthand |
| `+ev` | append to existing |

---

### `$Error[0]`

Most recent error

**Syntax**

```bash
$Error[0].Exception.Message
```

**Options**

| Flag | Description |
|------|-------------|
| `$Error.Clear()` | clear all |
| `.InvocationInfo` | .ScriptStackTrace |
| `.FullyQualifiedErrorId` | — |
| `.CategoryInfo` | — |

---

### `throw`

Throw terminating error

**Syntax**

```bash
throw 'message'
```

**Options**

| Flag | Description |
|------|-------------|
| `throw` | [System.Exception]::new('msg') |
| `throw` | $errorRecord |

---

### `Write-Error`

Non-terminating error

**Syntax**

```bash
Write-Error 'message'
```

**Options**

| Flag | Description |
|------|-------------|
| `-Category` | -ErrorId |
| `-TargetObject` | -RecommendedAction |
| `-CategoryReason` | -Exception |

---

### `Trap`

Legacy error trap

**Syntax**

```bash
trap [type] { statement }
```

**Options**

| Flag | Description |
|------|-------------|
| `trap` | { continue } |
| `trap` | [System.Exception] { } |

---

### `-WhatIf`

Dry-run simulation

**Syntax**

```bash
Remove-Item file -WhatIf
```

**Options**

| Flag | Description |
|------|-------------|
| `requires` | CmdletBinding |
| `-Confirm` | prompt each action |
| `$WhatIfPreference` | global |

---

### `$PSCmdlet.ShouldProcess()`

Confirm in advanced functions

**Syntax**

```bash
if ($PSCmdlet.ShouldProcess("target","action")) { }
```

**Options**

| Flag | Description |
|------|-------------|
| `Use` | with [CmdletBinding(SupportsShouldProcess)] |

---


## Scripting & Flow

### `function`

Define a function

**Syntax**

```bash
function Name { param(); }
```

**Options**

| Flag | Description |
|------|-------------|
| `[CmdletBinding()]` | advanced |
| `param()` | positional params |
| `[Parameter(Mandatory)]` | attr |
| `[ValidateSet()]` | [ValidateRange()] |
| `pipeline` | input ValueFromPipeline |
| `begin{}` | process{} end{} |

---

### `param()`

Script/function parameters

**Syntax**

```bash
param([type]$Name = 'default')
```

**Options**

| Flag | Description |
|------|-------------|
| `[Parameter(Mandatory,Position=0)]` | — |
| `[ValidateNotNullOrEmpty()]` | — |
| `[ValidateScript({...})]` | — |
| `[Alias('n')]` | — |
| `[SupportsWildcards()]` | — |

---

### `if / elseif / else`

Conditional

**Syntax**

```bash
if (cond) { } elseif { } else { }
```

---

### `switch`

Multi-branch condition

**Syntax**

```bash
switch ($val) { 'a' { } default { } }
```

**Options**

| Flag | Description |
|------|-------------|
| `-Wildcard` | -Regex  -CaseSensitive |
| `-File` | read from file |
| `-Exact` | (default) |
| `{$_` | -gt 5} { } expression case |

---

### `for`

Counter loop

**Syntax**

```bash
for ($i=0; $i -lt N; $i++) { }
```

---

### `foreach`

Iterate collection

**Syntax**

```bash
foreach ($item in $collection) { }
```

**Options**

| Flag | Description |
|------|-------------|
| `or` | collection \| ForEach-Object { } |

---

### `while`

While loop

**Syntax**

```bash
while (condition) { }
```

---

### `do while / do until`

Post-condition loops

**Syntax**

```bash
do { } while (cond)  |  do { } until (cond)
```

---

### `break / continue`

Loop control

**Syntax**

```bash
break  |  continue
```

**Options**

| Flag | Description |
|------|-------------|
| `break` | N break N levels |
| `continue` | to next iteration |

---

### `return`

Return from function

**Syntax**

```bash
return $value
```

**Options**

| Flag | Description |
|------|-------------|
| `implicit` | return: last expression |

---

### `. (dot sourcing)`

Run script in current scope

**Syntax**

```bash
. .\script.ps1
```

**Options**

| Flag | Description |
|------|-------------|
| `loads` | functions into current scope |

---

### `& (call operator)`

Invoke script/cmd

**Syntax**

```bash
& '.\script.ps1' arg1 arg2
```

**Options**

| Flag | Description |
|------|-------------|
| `&` | $scriptblock  execute block |
| `&` | $exe  run executable |

---

### `Invoke-Expression` <sub>iex</sub>

Evaluate string as command

**Syntax**

```bash
Invoke-Expression 'Get-Process'
```

**Options**

| Flag | Description |
|------|-------------|
| `use` | carefully — security risk |

---

### `[ScriptBlock]`

Script block object

**Syntax**

```bash
$sb = { param($x) $x * 2 }
```

**Options**

| Flag | Description |
|------|-------------|
| `&` | $sb 5  invoke |
| `$sb.Invoke(5)` | invoke method |
| `$sb.ToString()` | get source |

---

### `#Requires`

Script requirements

**Syntax**

```bash
#Requires -Version 7.0
```

**Options**

| Flag | Description |
|------|-------------|
| `-Version` | minimum PS version |
| `-Modules` | module list |
| `-PSEdition` | Desktop/Core |
| `-RunAsAdministrator` | — |
| `-ShellId` | — |

---

### `[CmdletBinding()]`

Advanced function attribute

**Syntax**

```bash
[CmdletBinding(SupportsShouldProcess)]
```

**Options**

| Flag | Description |
|------|-------------|
| `ConfirmImpact` | High/Medium/Low/None |
| `DefaultParameterSetName` | — |
| `PositionalBinding=$false` | — |
| `HelpUri` | RemotingCapability |

---


## Environment

### `Get-ChildItem Env:`

List environment variables

**Syntax**

```bash
Get-ChildItem Env:
```

**Options**

| Flag | Description |
|------|-------------|
| `-Filter` | -Name |
| `-Include` | -Exclude |

---

### `$env:VAR`

Get env variable

**Syntax**

```bash
$env:PATH   $env:COMPUTERNAME
```

**Options**

| Flag | Description |
|------|-------------|
| `$env:USERPROFILE` | $env:TEMP |
| `$env:USERNAME` | $env:WINDIR |

---

### `$env:VAR = 'val'`

Set env variable (session)

**Syntax**

```bash
$env:MY_VAR = 'hello'
```

**Options**

| Flag | Description |
|------|-------------|
| `lasts` | only for current session |

---

### `[Environment]::SetEnvironmentVariable`

Set env variable (persistent)

**Syntax**

```bash
[Environment]::SetEnvironmentVariable('VAR','val','User')
```

**Options**

| Flag | Description |
|------|-------------|
| `User` | Machine  Process scope |
| `User:` | HKCU  Machine: HKLM (admin) |

---

### `[Environment]::GetEnvironmentVariable`

Get env variable by scope

**Syntax**

```bash
[Environment]::GetEnvironmentVariable('PATH','Machine')
```

**Options**

| Flag | Description |
|------|-------------|
| `User` | Machine  Process |

---

### `Get-Content Env:PATH`

Read PATH variable

**Syntax**

```bash
$env:PATH -split ';'
```

---

### `Set-Content Env:PATH`

Update PATH in session

**Syntax**

```bash
$env:PATH += ';C:\newdir'
```

---

### `[Environment]::OSVersion`

OS version info

**Syntax**

```bash
[Environment]::OSVersion
```

**Options**

| Flag | Description |
|------|-------------|
| `.Platform` | .Version  .VersionString |
| `.ServicePack` | — |

---

### `[System.Runtime.InteropServices.RuntimeInformation]`

OS / runtime detection

**Syntax**

```bash
[RuntimeInformation]::IsOSPlatform([OSPlatform]::Windows)
```

**Options**

| Flag | Description |
|------|-------------|
| `OSPlatform:` | Windows  Linux  OSX |
| `RuntimeIdentifier` | FrameworkDescription |
| `OSDescription` | ProcessArchitecture |

---

### `$IsWindows / $IsLinux / $IsMacOS`

Platform detection (PS6+)

**Syntax**

```bash
if ($IsLinux) { }
```

---

### `$PSEdition`

Desktop or Core edition

**Syntax**

```bash
if ($PSEdition -eq 'Core') { }
```

---


## Formatting & Output

### `Format-Table` <sub>ft</sub>

Table output

**Syntax**

```bash
obj | Format-Table [props]
```

**Options**

| Flag | Description |
|------|-------------|
| `-AutoSize` | -Wrap  -HideTableHeaders |
| `-GroupBy` | -Property @{N='..'E={..}} |
| `-View` | named view |

---

### `Format-List` <sub>fl</sub>

Property list output

**Syntax**

```bash
obj | Format-List [props]
```

**Options**

| Flag | Description |
|------|-------------|
| `-GroupBy` | -Property * all |
| `-Force` | -View |

---

### `Format-Wide` <sub>fw</sub>

Wide multi-column output

**Syntax**

```bash
obj | Format-Wide [prop]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Column` | N  -AutoSize |
| `-GroupBy` | -Property |

---

### `Format-Custom` <sub>fc</sub>

Custom view output

**Syntax**

```bash
obj | Format-Custom
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | -View custom view name |

---

### `Out-GridView` <sub>ogv</sub>

GUI interactive table

**Syntax**

```bash
obj | Out-GridView
```

**Options**

| Flag | Description |
|------|-------------|
| `-PassThru` | -Title  -OutputMode |

---

### `Out-String`

Objects to string

**Syntax**

```bash
obj | Out-String
```

**Options**

| Flag | Description |
|------|-------------|
| `-Stream` | line by line |
| `-Width` | -NoNewline (PS7+) |

---

### `ConvertTo-Html`

HTML table

**Syntax**

```bash
obj | ConvertTo-Html
```

**Options**

| Flag | Description |
|------|-------------|
| `-Property` | -Head  -Body |
| `-As` | Table/List  -Fragment |
| `-Title` | -PreContent  -PostContent |

---

### `Export-Clixml` <sub>epclixml</sub>

Serialize to XML

**Syntax**

```bash
obj | Export-Clixml -Path file.xml
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | -Encoding |
| `-NoClobber` | -Force |
| `-Confirm` | -WhatIf |

---

### `Import-Clixml` <sub>ipclixml</sub>

Deserialize from XML

**Syntax**

```bash
Import-Clixml -Path file.xml
```

---

### `ConvertTo-Json`

JSON output

**Syntax**

```bash
obj | ConvertTo-Json -Depth 5
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | default 2 |
| `-Compress` | -EnumsAsStrings |
| `-AsArray` | -EscapeHandling |

---

### `ConvertFrom-Json`

Parse JSON

**Syntax**

```bash
'{}' | ConvertFrom-Json
```

**Options**

| Flag | Description |
|------|-------------|
| `-Depth` | -AsHashtable |
| `-NoEnumerate` | — |

---

### `$FormatEnumerationLimit`

Max items shown in format

**Syntax**

```bash
$FormatEnumerationLimit = -1
```

**Options**

| Flag | Description |
|------|-------------|
| `default` | 4  use -1 for all |

---


## Misc

### `Get-Help` <sub>help / man</sub>

Get cmdlet documentation

**Syntax**

```bash
Get-Help Get-Item
```

**Options**

| Flag | Description |
|------|-------------|
| `-Full` | -Detailed  -Examples |
| `-Parameter` | name |
| `-Online` | open browser |
| `-ShowWindow` | GUI window |
| `Update-Help` | first |

---

### `Update-Help`

Download latest help files

**Syntax**

```bash
Update-Help
```

**Options**

| Flag | Description |
|------|-------------|
| `-Module` | specific module |
| `-Force` | reimport |
| `-SourcePath` | offline source |
| `-UICulture` | en-US  -Recurse |

---

### `Show-Command`

GUI form for any cmdlet

**Syntax**

```bash
Show-Command Get-EventLog
```

**Options**

| Flag | Description |
|------|-------------|
| `-Name` | -Height  -Width |
| `-NoCommonParameter` | — |

---

### `Get-History` <sub>h / ghy</sub>

Command history

**Syntax**

```bash
Get-History
```

**Options**

| Flag | Description |
|------|-------------|
| `-Count` | N |
| `-Id` | -CommandLine (filter) |

---

### `Invoke-History` <sub>r / ihy</sub>

Re-run history entry

**Syntax**

```bash
Invoke-History [-Id] N
```

**Options**

| Flag | Description |
|------|-------------|
| `-CommandLine` | search string |

---

### `Clear-History`

Clear command history

**Syntax**

```bash
Clear-History
```

**Options**

| Flag | Description |
|------|-------------|
| `-Id` | -Count N |
| `-CommandLine` | -Newest  -Oldest |

---

### `Add-History`

Add entry to history

**Syntax**

```bash
Add-History -InputObject obj
```

**Options**

| Flag | Description |
|------|-------------|
| `-Passthru` | — |

---

### `Start-Transcript`

Log session to file

**Syntax**

```bash
Start-Transcript [-Path] file
```

**Options**

| Flag | Description |
|------|-------------|
| `-Append` | -NoClobber |
| `-Force` | -IncludeInvocationHeader |
| `-UseMinimalHeader` | (PS7.2+) |

---

### `Stop-Transcript`

Stop session logging

**Syntax**

```bash
Stop-Transcript
```

---

### `Debug-Runspace`

Debug a runspace

**Syntax**

```bash
Debug-Runspace -Name name
```

**Options**

| Flag | Description |
|------|-------------|
| `-Id` | -Runspace  -BreakAll |

---

### `Set-PSDebug`

Enable script debugging

**Syntax**

```bash
Set-PSDebug -Trace 1
```

**Options**

| Flag | Description |
|------|-------------|
| `-Trace` | 0/1/2  -Step  -Strict |
| `-Off` | disable |

---

### `Set-StrictMode`

Strict coding rules

**Syntax**

```bash
Set-StrictMode -Version 3.0
```

**Options**

| Flag | Description |
|------|-------------|
| `-Version` | Off/1/2/3/Latest |

---

### `Measure-Command`

Time a script block

**Syntax**

```bash
Measure-Command { Get-Process }
```

---

### `Test-Json`

Validate JSON string (PS6+)

**Syntax**

```bash
'{}' | Test-Json
```

**Options**

| Flag | Description |
|------|-------------|
| `-Schema` | JSON schema string |
| `-SchemaFile` | path to schema |

---

### `ConvertTo-SecureString`

Encrypt string

**Syntax**

```bash
ConvertTo-SecureString 'pass' -AsPlainText -Force
```

---

### `New-Guid`

Generate a new GUID

**Syntax**

```bash
New-Guid
```

**Options**

| Flag | Description |
|------|-------------|
| `or` | [Guid]::NewGuid() |

---

### `Get-Random`

Get random number/item

**Syntax**

```bash
Get-Random
```

**Options**

| Flag | Description |
|------|-------------|
| `-Maximum` | -Minimum |
| `-Count` | N from collection |
| `-InputObject` | -SetSeed reproducible |
| `-Shuffle` | (PS7.1+) |

---

### `Start-Sleep` <sub>sleep</sub>

Pause execution

**Syntax**

```bash
Start-Sleep -Seconds N
```

**Options**

| Flag | Description |
|------|-------------|
| `-Seconds` | -Milliseconds |
| `-Duration` | (PS7+) timespan |

---

### `Get-Clipboard`

Get clipboard content

**Syntax**

```bash
Get-Clipboard
```

**Options**

| Flag | Description |
|------|-------------|
| `-Format` | Text/FileDropList/Image/Audio |
| `-Raw` | -TextFormatType |

---

### `Set-Clipboard`

Set clipboard content

**Syntax**

```bash
'text' | Set-Clipboard
```

**Options**

| Flag | Description |
|------|-------------|
| `-Value` | -Append  -AsHtml |
| `-Confirm` | -WhatIf |

---

### `Register-EngineEvent`

Subscribe to PS engine events

**Syntax**

```bash
Register-EngineEvent -SourceIdentifier PSExiting -Action {}
```

**Options**

| Flag | Description |
|------|-------------|
| `-SourceIdentifier` | -Action |
| `-MessageData` | -Forward |
| `-SupportEvent` | -MaxTriggerCount |

---

### `Register-ObjectEvent`

Subscribe to .NET events

**Syntax**

```bash
Register-ObjectEvent $obj EventName -Action {}
```

**Options**

| Flag | Description |
|------|-------------|
| `-InputObject` | -EventName |
| `-SourceIdentifier` | -Action |
| `-MessageData` | -Forward |

---

### `Wait-Event`

Wait for event

**Syntax**

```bash
Wait-Event [-SourceIdentifier name]
```

**Options**

| Flag | Description |
|------|-------------|
| `-Timeout` | seconds |

---

### `Get-Event`

List queued events

**Syntax**

```bash
Get-Event
```

**Options**

| Flag | Description |
|------|-------------|
| `-SourceIdentifier` | -EventIdentifier |

---

### `Remove-Event`

Delete event from queue

**Syntax**

```bash
Remove-Event -SourceIdentifier name
```

**Options**

| Flag | Description |
|------|-------------|
| `-EventIdentifier` | -Confirm |

---

### `Unregister-Event`

Cancel event subscription

**Syntax**

```bash
Unregister-Event -SourceIdentifier name
```

**Options**

| Flag | Description |
|------|-------------|
| `-EventIdentifier` | -Force  -Confirm |

---

### `ConvertFrom-Markdown`

Parse Markdown (PS7+)

**Syntax**

```bash
ConvertFrom-Markdown -Path file.md
```

**Options**

| Flag | Description |
|------|-------------|
| `-AsVT100EncodedString` | ANSI render |
| `-LiteralPath` | -InputObject |

---

### `Show-Markdown`

Render Markdown in terminal (PS7+)

**Syntax**

```bash
Get-Content file.md | Show-Markdown
```

**Options**

| Flag | Description |
|------|-------------|
| `-AsVT100EncodedString` | — |

---

