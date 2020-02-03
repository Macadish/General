# Commonly Used Bash Codes

* Check File Size
```bash
# Show the file size in Gb
stat --printf="%s GB\n" *.fna | awk '{print $1/1000000}'
ls -lh | awk '{print $5, $9}'
du -a -h --max-depth=1 | sort -hr
du -h -d 1 | sort -n #for macOS
```
* Submit a Job
