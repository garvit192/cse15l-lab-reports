# Lab Report 3

This lab report covers a few interesting uses and options of the find command

## Looking for a file in multiple diretories
We can use the  find command to look for files in multiple directories without having to use * to set the path type of the location. This way we can search for files without having to be limited to a single path type.

For example the file "chapter-1.txt" is located in the directory technical/911report, however if we are not sure of its location we can search for it in the technical/government/Media as well if we suspect that the file might be there

```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find technical/911report technical/government/Media -name "chapter-1.txt"
technical/911report/chapter-1.txt
```
It is possible to combine using * with this method to look through directories with different path length. For example we can look for the file "chapter-1.txt" in all directories in technical that match the format technical/* and technical/government/*

```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find technical/* technical/government/* -name "chapter-1.txt"
technical/911report/chapter-1.txt
```
Source [here](https://linuxhandbook.com/find-command-examples/#search-for-files-in-multiple-directories)

## Finding files based on file size
It is possible to use the `-size` option to get files based on their size. We can modify it by using + and - to set the file size to be greater than or less than the number mentioned

For example if I need files whose size is greater than 100KB from technical/government/Env_Prot_Agen I can do the following
``` 
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find technical/government/Env_Prot_Agen -size +100k 
technical/government/Env_Prot_Agen/multi102902.txt
technical/government/Env_Prot_Agen/ctm4-10.txt
technical/government/Env_Prot_Agen/bill.txt
technical/government/Env_Prot_Agen/tech_adden.txt
```

It is also possible to find the file size in a particular range like 100KB to 150KB
```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find technical/government/Env_Prot_Agen -size +100k -size -150k
technical/government/Env_Prot_Agen/ctm4-10.txt
```
Source [here](https://linuxhandbook.com/find-command-examples/#find-big-files-or-small-search-based-on-file-size)
## Finding files based on time of last acess
The `-amin` option can be used to find files based on a specific access time. It can give us files that were accessed based on the time elapsed since they were last opened.

The following gives files accessed in last 10 mins
```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find technical/*/* -amin -10
technical/911report/chapter-10.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-3.txt
technical/biomed/1471-2091-3-31.txt
technical/biomed/1471-213X-1-1.txt
technical/biomed/1471-213X-1-6.txt
technical/government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
technical/government/About_LSC/commission_report.txt
technical/government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
technical/government/Env_Prot_Agen/ro_clear_skies_book.txt
technical/government/Env_Prot_Agen/ctm4-10.txt
technical/government/Gen_Account_Office/ai9868.txt
technical/plos/journal.pbio.0020019.txt
```

It is also possible to get a range of acess times like done to find files with specific filesize.

```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find technical/*/* -amin +9  -amin -12
technical/government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
technical/government/About_LSC/commission_report.txt
technical/government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
technical/government/Env_Prot_Agen/ro_clear_skies_book.txt
technical/government/Env_Prot_Agen/ctm4-10.txt
```
Source [here](https://linuxhandbook.com/find-command-examples/#find-recently-modified-files-search-based-on-modify-or-creation-time)
## Excluding a directory from 
While finding files it might be useful to skip over a few directories since they are too large or it is known that the file is not in that directory. By using the `! -path` option we can do that.

For example we want to find the file "bill.txt" which is in technical/government/Env_Prot_Agen, but don't want to search through technical/plos
```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find ./* -name "bill.txt" ! -path technical/plos/*    
./technical/government/Env_Prot_Agen/bill.txt
```

To confirm that this doesskip the directory, I ran the command again but in place of technical/plos/* I entered technical/government/Env-Prot-Agen/*. This should not produce any results.
```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find ./* -name "bill.txt" ! -path technical/government/Env-Prot-Agen/*
zsh: no matches found: technical/government/Env-Prot-Agen/*
```

It is also possible to exclude multiple directories with this 
```
garvitagarwal@Garvits-MacBook-Pro stringsearch-data-main % find ./* -name "bill.txt" ! -path technical/government/Env-Prot-Agen/* ! -path technical/plos/*
zsh: no matches found: technical/government/Env-Prot-Agen/*
```
Source [here](https://www.crybit.com/exclude-directories/#:~:text=.%2Fcry%2Ffindme-,Method%201%20%3A%20Using%20the%20option%20%E2%80%9C%2Dprune%20%2Do%E2%80%9D,print%E2%80%9D%20switches%20with%20find%20command.&text=The%20directory%20%E2%80%9Cbit%E2%80%9D%20will%20be%20excluded%20from%20the%20find%20search!)
