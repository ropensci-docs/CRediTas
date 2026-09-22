# Read a template from a csv file

The template should be created using `create_template()`

## Usage

``` r
template_read(file)
```

## Arguments

- file:

  A character vector with the path to the csv file

## Value

a data.frame with the content of the csv file

## Examples

``` r
# Create a temporary file for this example
file <- tempfile()

# Create a template and save it to a csv file
template_create(authors = c("Josep Maria", "Jane Doe"), file = file)

# Read the template back (in real life once it has been populated)
template_read(file)
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
