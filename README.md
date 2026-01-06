# dbt Airbnb Analytics — Berlin

This project analyzes Airbnb listing data for Berlin, Germany using dbt and Snowflake. I built this to demonstrate a full analytics engineering workflow, from raw data ingestion through to a working BI dashboard.

## About the Project

The scenario here is working as an analytics engineer responsible for Airbnb's Berlin data pipeline. The project takes raw listing, review, and host data from Inside Airbnb (their public data sharing site), loads it into Snowflake, and transforms it into clean, tested, documented models ready for analytics.

The pipeline handles:
- Data cleansing and standardization
- Incremental loading for review events
- Slowly changing dimensions for tracking historical changes
- Data quality testing at each layer
- Auto-generated documentation with lineage

## Tech Stack

- **dbt** for transformations
- **Snowflake** as the data warehouse (free trial works fine)
- **Preset** for dashboards (managed Superset)

## Project Structure

```
models/
  staging/           -- clean up raw data
    stg_listings.sql
    stg_reviews.sql
    stg_hosts.sql
  marts/             -- final tables for analytics
    dim_hosts.sql
    dim_listings.sql
    fct_reviews.sql
snapshots/           -- SCD type 2 tracking
tests/               -- custom data tests
macros/              -- reusable SQL
```

## Getting Started

### Prerequisites

You'll need Python 3.8+ and a Snowflake account. Snowflake offers a free trial at signup.snowflake.com which is plenty for this project.

### Install dbt

```bash
pip install dbt-snowflake
```

### Set Up Your Profile

Create a file at `~/.dbt/profiles.yml`:

```yaml
dbt_airbnb:
  target: dev
  outputs:
    dev:
      type: snowflake
      account: your_account
      user: your_username
      password: your_password
      role: TRANSFORM
      database: AIRBNB
      warehouse: COMPUTE_WH
      schema: DEV
      threads: 4
```

### Clone and Run

```bash
git clone https://github.com/yourusername/dbt-airbnb-berlin.git
cd dbt-airbnb-berlin
dbt deps
dbt debug    # verify connection
dbt build    # run models and tests
```

To view the documentation and lineage graph:

```bash
dbt docs generate
dbt docs serve
```

## Screenshots

### Lineage Graph
![DAG](./assets/screenshots/lineage.png)

### Documentation
![Docs](./assets/screenshots/docs.png)

### Snowflake Output
![Snowflake](./assets/screenshots/snowflake.png)

### Dashboard
![Dashboard](./assets/screenshots/dashboard.png)

## Testing

The project includes both generic tests (unique, not_null, accepted_values, relationships) and custom tests for business logic validation. Run them with `dbt test`.

## Data Source

All data comes from [Inside Airbnb](http://insideairbnb.com/), which publishes anonymized Airbnb data for research purposes.

## Resources

- [dbt docs](https://docs.getdbt.com/)
- [Snowflake free trial](https://signup.snowflake.com/)
- [Preset](https://preset.io/)

---

Built by [Your Name](https://github.com/yourusername)
