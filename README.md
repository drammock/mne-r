
# MNE-R fast acccess to MNE-Python from within R

<img src="man/figures/mne_logo.png" align="right" alt="" width="160" />

The [MNE-Python](https://mne-tools.github.io/stable/index.html) project
provides a full tool stack for processing and visualizing
electrophysiology data. That is, electroencephalography (EEG),
magnetoencephalography but also intracranial EEG. MNE-R facilitates
integrating this mature and extensive functionality into R-based data
processing, visualization and statisticasl modeling. This is made
possible through the
[reticulate](https://rstudio.github.io/reticulate/), which enables
seamless integration of Python into R.

Currently, MNE-R is mainly focussing on documenting how to use
MNE-Python through R, based on familiar
[MNE-examples](https://mne-tools.github.io/stable/auto_examples/index.html)
while also showcasing what R can add to the game in terms of statistics
and visualization functionality.

In the future, more R-functions may be added that facilitate the
interaction with MNE-Python or implement complementary functionality.

The project is open to contributions.

## Getting Started

In order to use MNE-R, MNE-Python has to be installed with all its
dependencies. Some configuration may be needed to make sure `reticulate`
knows which Python installation to use. Please consider the
[reticulate](https://rstudio.github.io/reticulate/articles/calling_python.html)
and the [MNE](https://mne-tools.github.io/stable/getting_started.html)
documentation. We generally recommend using the
[Anaconda](https://www.anaconda.com) Python distribution and Python 3
instead of Python 2.

For seamlessly combining R and Python code in one Rmarkdown script,
currently [Rstudio 1.2
preview](https://blog.rstudio.com/2018/10/09/rstudio-1-2-preview-reticulated-python/)
is needed.

Currently, mnr-r can be installed from github.

``` r
devtools::install_github("mne-tools/mne-r")
```

To get started, simply laod the mne library

``` r
library(mne)  # load mne and get the mne object
#> Importing MNE version=0.18.dev0, path='/Users/dengeman/github/mne-python/mne'

print(names(mne)[1:10])  # the mne object wraps the loaded mne module inside Python
#>  [1] "AcqParserFIF"               "add_reference_channels"    
#>  [3] "add_source_space_distances" "annotations"               
#>  [5] "Annotations"                "apply_forward"             
#>  [7] "apply_forward_raw"          "average_forward_solutions" 
#>  [9] "BaseEpochs"                 "baseline"

# use dollar signs to access MNE modules, functions and objects
cat(mne$datasets$sample$data_path$`__doc__`)
#> Get path to local copy of sample dataset.
#> 
#>     Parameters
#>     ----------
#>     path : None | str
#>         Location of where to look for the sample dataset.
#>         If None, the environment variable or config parameter
#>         ``MNE_DATASETS_SAMPLE_PATH`` is used. If it doesn't exist, the
#>         "~/mne_data" directory is used. If the sample dataset
#>         is not found under the given path, the data
#>         will be automatically downloaded to the specified folder.
#>     force_update : bool
#>         Force update of the sample dataset even if a local copy exists.
#>     update_path : bool | None
#>         If True, set the ``MNE_DATASETS_SAMPLE_PATH`` in mne-python
#>         config to the given path. If None, the user is prompted.
#>     download : bool
#>         If False and the sample dataset has not been downloaded yet,
#>         it will not be downloaded and the path will be returned as
#>         '' (empty string). This is mostly used for debugging purposes
#>         and can be safely ignored by most users.
#>     
#>     verbose : bool, str, int, or None
#>         If not None, override default verbose level (see :func:`mne.verbose`
#>         and :ref:`Logging documentation <tut_logging>` for more).
#> 
#>     Returns
#>     -------
#>     path : str
#>         Path to sample dataset directory.
```

## Known issues

Currently, when making matplotlib figures from within R, the resulting
image will not be rendered inside Rstudio. You will need to save the
figure or explicitly write Python code in a Python chunk.
