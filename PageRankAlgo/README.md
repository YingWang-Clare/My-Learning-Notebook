Most of the notes come from [this great tutorial](https://www.cs.princeton.edu/~chazelle/courses/BIB/pagerank.htm).

It counts the number, and quality, of links to a page which determines an estimation of how important the page is. The underlying assumption is that pages of importance are more likely to receive a higher volume of links from other pages.

PageRank is defined in the original Google paper as follows:


PR(A) = (1-d) + d (PR(T1)/C(T1) + ... + PR(Tn)/C(Tn))


where,

* we assume that a page A has pages T1 to Tn which point to it (i.e., are citations).
* d is a damping factor which can be set between 0 and 1. It is usually set to 0.85.
* C(A) is defined as the number of links going out of page A.     
* Note that the PageRanks form a probability distribution over web pages, so the sum of all web pages' PageRanks will be one.    
          
1. PR(Tn) - Each page has a notion of its own self-importance. That’s “PR(T1)” for the first page in the web all the way up to “PR(Tn)” for the last page
2. C(Tn) - Each page spreads its vote out evenly amongst all of it’s outgoing links. The count, or number, of outgoing links for page 1 is “C(T1)”, “C(Tn)” for page n, and so on for all pages.
3. PR(Tn)/C(Tn) - so if our page (page A) has a backlink from page “n” the share of the vote page A will get is “PR(Tn)/C(Tn)”
4. d(... - All these fractions of votes are added together but, to stop the other pages having too much influence, this total vote is “damped down” by multiplying it by 0.85 (the factor “d”)
5. (1 - d) - The (1 – d) bit at the beginning is a bit of probability math magic so the “sum of all web pages' PageRanks will be one”: it adds in the bit lost by the d(.... It also means that if a page has no links to it (no backlinks) even then it will still get a small PR of 0.15 (i.e. 1 – 0.85). (Aside: the Google paper says “the sum of all pages” but they mean the “the normalised sum” – otherwise known as “the average” to you and me.


