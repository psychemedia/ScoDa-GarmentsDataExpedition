
APPROACH 1
----------


#Data file in code/assortedScrapers
sqlite3 scraperwiki.sqlite

sqlite> .output bgmea.csv
sqlite> select * from BGMEA_indexData;
sqlite> .output stdout


#I think sqlite table BGMEA may have addresses, but I didn't tidy up whitespace in the scraper

Scraped data from accord doc in accord.csv

Merge the company names lists from accord.csv and bgmea.csv in R:

accord <- read.csv("~/code/ScoDa-GarmentsDataExpedition/matchingTests/accord.csv")bgmea <- read.csv("~/code/ScoDa-GarmentsDataExpedition/matchingTests/bgmea.csv", header=F)tmp=rbind(data.frame(V2=accord$FactoryName,typ='accord'),data.frame(V2=bgmea$V2,typ='BGMEA'))write.csv(tmp, "data.csv", row.names=FALSE)


Load data.csv into OpenRefine ( project data-csv.google-refine.tar.gz ) and make a start cleaning and clustering on the names (more could be done) to start normalising them. Output is file postOpenRefine-data-csv.csv

Next step (not yet done) is to go through postOpenRefine-data-csv.csv (in python, probably) and generate two sets - one with normalised names from accord list, one with normalised names from bgmea list.

We can then use these two sets of normalised names to look for set intersections and set differences to find names in both lists, in just bgmea list, in just accord list.


APPROACH 2
----------

Not tried yet - e.g. script I started developing in http://blog.ouseful.info/2012/09/26/merging-data-sets-based-on-partially-matched-data-elements/

Something else we could add in to the partial matching - just match the first characters of the cleaned (uppercased, stripped apostrophe, full stop, brackets, ltd/limited etc) company names.


APPROACH 3
----------

Is this fuzzy matching Python library useful for a recipe? https://pypi.python.org/pypi/jellyfish/0.1.2

Any other fuzzy matching libraries out there, or recipes for using them to reconcile fuzzily matching lists?

Any clustering libraries that might be useful in this respect?


APPROACH 4
----------

For countries where OpenCorporates data exists, use OpenRefine reconciliation service to try to get back corporate identifiers based on company name.