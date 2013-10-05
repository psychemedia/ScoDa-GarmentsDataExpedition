
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

accord <- read.csv("~/code/ScoDa-GarmentsDataExpedition/matchingTests/accord.csv")bgmea <- read.csv("~/code/ScoDa-GarmentsDataExpedition/code/matchingTests/bgmea.csv", header=F)tmp=rbind(data.frame(V2=accord$FactoryName,typ='accord'),data.frame(V2=bgmea$V2,typ='BGMEA'))write.csv(tmp, "data.csv", row.names=FALSE)


Load data.csv into OpenRefine ( project data-csv.google-refine.tar.gz ) and make a start cleaning and clustering on the names (more could be done) to start normalising them. Output is file postOpenRefine-data-csv.csv

Next step (not yet done) is to go through postOpenRefine-data-csv.csv (in python, probably) and generate two sets - one with names from accord list, one with names from bgmea list.

We can then look for set intersections and set differences to find names in both lists, in just bgmea list, in just accord list.


APPROACH 2
----------

Not tried yet - e.g. script I started developing in http://blog.ouseful.info/2012/09/26/merging-data-sets-based-on-partially-matched-data-elements/