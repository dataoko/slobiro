SUPERVIZOR UTILS
================

Various utilities for http://supervizor.kpk-rs.si

Search orgs
-----------

Main search:

	$ ./search-orgs "škofja" | head -n3
	30090					 CENTER SLEPIH, SLABOVIDNIH IN STAREJŠIH ŠKOFJA LOKA
	30627					 CENTER ZA SOCIALNO DELO ŠKOFJA LOKA
	63223					 DIJAŠKI DOM ŠKOFJA LOKA
	
Raw:

	$ ./search-orgs-raw "univerza škofja loka"
	[
	  {
	      "id": 71820, 
	      "label": "LJUDSKA UNIVERZA \u0160KOFJA LOKA"
	 }
	]

From Raw to main:

     	 $ ./search-orgs-raw "srednja šola" | ./parse-search-res | head -n3
	 69370					      DVOJEZIČNA SREDNJA ŠOLA LENDAVA KETNYELVU KOZEPISKOLA LENDVA
	 70440					      EKONOMSKA GIMNAZIJA IN SREDNJA ŠOLA RADOVLJICA
	 69620					      GIMNAZIJA IN EKONOMSKA SREDNJA ŠOLA TRBOVLJE


From org name to page:
----------------------

	$ ./get-org-url "srednja šola muta"
	http://sunshine.owca.info/organ/70300/


Parse organisation data by SKD-s:
---------------------------------

Find page os specific org, load it, parse SKD (groups), translate them to root groups, sum groups together and sort by amount descending.

     ./get-org-url "OBČINA POSTOJNA" | xargs ./load-page | ./parse-skds | ./to-root-groups | ./sum-amonts-by-groups | tee temp1 | sort -nr

Output:

	26717386      GRADBENIŠTVO
	21641277      FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
	11926663      STROKOVNE, ZNANSTVENE IN TEHNIČNE DEJAVNOSTI
	7719177	      INFORMACIJSKE IN KOMUNIKACIJSKE DEJAVNOSTI
	5403339	      DRUGE RAZNOVRSTNE POSLOVNE DEJAVNOSTI
	5039914	      OSKRBA Z VODO, RAVNANJE Z ODPLAKAMI IN ODPADKI, SANIRANJE OKOLJA
	3679069	      PROMET IN SKLADIŠČENJE
	3226351	      DEJAVNOST JAVNE UPRAVE IN OBRAMBE, DEJAVNOST OBVEZNE SOCIALNE VARNOSTI
	2884495	      PREDELOVALNE DEJAVNOSTI
	2826572	      KULTURNE, RAZVEDRILNE IN REKREACIJSKE DEJAVNOSTI
	2102741	      DRUGE DEJAVNOSTI
	2087309	      OSKRBA Z ELEKTRIČNO ENERGIJO, PLINOM IN PARO
	1979931	      TRGOVINA, VZDRŽEVANJE IN POPRAVILA MOTORNIH VOZIL
	1575485	      POSLOVANJE Z NEPREMIČNINAMI
	1127015	      GOSTINSTVO
	587064	      ZDRAVSTVO IN SOCIALNO VARSTVO
	190670	      
	184014	      IZOBRAŽEVANJE
	137443	      KMETIJSTVO IN LOV, GOZDARSTVO, RIBIŠTVO
	17941	      RUDARSTVO

Sum them also:

	$ cat temp1 | ./sum-all-amounts
	101053856

Parse organisation's providers:
------------------------------

Get organisation's url, load it, parse firms out of it, get groups of firms (w/ separate requests, 0.3s delay) and get root groups out of those.

	$ ./get-org-url "OBČINA POSTOJNA" | xargs ./load-page | ./parse-firms | head -n5 | ./get-firm-groups | ./get-firm-root-groups

	8139828		/organ/75949/podj/24009725/	      PZ SLOVENIJE, d.d. - bančna skupina Nove KBM d.d.	Drugo denarno posredništvo FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
	7362336		/organ/75949/podj/98026305/	      BANKA MORJE d.d.	 Drugo denarno posredništvo	FINANČNE IN ZAVAROVALNIŠKE DEJAVNOSTI
	7297652		/organ/75949/podj/95666222/	      GORENJSKA d.d. - v stečaju	       Gradnja cest	GRADBENIŠTVO
	7164203		/organ/75949/podj/63624443/	      CPR d.d. Gradnja cest	       GRADBENIŠTVO
	6391536		/organ/75949/podj/28928695/	      VATMEL d.o.o.    Druge telekomunikacijske dejavnosti	INFORMACIJSKE IN KOMUNIKACIJSKE DEJAVNOSTI


Get sums of all first 50 and of "construction" companies.

	echo GRD: `./get-org-url "OBČINA POSTOJNA" | xargs ./load-page | ./parse-firms | ./get-firm-groups | ./get-firm-root-groups | tee temp1 | grep "GRADBENIŠTVO" | ./sum-all-amounts` ; cat temp1 | echo "VSI: " `./sum-all-amounts`
	GRD: 16773808
	VSI: 51284622

