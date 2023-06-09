# qcew

A package for retrieving Quarterly Census of Employment and Wages ([QCEW](https://www.bls.gov/cew/)) data from the Bureau of Labor Statistics' [database](https://www.bls.gov/cew/downloadable-data-files.htm).

## Requirements
- Python ≥ 3.8

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install qcew.

```bash
pip install qcew
```

## Usage

```python
import qcew

# Get the entire quarterly census of employment and wages database for 2020.
data = qcew.get_qcew_data(
    year="2020",
    annual=False,
    fields=None
)

# Get annual average employment and pay data for the United States from 2001 to 2021.
data = qcew.get_qcew_data_slice(
    slice_type="area",
    qcew_codes=["US000"],
    years=[str(i) for i in range(2001, 2022)],
    annual_data=True,
    fields=[
        "area_fips",
        "own_code",
        "industry_code",
        "year",
        "disclosure_code",
        "annual_avg_emplvl",
        "avg_annual_pay"
        ]
    )

# Get monthly employment data for the state of Hawaii as well as Honolulu County, HI in 2020.
data = qcew.get_qcew_data_slice(
    slice_type="area",
    qcew_codes=[
        "15000", # Hawaii -- Statewide
        "15003", # Honolulu County, HI
        ],
    years=["2020"],
    annual_data=False,
    fields=[
        "area_fips",
        "own_code",
        "industry_code",
        "year",
        "qtr",
        "disclosure_code",
        "month1_emplvl",
        "month2_emplvl",
        "month3_emplvl"
        ]
    )

# Get annual average employment and pay data for the manufacturing sector as a whole from 2010 to 2020.
data = qcew.get_qcew_data_slice(
    slice_type="industry",
    qcew_codes=[
        "31-33", # NAICS code for manufacturing sector.
        ],
    years=[str(i) for i in range(2010, 2021)],
    annual_data=True,
    fields=[
        "area_fips",
        "own_code",
        "industry_code",
        "year",
        "disclosure_code",
        "annual_avg_emplvl",
        "avg_annual_pay"
        ]
    )

# Get monthly employment data for establishments with fewer than 5 employees in the first quarter of 2021.
data = qcew.get_qcew_data_slice(
    slice_type="size",
    qcew_codes=[
        "1", # Size code for establishments with fewer than 5 employees.
        ],
    years=["2021"],
    annual_data=False,
    fields=[
        "area_fips",
        "own_code",
        "industry_code",
        "size_code",
        "year",
        "qtr",
        "disclosure_code",
        "month1_emplvl",
        "month2_emplvl",
        "month3_emplvl"
        ]
    )
```

## License
Distributed under the MIT license. See [LICENSE](/LICENSE) for more information.
