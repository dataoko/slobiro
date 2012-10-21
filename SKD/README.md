SKD - Standarda Klasifikacija Dejavnosti
========================================

Examples:
--------

get the topmost parent code of the group name:

	$ cat SKD.csv | ./parse | ./find "Pogrebna dejavnost" | ./getgroup
	S

Get the name based on the code

	$ cat SKD.csv | ./parse | ./getname S
	DRUGE DEJAVNOSTI

Get the top most name based on a subgroup name

	$ ./getgroupname "Gradnja cest"
	GRADBENIŠTVO


Todo:
-----

* Programatically get the CSV file. The websites seems to use POST with some session data so I wasn't able to at this poitn.