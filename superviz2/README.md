SUPERVIZOR UTILS
================

Various utilities for http://supervizor.kpk-rs.si

Examples
--------

Search the orgranisations by name:

       ./search-org "OBČINA SEV" | ./parse-serach-res

Find page of specific organisation and load the page, parse SKD-s, sum them and sort them top to bottom. This is based on new SKD-s supervizor functionality:

     ./get-organ-url "OBČINA POSTOJNA" | xargs ./load-page | ./parse-skds | ./to-toplevel-groups | \
     ./sum-groups | sort -nr > out/postojna.skdsums


