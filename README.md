rOpenSci fellowship application
===============================

Goals
-----

Large data sets containing community taxonomic information are becoming
increasingly common, but the hierarchical nature of taxonomic
information makes manipulating these data sets difficult and many R
packages made for this have similar, yet unique, data structures and
functions. These differences make it difficult to use multiple packages
on the same data set and causes programmers to spend time creating and
maintaining analogous solutions for the same low-level problems of data
storage and manipulation, rather than focusing on novel functionality.
These inefficiencies are likely to get worse as the cost of
high-throughput sequences decreases, the interest in microbiome research
increases, and the number of associated R packages increases. To address
this problem, we are developing what we hope will become a standard in R
for storing, manipulating, and plotting taxonomic information and any
other application-specific data associated with it. Being awarded this
fellowship will allow us to devote the time needed to bring this project
to maturity and help integrate it into the community of R programmers
working with taxonomic data. A common infrastructure will allow
programmers to make focused, novel contributions without creating
redundant functionality. A cohesive community of packages will encourage
users to conduct analyses entirely within R, increasing the
effectiveness of reproducibility tools like `packrat` and R Markdown.

We are working on developing the rOpenSci package `taxa`, in
collaboration with Scott Chamberlain, to provide a set of all-purpose
classes and associated manipulation functions for taxonomic data,
modeled after the `dplyr` data-manipulation philosophy. In addition to
classes that represent `taxa`, classifications, and taxonomic trees, the
`taxa` packages has a class that stores any number of
application-specific tables, lists, or vectors mapped to a taxonomic
tree so that manipulations to the taxonomy are also applied to the
corresponding data and vice versa. Manipulation functions take into
account the hierarchical relationships between taxa as well. For
example, when filtering taxa or associated data, the supertaxa or
subtaxa of taxa that meet some condition can be preserved or discarded.
The `taxa` package also implements extremely flexible parsers to read
data in from nearly any format containing taxonomic information.

Although the `taxa` package is already useful, to make it a solid
foundation for the community to build on, we want to make it faster,
more robust, and work to integrate it with enough other packages. By
testing with very large data sets, we want to determine current limits
and bottlenecks so that we can identify parts of code to refactor or
replace with C++ to increase speed. We also want to implement parallel
processing to make better use of modern multi-core computers. Since we
hope to make this a foundational package, we want to add extensive unit
tests in addition to the many already implemented, to minimize bugs and
their effects on dependent packages. Perhaps most importantly, we want
to work with the maintainers of popular packages using taxonomic data to
integrate `taxa` and jump start adoption. We have just started the
process of integrating `taxa` into `taxize` \[@chamberlain2013taxize\],
the primary package for downloading taxonomic data from public
databases, and `metacoder`, our package for analysis and visualization
of community taxonomic data. Once `taxize` and `metacoder` are
refactored to use `taxa`, database searching/downloading and flexible
visualization will be easy using the classes implemented by `taxa`,
providing useful tools for a wide variety of research objectives and R
packages. This useful, all-purpose functionality will incentivize others
to adopt the `taxa` package as a standard.

The other related project we are working on is `metacoder`, an R package
for visualization and analysis of community taxonomic data, with an
emphasis on providing tools for microbiome research
\[@foster2017metacoder\]. `Metacoder` introduced a way of visualizing
statistics distributed throughout a hierarchy (e.g. a taxonomic tree) by
quantitatively mapping statistics to the the color or size of nodes and
edges in a tree. We call these “heat trees” and they have been
enthusiastically received as an intuitive and information-dense
alternative to stacked bar charts, which is the most common way taxon
abundance in communities are currently plotted in publications. The
`heat_tree` function in `metacoder` is highly flexible, yet only
requires a few arguments to produce high-quality figures in most cases,
since raw statistics are automatically mapped to color/size and the size
range of elements displayed are optimized for each graph to strike a
balance between avoiding overlaps and maximizing the apparent
differences. `Metacoder` also provides a way to simulate PCR in R, which
is important for selecting primers for metabarcoding research.

