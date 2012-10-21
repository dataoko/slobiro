SKD - Standarda Klasifikacija Dejavnosti
========================================

Examples:
--------

	~/Work/slobiro/SKD$ cat SKD.csv | ./parse | ./find "Pogrebna dejavnost" | ./getgroup
	S

	~/Work/slobiro/SKD$ cat SKD.csv | ./parse | ./getname S
	DRUGE DEJAVNOSTI

Todo:
-----

* Programatically get the CSV file. The websites seems to use POST with some session data.