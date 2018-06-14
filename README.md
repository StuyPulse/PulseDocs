# PulseDocs

Documentation for Stuypulse's Software Engineering division

## Usage

Pulsedocs uses MKDocs.

**Prerequisites:**

1) [Ensure MKDocs is installed](http://www.mkdocs.org/#installation)
2) Ensure mkdocs-material is installed with `pip install mkdocs-material`

**Testing**

Test with `mkdocs serve` in the project's root directory

**Building for hosting**

Build with `mkdocs build` in the project's root directory.
Compiled html will be found in the `site/` folder

**Editing**

To add a page, create a markdown file somewhere in `docs/...`
and add an entry to `mkdocs.yml`. `mkdocs.yml` is a YAML file
(YAML is an easy-to-read data format) which determines the
documentation pages to be displayed and their heirarchy.

See https://www.mkdocs.org for details.
