# Write CRediT author statement

The function transforms the information in the template (from
`template_create`) to a raw string following the CRediT authors
statement format of "author1: contributions author2: contributions ..."

## Usage

``` r
cras_write(
  cras_table,
  file,
  drop_authors = TRUE,
  overwrite = FALSE,
  markdown = TRUE,
  quiet = FALSE
)
```

## Arguments

- cras_table:

  A data.frame created using `create_template()`

- file:

  The text file to be created. If not provided (default), the statement
  is returned as a string instead of written to a file.

- drop_authors:

  If TRUE (default) the authors without contributions are removed from
  the statement. If FALSE, they are kept without contributions assigned.

- overwrite:

  If TRUE, the file is overwritten. Otherwise, a error is triggered.

- markdown:

  If TRUE (default), the authors are surrounded by \*\* to make them
  bold in markdown.

- quiet:

  If TRUE and `drop_authors` is also TRUE, authors without contributions
  are silently dropped out. If FALSE, a warning is triggered in case any
  authors is dropped out.

## Value

A text file with the CRediT authors statement or, if file is NULL
(default), a character vector of length 1 with the statement that can be
used in a Rmarkdown or quarto document using inline code:
`` `r cras_write(cras_table, markdown = TRUE)` ``

## Examples

``` r
# Generate a template and populate it (randomwly for this example)
cras_table <- template_create(authors = c("Josep Maria", "Jane Doe"))
cras_table[,2:ncol(cras_table)] <- sample(0:1, (ncol(cras_table)-1)*2,
                                          replace = TRUE)

# Create a temporary file just for this example
file <- tempfile()

# Write to the file
cras_write(cras_table, file, markdown = TRUE)

# Check the content of the file
readLines(file)
#> [1] "**Josep Maria:** Methodology, Investigation, Writing - review & editing, Supervision, Funding acquisition. **Jane Doe:** Software, Formal analysis, Data curation, Writing - review & editing."
```
