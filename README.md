# Rupesh Patel's personal website

This is my personal Quarto website for UBC MDS DSCI 521.
It includes my background, a post about my first weeks in MDS,
and two computational posts using Python and R.

Website: https://datasci201195.github.io

Repository: https://github.com/datasci201195/datasci201195.github.io

## Software requirements

Install these tools before building the website:

| Tool | Version used |
|---|---|
| Quarto CLI | 1.10.18 |
| uv | 0.12.5 |
| R | 4.6.1 |
| Python | 3.14 |

Git is also required to clone the repository.

Installation instructions:

- [Quarto CLI](https://quarto.org/docs/get-started/)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- [R](https://cran.r-project.org/)
- [Git](https://git-scm.com/downloads)

Make sure `git`, `quarto`, `uv`, and `Rscript` are available in
your terminal.

Python is selected using `.python-version`. During environment setup,
uv can download Python 3.14 if it is not already available.

R must be installed separately. The committed renv startup files
automatically bootstrap renv when R starts in the repository.

## Build the website

Run the following commands in a terminal. Start in a folder where
you want to create a new copy of the repository.

### 1. Clone the repository

```bash
git clone https://github.com/datasci201195/datasci201195.github.io.git
cd datasci201195.github.io
```

Run all remaining build commands from this repository's root folder,
where `_quarto.yml` is located.

### 2. Restore the Python environment

```bash
uv sync --locked
```

This creates the local `.venv` environment and installs the package
versions recorded in `uv.lock`. The `--locked` option checks that
the lockfile matches the project requirements without updating it.

### 3. Restore the R environment

```bash
Rscript -e "renv::restore(prompt = FALSE)"
```

This runs R code from the terminal and installs the package versions
recorded in `renv.lock`.

Starting R from the repository root allows `.Rprofile` to activate
the project's R environment.

### 4. Render the website

```bash
uv run quarto render
```

This executes the computational posts and builds the website.
Using `uv run` makes the project's Python environment available
to Quarto.

The generated website is saved in `docs/`, as configured in
`_quarto.yml`.

## Open the website locally

After rendering, open `docs/index.html` in a browser.

On macOS, run:

```bash
open docs/index.html
```

For a local preview server, run this from the repository root:

```bash
uv run quarto preview
```

Open the local address printed in the terminal if the browser does
not open automatically. Press Ctrl+C in the terminal to stop the
preview server.

## Computational posts

### Python: Penguin body mass

File: `posts/penguins-python/index.qmd`

This post compares average body mass across Adelie, Chinstrap,
and Gentoo penguins. It checks missing values, summarizes the data,
and generates a bar chart.

Data: [Palmer Penguins](https://allisonhorst.github.io/palmerpenguins/).

The data was collected by Dr. Kristen Gorman and Palmer Station
Antarctica LTER and is available under a CC0 licence.

The dataset is included in the Python `palmerpenguins` package
and loaded using `load_penguins()`.

### R: Car weight and fuel efficiency

File: `posts/mtcars-r/index.qmd`

This post explores the relationship between car weight and fuel
efficiency. It compares average MPG by cylinder group, generates
a scatter plot, and calculates a correlation.

Data: [Motor Trend Car Road Tests](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html).

The `mtcars` dataset is included with R and contains 32 cars from
the 1973–74 model years.

### Network requirements

Internet access is needed to clone the repository and download
Python, renv, and required packages during initial setup.

Once the environments are installed, neither post needs an internet
connection to fetch its dataset. Both datasets are available locally
through their installed packages.

## Environment files

The Python environment is defined by:

- `pyproject.toml`
- `uv.lock`
- `.python-version`

The R environment is defined by:

- `renv.lock`
- `.Rprofile`
- `renv/activate.R`
- `renv/settings.json`

Installed environment folders such as `.venv/` and `renv/library/`
are excluded from Git.

## Publishing

GitHub Pages serves the rendered website from the `docs/` folder.
After changing the source files, render again and commit the updated
website output before pushing to GitHub.