# Create a template to fill the CRediT author statement.

Create a template to fill the CRediT author statement.
(<https://credit.niso.org>). The template is a table where the authors
are the rows and the columns are the roles.

## Usage

``` r
template_create(authors, file, roles = roles_get())
```

## Arguments

- authors:

  A character vector with all the authors to be included in the
  statement.

- file:

  If a path is provided, the template is saved as a csv for excel

- roles:

  A character vector with the roles to be included in the statement. If
  NULL, it uses all the roles defined in the CRediT author statement.

## Value

A dataframe with a row for each author and a column for each role,
filled with zeros.

## Details

The dataframe can be edited in R or, if file is provided, it is exported
to a csv to be edited manually in your preferred csv editor. The csv is
created to be compatible with Microsoft Excel, since it is the most
popular spreadsheet software among scientists. Therefore, it is
separated by semicolon.

## Examples

``` r
template_create(authors = c("Josep Maria", "Jane Doe"))
#>       Authors Conceptualization Methodology Software Validation Formal analysis
#> 1 Josep Maria                 0           0        0          0               0
#> 2    Jane Doe                 0           0        0          0               0
#>   Investigation Resources Data curation Writing - original draft
#> 1             0         0             0                        0
#> 2             0         0             0                        0
#>   Writing - review & editing Visualization Supervision Project administration
#> 1                          0             0           0                      0
#> 2                          0             0           0                      0
#>   Funding acquisition
#> 1                   0
#> 2                   0
```
