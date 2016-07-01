---
layout: post
category : 
tagline: ""
tags : [Powershell, Commands]
---
{% include JB/setup %}

Some usefull Windows powershell and grep commands

* Select unique single letter words from a text file.

        cat textFile.txt |% { $_ -split '\s' } |? { $_ -match '^.$' } | select -Unique

* Select strings that contain a single characters surrounded by space and folloed by a number, e.g. " a -0.23243"

         sls '\s\w($|\s+-?[0-9.]+)' textFile.txt
         
* Find strings that contain capital letters

        cat list | grep -E \w*[A-Z]+\w*
        
* Find all strings in FileA which are not present in FileB

        grep -F -x -v -f fileB fileA
        
* Count lines in a file

        cat list | find /v /c ""
         
* Display the first 100 lines in a text file:

         powershell -command "& {Get-Content lm.arpa -TotalCount 100}"

* Split large text file into smaller files (make sure that the "split" directory exists)

```
$reader = new-object System.IO.StreamReader("C:\full_path_to_large_file.txt")
$count = 1
$upperBound = 1000000
$ext="txt"
$rootName = "C:\split\"
$fileName = "{0}{1}.{2}" -f ($rootName, $count, $ext)
while(($line = $reader.ReadLine()) -ne $null)
{
    Add-Content -path $fileName -value $line
    if((Get-ChildItem -path $fileName).Length -ge $upperBound)
    {
        ++$count
        $fileName = "{0}{1}.{2}" -f ($rootName, $count, $ext)
    }
}

$reader.Close()
```
* Dispay N line before|after matching line

         grep -(B|A)N <expr> files
