# deJUNKER

deJUNKER is an R package for variance decomposition using conditional variational auto-encoders. 

## Function `decompose.var`
`decompose.var` is a function that decomposes input contrasts to decoded and residual fractions according to a trained contrast encoder-decoder.

Input:
- `M`: a matrix of raw gene counts
- `MD`: a matrix of gene deltas with the same dimensions as `M`
- `treatm`: vector indicating column indices in `M` corresponding to treatments
- `cntr`: vector indicating column indices in `M` corresponding to controls
- `process_input`: if `TRUE` (default), the count matrix will be preprocessed (library normalized, log-transformed, NA values will be set to 0)
- `organism`: organism of interest (default: Human)
-  `feature_type:` Set to AUTO for automatic feature id-type detection. Alternatively specify the type of supplied id features.
Output: a summarized experiment with the decomposed contrasts in the assays slots and the decomposed variance as colData.

Example 1: 

`RES <- decompose.var(M = ContextM, MD = DeltaM, process_input = FALSE)`

Example 2: 

`RES <- decompose.var(M = CountM, treatm = c(3,4,5,6), cntr = c(1,1,2,2), process_input = FALSE)`

## Function `query.with.contrasts`

`query.with.contrasts` is a function that queries the contrast database with a set of contrasts.

Input: 
- `CONTRASTS`: a summarized experiment with assays containing contrasts named INPUT_CONTRASTS, DECODED_CONTRASTS and RESIDUAL_CONTRASTS (at least one should be present)
- `use`: determines if all genes or genes expressed in both query and target context will be used
- `expr.thr`: quantile in the provided context that determines the expression value above which a gene is considered to be expressed. 
 This same value is then used for thresholding the contrast database (only applies when `use` is set to `expressed.in.both`). 
- `organism`: organism of interest (default: Human)
- `preserve.in.GlobalEnv`: whether the contrast database (stored as a SExp in `target.contrasts`) should be preserved in the GlobalEnv
- `plot.contrast`: which of the contrasts should be plotted (relative to the query contrast)
- `detail.topn`: number of top hits for which metadata will be returned in the TopHits slot of the results

Output: a list of PearsonRhos, Zscores against the database as well as detailed Metadata for the `detail.topn` hits.

Example: 

`RESULT <- query.with.contrasts(CONTRASTS=RES)`

## Installation

deJUNKER can be installed from GitHub using:

```
devtools::install_github("path/to/deJUNKER")
```









