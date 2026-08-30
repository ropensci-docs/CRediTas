# Get started

## CRediTas

The goal of CRediTas is to facilitate the tedious job of creating
[CRediT authors statements](https://credit.niso.org/) for scientific
publications.

### Installation

You can install the development version of CRediTas from
[r-universe](https://r-universe.dev/) with:

``` r

install.packages("CRediTas", repos = "https://ropensci.r-universe.dev")
```

Or you can install de long term release version from
[CRAN](https://CRAN.R-project.org/package=CRediTas) as usual:

``` r

install.packages("CRediTas")
```

### Create a template

The workflow is meant to work with three basic functions. First, we
create a template table. It can be created as a `data.frame` and being
populated in R.

``` r

library(CRediTas)

cras_table <- template_create(authors = c("Friedrich Ratzel", 
                                          "Pau Vidal de la Blache", 
                                          "Élisée Reclus"))
knitr::kable(cras_table)
```

| Authors | Conceptualization | Methodology | Software | Validation | Formal analysis | Investigation | Resources | Data curation | Writing - original draft | Writing - review & editing | Visualization | Supervision | Project administration | Funding acquisition |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Friedrich Ratzel | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Pau Vidal de la Blache | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Élisée Reclus | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

As you can see, the table is empty. So you must provide the information
of who did what. To do this, you can use the `fix` function to edit
directly in R:

``` r


fix(cras_table)
```

Alternatively, you can write the template as a csv file and then
populate it in your preferred csv editor.

``` r


template_create(authors = c("Friedrich Ratzel", 
                                          "Pau Vidal de la Blache", 
                                          "Élisée Reclus"),
                            file = path_to_your_csv_file)
```

Additionally, you can also define the roles to be included in the
template. If `roles` is no specified, the roles recommended by the
CRediT system are all included:

``` r


cras_got <- template_create(authors = c("Danaerys Targaryen", "Kingslayer", "John Snow"),
                roles = c("Free slaves", "Kill white walkers", "Ride dragons"))

# add contribution roles
cras_got[-2, -1] <- 1

knitr::kable(cras_got)
```

| Authors            | Free slaves | Kill white walkers | Ride dragons |
|:-------------------|------------:|-------------------:|-------------:|
| Danaerys Targaryen |           1 |                  1 |            1 |
| Kingslayer         |           0 |                  0 |            0 |
| John Snow          |           1 |                  1 |            1 |

### Read a template

If you wrote the template to a file, then you can read it back to R as
follows:

``` r


cras_table <- template_read(path_to_your_csv_file)
```

### Generate the CRediT author statement

Once the `cras_table` is populated, for instance:

| Authors | Conceptualization | Methodology | Software | Validation | Formal analysis | Investigation | Resources | Data curation | Writing - original draft | Writing - review & editing | Visualization | Supervision | Project administration | Funding acquisition |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Friedrich Ratzel | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 0 |
| Pau Vidal de la Blache | 1 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 1 |
| Élisée Reclus | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |

A text file can be generated following the CRediT author statement
format.

``` r


textfile <- tempfile()

cras_write(cras_table, textfile, markdown = TRUE)
```

If you open the text file, you will find this:

**Friedrich Ratzel:** Validation, Data curation, Writing - original
draft, Supervision, Project administration. **Pau Vidal de la Blache:**
Conceptualization, Validation, Resources, Data curation, Writing -
original draft, Writing - review & editing, Project administration,
Funding acquisition. **Élisée Reclus:** Conceptualization, Software,
Writing - review & editing.

Moreover, if you are writing your paper in RMarkdown or quarto, you can
insert the CRediT author statement directly in the text using an inline
chunk `` `r cras_write(cras_table, markdown = TRUE)` ``.

#### Do not drop authors without contributions

In some cases, one or several authors did not contribute to any specific
role. The `drop` arguments determines if they must be removed from the
statement. If `drop = TRUE` (default), the authors are removed.
Otherwise, they are kept without contributions as below.

``` r


cras_write(cras_got, drop = FALSE, markdown = TRUE)
```

**Danaerys Targaryen:** Free slaves, Kill white walkers, Ride dragons.
**Kingslayer** . **John Snow:** Free slaves, Kill white walkers, Ride
dragons.
