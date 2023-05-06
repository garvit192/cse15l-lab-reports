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

## 