# How to HMDA — NICAR 2026

A hands-on workshop notebook for finding DSCR (Debt Service Coverage Ratio) investor loans in public HMDA mortgage data, presented at NICAR 2026.

---

## About the data

**HMDA** (Home Mortgage Disclosure Act) is a federal law requiring most home mortgage lenders to publicly disclose detailed information about individual loan applications. The data covers loan type, amount, applicant characteristics, and geography down to the census tract level.

**DSCR loans** are a non-QM investor mortgage product approved on projected rental income rather than borrower income. This notebook walks through how to identify them in HMDA data and analyze their geographic distribution.

---

## Prerequisites

### Software

- **R** ≥ 4.1 (required for native pipe `|>` and lambda `\(x)` syntax)
- **RStudio** (recommended) or another IDE with Quarto support)

### R packages

```r
install.packages(c(
  "tidyverse", "janitor", "vroom", "sf",
  "leafsync", "tidycensus", "mapview",
  "httr2", "purrr", "RColorBrewer"
))
```

### Census API key (Chapter 2 only)

Chapter 2 pulls tract-level ACS data via `tidycensus`. You'll need a free Census API key:

1. Request one at <https://api.census.gov/data/key_signup.html>
2. Activate it via the link in your email
3. Load in the `tidycensus` package: `library(tidycensus)`
3. Register your api key in R: `census_api_key("YOUR_KEY", install = TRUE)`

---

## Data files

These are the two files in `data/raw/` that this notebook depends on.

| File | Description |
|------|-------------|
| `hmda_18_24_cln.csv.zip` | Pre-processed HMDA data 2018–2024, filtered to first-lien originated loans on 1–4 unit investment property (closed-end). This is the starting point for the class to avoid long load times. |
| `msa_omb.csv` | OMB core-based statistical area delineation file from the Census Bureau, used to map MSA/MD codes to human-readable names. Skip the first 2 rows on read. |

For anyone wanting to start from scratch with raw HMDA files, download them from the [CFPB HMDA Data Browser](https://ffiec.cfpb.gov/data-browser/data/2024?category=states).

---

## Project structure

```
analysis/
  finding_dscr_loans_in_hmda_data.qmd   # main notebook
data/
  raw/       # input files 
  
nicar_2026_how_to_hmda.Rproj
```

---
## License

Copyright 2025, The Venetoulis Institute for Local Journalism

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

Redistributions of source code must retain the above copyright notice, this list of conditions, and the following disclaimer.
Redistributions in binary form must reproduce the above copyright notice, this list of conditions, and the following disclaimer in the documentation and/or other materials provided with the distribution.
Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

---

## Contact

**Sahana Jayaraman**
Data reporter, The Baltimore Banner
sahana.jayaraman@thebanner.com
