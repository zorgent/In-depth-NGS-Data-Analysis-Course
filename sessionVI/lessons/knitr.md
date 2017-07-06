Introduction to knitr
================

[knitr](https://yihui.name/knitr/), developed by [Yihui Xie](https://yihui.name), is an R package designed for report generation within [RStudio](https://www.rstudio.com). It enables dynamic generation of multiple file formats from an [RMarkdown](http://rmarkdown.rstudio.com/) file, including HTML and PDF documents.

As RMarkdown grows as an acceptable [reproducible manuscript](https://elifesciences.org/labs/cad57bcf/composing-reproducible-manuscripts-using-r-markdown) format, using [knitr](https://yihui.name/knitr/) to generate a report summary is becoming common practice.

Document creation is now integrated into [RStudio](https://www.rstudio.com), and can be accessed using the GUI (show image of knit button) or two command line options:

chunks
======

In RMarkdown, programming chunks are defined by three backticks ("\`\`\`") then then programming language, followed by a *unique* chunk label, and customization options.

Code languages
--------------

Recently [RStudio](https://www.rstudio.com) has added support for additional [code languages](http://rmarkdown.rstudio.com/lesson-5.html) besides R inside code including bash and python:

-   Python
-   SQL
-   Bash
-   Rcpp
-   Stan
-   JavaScript
-   CSS

This is still in development but allows for integration of multiple programming languages into a single workflow, and is shaping up to be a very powerful tool for NGS analysis in the future.

Global options
--------------

``` r
library(knitr)
opts_chunk$set(
    autodep = TRUE,
    cache = TRUE,
    cache.lazy = TRUE,
    dev = c("png", "pdf", "svg"),
    error = TRUE,
    fig.height = 6,
    fig.retina = 2,
    fig.width = 6,
    highlight = TRUE,
    message = FALSE,
    prompt = TRUE,
    tidy = TRUE,
    warning = FALSE)
```

Per chunk options
-----------------

Walk through some examples of useful per chunk options:

-   `echo = FALSE`
-   `eval = FALSE`
-   `include = FALSE`
-   `message = FALSE`
-   `results = "asis"`
-   `warning = FALSE`

Resize an image:

-   `fig.height = 6`
-   `fig.width = 4`

`setup` chunk
=============

The `setup` chunk is a special knitr chunk that should be placed at the start of the document. We recommend storing all `library()` loads required for the script and other `load()`/`data()` requests for external files here. In our RMarkdown templates, such as the bcbioRnaseq [differential expression template](https://github.com/hbc/bcbioRnaseq/blob/master/inst/rmarkdown/templates/differential_expression/skeleton/skeleton.Rmd), we store all the user-defined parameters in the `setup` chunk that are required for successful knitting.

> {r setup, include=FALSE} knitr::opts\_chunk$set(echo = TRUE)

knitr::knit
-----------

``` r
help("knit", "knitr")
```

When you `knit()` a document, by default this will generate an HTML report. If you would prefer a different document format, this can be specified in the YAML header with the `output:` parameter.

*refer back to RMarkdown table*

rmarkdown::render
-----------------

``` r
help("render", "rmarkdown")
```

Mention that `render()` allows for output of multiple document formats.

`_output.yaml` file from bcbioRnaseq [link](https://github.com/hbc/bcbioRnaseq/blob/master/docs/downloads/_output.yaml):

    rmarkdown::html_document:
        code_folding: hide
        df_print: kable
        highlight: pygments
        number_sections: false
        toc: true
    rmarkdown::pdf_document:
        number_sections: false
        toc: true
        toc_depth: 1

Note on pandoc? PDF rendering can fail on some systems, may require Homebrew install.

kable
=====

Section about stylized tables using `kable`.

``` r
help("kable", "knitr")
```

Alignment parameters from basejump scripts, previous consults \[need to add\].

Alternatives:

-   xtable
-   pandoc table