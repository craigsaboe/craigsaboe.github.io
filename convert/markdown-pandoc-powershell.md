---
layout: post
Title: Convert Word Docs to Markdown with Pandoc and Powershell
author: @craigsaboe
published: 2022-5-12 9:22:00
---

* Straightforward way to convert a directory structure of files of one type to another
* Uses Powershell to orchestrate, and [Pandoc](https://pandoc.org/) for file conversion, which supports a LOT of different inputs + outputs

```
$workingDir = 'C:\\Users\\csaboe\\The Kyle David Group LLC\\The Kyle David Group LLC Team Site - Documents\\Active Clients\\Ten4\\'
$wikiDir = 'C:\Projects\DCi-1\wiki\'
Set-Location -Path $workingDir

Get-ChildItem -File -Recurse -Filter *.docx | ForEach-Object {
  $filename = [System.IO.Path]::GetFileNameWithoutExtension($_)
  $targetDir = $wikiDir + ($file.DirectoryName -replace $workingDir,"") + '\'
  $targetFile = $targetDir + $filename + '.md'

  New-Item -Path $targetDir -ItemType Directory
  pandoc -f docx -t markdown -o ($targetFile) ($_.FullName)
}
```