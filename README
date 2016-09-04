Tuls 1.0

A program that basically just does 'ls'. However, there are two reasons for this program.

1: Its script friendly. Easy to awk sections and always knowing what you get.

2: When using 'ls' in a script, you never know if its going to work between different
   linux distributions. Using tuls, you know it will work.


This program was made by Cruxis for Turranius. Big props to Cruxis for it. Thanks bud!


How to install it? 
There are two ways. If you run linux, you can most likely just copy the binary to /glftpd/bin
or where ever you want to put it.

The other way is to compile the source yourself.
Simply: gcc tuls.c -o /glftpd/bin/tuls


Might want to chmod it to 755 too.

Simply running it will show you if it works or not.



There is only one option that tuls accepts. Thats the path to list. 
If none is defined, it will list the directory you are currently in.

Sorting is a bit trickier. By default it does not sort at all.

With bash, you can use the following examples to sort.


Sort by date:
Since tuls shows seconds since 1970-01-01, its best to sort on that.
Example: tuls | tr '^' ' ' | sort -k6 -n -r | tr ' ' '^'
Would sort the output by date, oldest last. To reverse it, remove the -r from sort.


Sort by name:
Example: tuls | tr -s ':' ' ' | sort -k4 -n -r
Would sort the output by name. To reverse order, remove the -r from sort.


Of course, when sorting, you might not want to to display the "Listing blabla" text 
or the . and .. directories.
If so, simple add: egrep -v "^Listing\ |::\.[\.\:]::"
and it wont display those.
Example: tuls | egrep -v "^Listing\ |::\.[\.\:]::" | tr '^' ' ' | sort -k6 -n -r | tr ' ' '^'


If you want to define how to show the date on a file/dir, you can.
The 'date' format is a bit different for different distributions, but for linux:
Example: date -d "1970-01-01 `tuls / | grep "::::root::::" | cut -d '^' -f6` sec" +%F" "%T
You can now modify the +%F" "%T to any other format you want the date to be displayed in.


You may also specify your own list mode. Slower but it works.

Example:
for rawdata in `tuls | egrep -v "^Listing\ |::\.[\.\:]::" | tr '^' ' ' | sort -k6 -n -r | tr ' ' '^'`
do
  perm="`echo "$rawdata" | awk -F"::::" '{print $1}'`"
  name="`echo "$rawdata" | awk -F"::::" '{print $4}'`"
  date="`echo "$rawdata" | awk -F"::::" '{print $5}' | cut -d '^' -f1-5 | tr '^' ' '`"
  secs="`echo "$rawdata" | awk -F"::::" '{print $5}' | cut -d '^' -f6`"

  echo "$perm $name $date $secs"
done


If you also want to translate the uid and gid using /etc/passwd & /etc/group:
for rawdata in `tuls | egrep -v "^Listing\ |::\.[\.\:]::" | tr '^' ' ' | sort -k6 -n -r | tr ' ' '^'`
do
  perm="`echo "$rawdata" | awk -F"::::" '{print $1}'`"
  uid="`echo "$rawdata" | awk -F"::::" '{print $2}'`"
  gid="`echo "$rawdata" | awk -F"::::" '{print $3}'`"
  name="`echo "$rawdata" | awk -F"::::" '{print $4}'`"
  date="`echo "$rawdata" | awk -F"::::" '{print $5}' | cut -d '^' -f1-5 | tr '^' ' '`"
  secs="`echo "$rawdata" | awk -F"::::" '{print $5}' | cut -d '^' -f6`"

  username="`grep ":$uid:[0-9]" /etc/passwd | cut -d ':' -f1`"
  group="`grep ":$gid:" /etc/group | cut -d ':' -f1`"

  echo "$perm $username $group $name $date $secs"
done


Oh well, you get the idea.

/Turranius - 2004