# [v1.3.7][1.3.7]
## Bug fixes
- Fix inconsistent behavior of `utf::segmenter` (and thus `icu_tokenizer`) for
    different locales. Thanks @CanoeFZH and @tng-konrad for helping debug
    this!

## Enhancements
- Allow for specifying the language and country for locale generation in
    setting up `utf::segmenter` (and thus `icu_tokenizer`)
- Allow for suppression of `<s>` and `</s>` tags within `icu_tokenizer`,
    mostly useful for information retrieval experiments with unigram words.
    Thanks @husseinhazimeh for the suggestion!
- Add a `default-unigram-chain` filter chain preset which is suitable for
    information retrieval experiments using unigram words. Thanks
    @husseinhazimeh for the suggestion!

# [v1.3.6][1.3.6]
## Bug fixes
- Fix potential off-by-one when calculating the number of documents in a
    `line_corpus` when its files do not end in a newline

## Enhancements
- Change `score_data` to support floating-point weights on query terms

# [v1.3.5][1.3.5]
## Bug fixes
- Fix missing support for sequence/parser analyzers in the classify tools

# [v1.3.4][1.3.4]
## New features
- Support building with biicode
- Add Vagrantfile for virtual machine configuration
- Add Dockerfile for Docker support

## Enhancements
- Improve `ir_eval` unit tests

## Bug fixes
- Fix `ir_eval::ndcg` incorrect log base and addition instead of subtraction in
    IDCG calculation
- Fix `ir_eval::avg_p` incorrect early termination

# [v1.3.3][1.3.3]
## Bug fixes
- Fix issues with system-defined integer widths in binary model files
    (mainly impacted the greedy tagger and parser); please re-download any
    parser model files you may have had before
- Fix bug where parser model directory is not created if a non-standard
    prefix is used (anything other than "parser")

## Enhancements
- Silence inconsistent missing overrides warning on clang >= 3.6

# [v1.3.2][1.3.2]
## Bug fixes
- fix potentially incorrect generation of vocabulary map files on 32-bit
    systems (this appears to have only impacted non-default block sizes)

# [v1.3.1][1.3.1]
## Bug fixes
- fix calculation of average precision in `ir_eval` (the denominator was
    incorrect)
- specify that labels are required for the `file_corpus` document list; this
    allows spaces in the path to each document

# [v1.3][1.3]
## New features
- additions to the graph library:
    * myopic search
    * BFS
    * preferential attachment graph generation model (supports node
        attractiveness from different distributions)
    * betweenness centrality
    * eigenvector centrality
- added a new natural language parsing library:
    * parse tree library (visitor-based)
    * shift-reduce constituency parser for generating phrase structure
        trees
    * reimplementation of evalb metrics for evaluating parsers
    * new filter for Penn Treebank-style normalization
- added a greedy averaged Perceptron-based tagger
- demo application for various basic text processing (profile)
- basic iostreams that support gzip compression (if compiled with ZLib
    support)
- added iteration method for `stats::multinomial` seen events
- added expected value and entropy functions to `stats` namespace
- added `linear_model`: a generic multiclass classifier storage class
- added `gz_corpus`: a compressed version of `line_corpus`
- added macros for generating type safe identifiers with user defined
    literal suffixes
- added a persistent stack data structure to `meta::util`

## Enhancements
- added operator== for `util::optional<T>`
- better CMake support for building the libsvm modules
- better CMake support for downloading unit-test data
- improved setup guide in README (for OS X, Ubuntu, Arch, and EWS/ENGRIT)
- tree analyzers refactored to use the new parser library (removes
    dependency on outside toolkits for generating tree files)
- analyzers that are not part of the "core" have been moved into their
    respective folders (so `ngram_pos_analyzer` is in `src/sequence`,
    `tree_analyzer` is in `src/parser`)
- `make_index` now checks if the files exist before loading an index, and
    if they are missing creates a new one (as opposed to just throwing an
    exception on a nonexistent file)
- cpptoml upgraded to support TOML v0.4.0
- enable extra warnings (-Wextra) for clang++ and g++

## Bug fixes
- fix `sequence_analyzer::analyze() const` when applied to untagged
    sequences (was throwing when it shouldn't)
- ensure that the inverted index object is destroyed first before
    uninverting occurs in the creation of a `forward_idnex`
- fix bug where `icu_tokenizer` would output spaces as tokens
- fix bugs where index objects were not destroyed before trying to delete
    their files in the unit tests
- fix bug in `sparse_vector::find()` where it would return a non-end
    iterator when asked to find an element that does not exist

# [v1.2][1.2]
## New features
- demo application for CRF-based POS tagging
- `nearest_centroid` classifier
- basic statistics library for representing relevant probability
    distributions
- `sparse_vector` utility class

## Enhancements
- `ngram_pos_analyzer` now uses the CRf internally (see issue #46)
- `knn` classifier new supports weighted knn
- `filesystem::copy_file()` no longer hangs without progress reporting with
    large files
- CMake build system now includes `INTERFACE` targets (better inclusion as
    a subproject in external projects)
- MeTA can now (optionally) be built with C++14 support

## Bug fixes
- `language_model_ranker` scoring function corrected (see issue #50)
- `naive_bayes` classifier scoring corrected
- several incorrect instances of `numeric_limits<double>::min()` replaced
    with the intended `numeric_limits<double>::lowest()`
- fix compilation with versions of ICU < 4.4

# [v1.1][1.1]
## Changes
- sequence analyzer and CRF implementation
- basic language model
- basic directed and undirected graphs
- restructure CMakeLists

# [v1.0][1.0]
- Initial release.

[unreleased]: https://github.com/meta-toolkit/meta/compare/v1.3.7...develop
[1.3.7]: https://github.com/meta-toolkit/meta/compare/v1.3.6...v1.3.7
[1.3.6]: https://github.com/meta-toolkit/meta/compare/v1.3.5...v1.3.6
[1.3.5]: https://github.com/meta-toolkit/meta/compare/v1.3.4...v1.3.5
[1.3.4]: https://github.com/meta-toolkit/meta/compare/v1.3.3...v1.3.4
[1.3.3]: https://github.com/meta-toolkit/meta/compare/v1.3.2...v1.3.3
[1.3.2]: https://github.com/meta-toolkit/meta/compare/v1.3.1...v1.3.2
[1.3.1]: https://github.com/meta-toolkit/meta/compare/v1.3...v1.3.1
[1.3]: https://github.com/meta-toolkit/meta/compare/v1.2...v1.3
[1.2]: https://github.com/meta-toolkit/meta/compare/v1.1...v1.2
[1.1]: https://github.com/meta-toolkit/meta/compare/v1.0...v1.1
[1.0]: https://github.com/meta-toolkit/meta/compare/01aff7e0bddfaba997141d96ef7a371b3221e0ee...v1.0
