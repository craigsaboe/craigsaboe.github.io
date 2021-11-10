Title: Pull a list of filenames in a UNC path
Date: 2021-11-10 9:22:00
Category: General

* To get the text list of files in a directory, you can normally do: <code>dir > filenames.txt</code>
* However, the Windows CLI can't use a UNC path as the current dir, so you need to use the Powershell CLI.  
* Once in the CLI, 'cd' to the UNC path and <code>dir > filenames.txt</code> will work
* 'dir' returns a table of info along with the filenames; to just get a straight list of filenames, use <code>Get-ChildItem -Name > C:\your\filename\here.txt}</code>