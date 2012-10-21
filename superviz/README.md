SUPERVIZOR UTILS
================

Various utilities for http://supervizor.kpk-rs.si

Examples
--------

Get page of some organisation and parse out the top 50 receiver firms (in simple form).

    $ ./get-org-page 75833 | ./parse-firms


Get receiver firms with links (x = extended)

    $ ./get-raw-org-page 75833 | tee temp1 | ./parse-firms-x > temp2

Get the main theme of firm and get it's SKD main group

    $ cat temp1 | ./parse-firms-x | head -n 2 | ./get-firms

Or all in one command (get only top 10 firms):

    $ ./get-raw-org-page 75833 | ./parse-firms-x | head -n 10 | ./get-firm-groups

Example of output:
  
    17392026	     /organ/75833/podj/68297530/    RBANKA d.d.	Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
    15376137	     /organ/75833/podj/98491881/    KOMUNALA Nova d.d. Zbiranje in odvoz nenevarnih odpadkov	   OSKRBA Z VODO, RAVNANJE Z ODPLAKAMI IN ODPADKI, SANIRANJE OKOLJA
    14331010	     /organ/75833/podj/95666222/    PREKMORJE d.d. - v stečaju Gradnja cest	GRADBENIŠTVO
    13726010	     /organ/75833/podj/98026305/    BANKA TRST d.d.  Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
    13350549	     /organ/75833/podj/94314527/    NOVA NBM d.d.     Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
    12355099	     /organ/75833/podj/91503027/    VODOVODI IN KANALIZACIJA NOVA LJUBLJAN d.d.		Zbiranje, prečiščevanje in distribucija vode OSKRBA Z VODO, RAVNANJE Z ODPLAKAMI IN ODPADKI, SANIRANJE OKOLJA
    11208577	     /organ/75833/podj/39716651/    RPG, d.d.	Gradnja cest GRADBENIŠTVO
    6688331	     /organ/75833/podj/52398790/    ARWIGO, d.o.o.	Medkrajevni in drug cestni potniški promet	PROMET IN SKLADIŠČENJE
    5393787	     /organ/75833/podj/77494962/    HAPY LEASING d.o.o.	Dejavnost finančnega zakupa	    FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
    5293943	     /organ/75833/podj/40502368/    KBBS d.d.	 Drugo denarno posredništvo  FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI


Finally, get just the amounts and main groups for statistics:

    $ ./get-raw-org-page 75833 | ./parse-firms-x | head -n 3 | ./get-firm-groups

Ouptut:

    17392026		     FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
    15376137		     OSKRBA Z VODO, RAVNANJE Z ODPLAKAMI IN ODPADKI, SANIRANJE OKOLJA
    14331010		     GRADBENIŠTVO

