SUPERVIZOR UTILS
================

Various utilities for http://supervizor.kpk-rs.si

Examples
--------

Get page of some organisation and parse out the top 50 receiver firms (in simple form).

  ./get-org-page 75833 | ./parse-firms


Get receiver firms with links (x = extended)

  ./get-raw-org-page 75833 | tee temp1 | ./parse-firms-x > temp2

Get the main theme of firm and get it's SKD main group

  cat temp1 | ./parse-firms-x | head -n 2 | ./get-firms

Or all in one command (get only top 10 firms):

  ./get-raw-org-page 75833 | ./parse-firms-x | head -n 10 | ./get-firm-groups

Example of output:

  17.392.026,82	     /organ/75833/podj/68297530/    RBANKA d.d.	Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
  15.376.137,96	     /organ/75833/podj/98491881/    KOMUNALA Nova d.d. Zbiranje in odvoz nenevarnih odpadkov	   OSKRBA Z VODO, RAVNANJE Z ODPLAKAMI IN ODPADKI, SANIRANJE OKOLJA
  14.331.010,05	     /organ/75833/podj/95666222/    PREKMORJE d.d. - v stečaju Gradnja cest	GRADBENIŠTVO
  13.726.010,41	     /organ/75833/podj/98026305/    BANKA TRST d.d.  Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
  13.350.549,64	     /organ/75833/podj/94314527/    NOVA NBM d.d.     Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
  12.355.099,16	     /organ/75833/podj/91503027/    VODOVODI IN KANALIZACIJA NOVA LJUBLJAN d.d.		Zbiranje, prečiščevanje in distribucija vode OSKRBA Z VODO, RAVNANJE Z ODPLAKAMI IN ODPADKI, SANIRANJE OKOLJA
  11.208.577,77	     /organ/75833/podj/39716651/    RPG, d.d.	Gradnja cest GRADBENIŠTVO
  6.688.331,72	     /organ/75833/podj/52398790/    ARWIGO, d.o.o.	Medkrajevni in drug cestni potniški promet	PROMET IN SKLADIŠČENJE
  5.393.787,71	     /organ/75833/podj/77494962/    HAPY LEASING d.o.o.	Dejavnost finančnega zakupa	    FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
  5.293.943,02	     /organ/75833/podj/40502368/    KBBS d.d.	 Drugo denarno posredništvo  FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI

