# CITATION.cff `authors` block from GitHub Contributors

Generate a
[CITATION.cff `authors` block](https://github.com/citation-file-format/citation-file-format/blob/main/schema-guide.md#authors)
using the GitHub API `/repos/${owner}/${repo}/contributors` endpoint.

_Only_ outputs an `authors` block; the rest of the file is up to you!


## Dependencies

NodeJS >=22


## Usage

```bash
node cff-authors-from-gh-contributors.js <owner> <repo> [github-token]
```

Review the output, especially `family-names` and `given-names`, for correctness.

The output is sorted by number of contributions.


## Features

* CFF `authors` block printed to stdout, all other messages to stderr.
  You can pipe to a clipboard tool, for example
  `node cff-authors-from-gh-contributors.js | xclip -sel cl`
* Use the GitHub username as `alias`.
* Use the GitHub user profile's "name" field, if present, as `given-names` and
  `family-names` with very naive string parsing.
  **Expect to hand-edit the output a bit**.
  The string is split by spaces, and the last element is used for the `family-names`,
  all other elements are used for `given-names`.
* Use the GitHub user profile's "e-mail" field, if present, as `email`.
* Use the GitHub user profile's "blog" field, if present, as `website`.


## Limitations

* **Excludes non-code contributors**.
  Consider if this is right for your community -- it's probably not.
  [**All contributors deserve to be acknowledged**](https://book.the-turing-way.org/community-handbook/acknowledgement/)!
  This is a quick-and-dirty tool to save time, I don't recommend using it as your only
  process for acknowledging your contributors.
* Only has access to the information users enter in the GitHub interface.
  If they haven't entered their name, we can only show their alias.
