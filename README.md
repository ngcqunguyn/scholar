scholar.jar
scholar.jar is a Java module that implements a querier and parser for Google Scholar's output. Its classes can be used independently, but it can also be invoked as a command-line tool.

This code is converted from Python code scholar.py of Christian (https://github.com/ckreibich/scholar.py). You can see his contact from his git-hub page above.

Thanks Christian for you greate work.

Cheers,
Quy Nguyen

Features

Extracts publication title, most relevant web link, PDF link, number of citations, number of online versions, link to Google Scholar's article cluster for the work, Google Scholar's cluster of all works referencing the publication.
Supports the full range of advanced query options provided by Google Scholar, such as title-only search or publication date timeframes.
Supports article cluster IDs, i.e., information relating to the variants of an article already identified by Google Scholar
Supports retrieval of citation details in standard external formats as provided by Google Scholar, including BibTeX and EndNote.
Command-line tool prints entries in CSV format, simple plain text, or in the citation export format.
Cookie support for higher query volume, including ability to persist cookies to disk across invocations.
Note

I will always strive to add features that increase the power of this API, but I will never add features that intentionally try to work around the query limits imposed by Google Scholar. Please don't ask me to add such features.

Example

Try java - jar scholar.jar --help for all available options. Note, the command line arguments changed considerably in version 2.0! A few examples:

Retrieve one article written by Einstein on quantum theory:

$ java - jar scholar.jar -c 1 --author "albert einstein" --phrase "quantum theory"
         Title On the quantum theory of radiation
           URL http://icole.mut-es.ac.ir/downloads/Sci_Sec/W1/Einstein%201917.pdf
          Year 1917
     Citations 184
      Versions 3
    Cluster ID 17749203648027613321
      PDF link http://icole.mut-es.ac.ir/downloads/Sci_Sec/W1/Einstein%201917.pdf
Citations list http://scholar.google.com/scholar?cites=17749203648027613321&as_sdt=2005&sciodt=0,5&hl=en
 Versions list http://scholar.google.com/scholar?cluster=17749203648027613321&hl=en&as_sdt=0,5
Note the cluster ID in the above. Using this ID, you can directly access the cluster of articles Google Scholar has already determined to be variants of the same paper. So, let's see the versions:

$ java - jar scholar.jar -C 17749203648027613321
         Title On the quantum theory of radiation
           URL http://icole.mut-es.ac.ir/downloads/Sci_Sec/W1/Einstein%201917.pdf
     Citations 184
      Versions 0
    Cluster ID 17749203648027613321
      PDF link http://icole.mut-es.ac.ir/downloads/Sci_Sec/W1/Einstein%201917.pdf
Citations list http://scholar.google.com/scholar?cites=17749203648027613321&as_sdt=2005&sciodt=0,5&hl=en

         Title ON THE QUANTUM THEORY OF RADIATION
           URL http://www.informationphilosopher.com/solutions/scientists/einstein/1917_Radiation.pdf
     Citations 0
      Versions 0
      PDF link http://www.informationphilosopher.com/solutions/scientists/einstein/1917_Radiation.pdf

         Title The Quantum Theory of Radiation
           URL http://web.ihep.su/dbserv/compas/src/einstein17/eng.pdf
     Citations 0
      Versions 0
      PDF link http://web.ihep.su/dbserv/compas/src/einstein17/eng.pdf
Let's retrieve a BibTeX entry for that quantum theory paper. The best BibTeX often seems to be the one linked from search results, not those in the article cluster, so let's do a search again:

$ java - jar scholar.jar -c 1 --author "albert einstein" --phrase "quantum theory" --citation bt
@article{einstein1917quantum,
  title={On the quantum theory of radiation},
  author={Einstein, Albert},
  journal={Phys. Z},
  volume={18},
  pages={121--128},
  year={1917}
}