`Metacoder` is currently being significantly refactored to use the
classes provided by `taxa` and more functionality is being added
specific to community taxonomic data analysis. We are considering
splitting out the low-level plotting abilities of `metacoder` into its
own package, since these are universally useful for any hierarchical
data, not just community taxon abundance data from high-throughput
sequencing. In that case, `metacoder` would focus exclusively on aiding
analysis of community taxonomic data, generally from high-throughput
sequencing. One particularly useful high-level visualization technique
we want to facilitate is a matrix of unlabeled heat trees that show
which taxa are deferentially abundant between every pair-wise set of
treatments accompanied by a larger, labeled tree that functions as a
key. This can be used to show the results of thousands of statistical
tests and the treatments/taxa they apply to in a graph that can fit in a
publication. Currently, making these graphs is quite complicated, but we
believe we can design a function that will make creating these graphs
easy for users. We also want to implement pairs of parser and writer
functions that handle the common formats used in metabarcoding research
to make it easy for users move data in to and out of R. These parsers
will return `taxa` objects, so they would be very useful for all
packages that adopt the `taxa` package as a standard. They could also be
used to convert between file formats, since a user could read from one
format and write to another. The `taxa` classes are flexible enough that
we should be able to losslessly read and write the same format, so this
would provide a way to subset or otherwise modify large, complicated
files, using the powerful manipulation functions provided by `taxa`.

Encouraging adoption of this framework by both users and developers is
key to the success of this project. We hope to facilitate adoption by
developers by offering to help maintainers adapt existing packages to
`taxa`. Once a critical mass of packages have adopted `taxa`, we expect
that it will naturally be adopted by new packages without our direct
assistance. To attract users, we want to write a series of posts on
major R blogs that cover specific uses of the framework and demonstrate
its usefulness. We also plan to present this work at biological and
computational conferences, including the UseR 2018 conference and the
rOpenSci 2018 unconference. We have already submitted a workshop
proposal for the 2018 11th International Congress of Plant Pathology
joint conference on reproducible analysis of microbiome data in R, which
will focus on applying these tools. We hope to publish a paper on the
`taxa` package in the F1000 open access journal. Finally, if this
framework is adopted by the community as we hope, we would also want to
publish an article describing the resources available for all-R analyses
of taxonomic data using this framework.

Expected outcomes and timeline
------------------------------

### Months 1-3: Improvements to the `taxa` package

-   Add missing dplyr analog functions (e.g. summarise, group\_by, etc)
-   Port slowest parts of the code to C++ to improve speed
-   Add ability to use multiple cores to improve speed
-   Add exhaustive unit tests (test coverage of &gt; 95%)

### Months 4-8: Improvements to `metacoder`

-   Finish the transition to using `taxa`
-   Add function to easily create a heat tree matrix for pairwise
    comparison of treatments
-   For each major file format used in metabarcoding research, add a
    function to parse the file’s contents into the classes provided by
    `taxa` and a corresponding writer to recreate the file format. We
    read from and written to the same format, the process should
    be lossless.
-   Add automatic overlap avoidance for labels
-   Add support for plotting categorical information
-   Add ability to plot multiple colors per node/edge automatically when
    multiple values per taxon are supplied. Nodes would be pie charts
    and edges would be stacked bar charts.
-   Add ability to automatically query, download and plot silhouettes
    representing `taxa` from the pylopics database in place of nodes
-   Add ability to highlight/delineate groups of `taxa` with shaded
    polygons
-   Add ability to plot user-supplied images in place of nodes
-   Add support for interactive plots using `plotly`

### Months 9-12: Outreach and community building

-   Contact the maintainers of major packages using taxonomic
    information and offer to help adopt `taxa`
-   Finish refactoring of `taxize` to use `taxa`
-   Present at the 2018 rOpenSci Unconference
-   Present at the 2018 useR! conference
-   Conduct a workshop and reproducible microbiome analysis in R using
    these tool at the 2018 11th International Congress of Plant
    Pathology
-   Write a series of blogs for R-bloggers demonstrating the usefulness
    of the `taxa`/`taxize`/`metacoder` framework
-   Publish a journal article on `taxa` in F1000Research, or another
    open-access journal
-   Publish a journal article on reproducible microbiome analysis in R
    in an open-access journal

Collaborators
-------------

Niklaus Grünwald, Horticultural Crops Research Laboratory, USDA-ARS,
Corvallis, Oregon, United States of America

High level budget
-----------------

### 2018 useR! conference

-   Airfare from Portland, OR to Brisbane Australia: $1,400
-   Per diem meals and incidentals Brisbane Australia: $98 x 4 days =
    $392
-   Per diem lodging Brisbane Australia: $159 x 4 days = $636
-   Student registration fee: $125

*Estimated subtotal: $2553*

### Salery

-   Compensation: $2,000 x 12 months = $24,000

*Estimated subtotal: $24,000*

### Total: ...

References
----------
