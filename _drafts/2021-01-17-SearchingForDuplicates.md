---
title:  "Searching for duplicates"
header:
  teaser: "images/commandline-example-helloworld.jpg"
permalink: "/2021/SearchingForDuplicates"
published: true
comments: true
tags:
  - bash
  - Unix
  - coding
---



List files in a directory, print each directory name (sanity check) and save duplicates within each directory to a tab delimited file

ls | while read i; do echo $i; cd $i; find . ! -empty -type f -exec md5sum {} + | sort | uniq -w32 -dD | tr -s [:space:] | sed 's/\ /\t/' >> ../photodupes.tsv; cd ../; done

remove all files in the 'facebook' folders that are duplicates
find . ! -empty -type f -exec md5sum {} + | sort | uniq -w32 -dD | tr -s [:space:] | sed 's/\ /\t/' | grep -i 'Facebook' | cut -f 2- -d '.' | sed 's/\///' | while read i; do rm "$i"; done

exiftool '-FileName<CreateDate' -d %Y%m%d_%H%M%S%%-c.%%e


find . ! -empty -type f -exec md5sum {} + | sort | uniq -w32 -dD | tr -s [:space:] | sed 's/\ /\t/' | grep "DUPLICATE" | cut -f 2- -d '.' | sed 's/\///' | while read i; do rm "$i"; done
