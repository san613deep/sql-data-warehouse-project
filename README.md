# SQL Server Data Warehouse & Analytics

A SQL Server data-warehouse project that integrates CRM and ERP source files, loads a Bronze layer, cleans and standardizes data in Silver, and builds a Gold dimensional model for analytical queries.

## Architecture

```text
CRM CSV files       ERP CSV files
     |                   |
     +---------+---------+
               |
               v
       BRONZE (raw landing)
               |
               v
       SILVER (cleaned / standardized)
               |
               v
       GOLD (dimensions + fact_sales)
               |
               v
       Analytical SQL queries
```

The project uses a medallion-style architecture and SQL Server stored procedures for the Bronze and Silver load processes. Gold tables are designed for reporting and dimensional analysis.

## Technology

- Microsoft SQL Server
- SQL Server Management Studio (SSMS)
- T-SQL stored procedures and views
- CSV source datasets
- Git / GitHub

## Repository layout

```text
datasets/
  source_crm/
  source_erp/
scripts/
  init_database.sql
  bronze/
    ddl_bronze.sql
    proc_load_bronze.sql
  silver/
    ddl_silver.sql
    proc_load_silver.sql
  gold/
    ddl_gold.sql
tests/
  quality_checks_silver.sql
  quality_checks_gold.sql
README.md
```

## Prerequisites

- SQL Server 2019 or later (SQL Server Express is suitable for local learning).
- SQL Server Management Studio.
- Permission for the SQL Server service account to read the CSV files.
- The repository datasets downloaded to a local directory.

## Setup and execution

### 1. Clone the repository

```powershell
git clone https://github.com/san613deep/sql-data-warehouse-project.git
cd sql-data-warehouse-project
```

### 2. Initialize the database

Open `scripts/init_database.sql` in SSMS and execute it against your SQL Server instance.

### 3. Create the Bronze schema tables

Execute `scripts/bronze/ddl_bronze.sql`.

### 4. Configure the source data path

The Bronze load procedure uses the SQLCMD variable `$(DataRoot)` instead of a developer-specific Windows path.

In SSMS:
1. Open `scripts/bronze/proc_load_bronze.sql`.
2. Enable **Query → SQLCMD Mode**.
3. Add or execute the following SQLCMD setting after replacing the path with your local repository directory:

```sql
:setvar DataRoot "C:\\path\\to\\sql-data-warehouse-project"
```

The folder should contain the `datasets/` directory. The SQL Server Database Engine service account must have read access to those CSV files; access from your Windows user account alone is not sufficient.

Execute the Bronze procedure script to create `bronze.load_bronze`, then run:

```sql
EXEC bronze.load_bronze;
```

Alternatively, run the script with `sqlcmd` and pass `-v DataRoot="C:\\path\\to\\sql-data-warehouse-project"`.

### 5. Create and load the Silver layer

Execute the following in order:

1. `scripts/silver/ddl_silver.sql`
2. `scripts/silver/proc_load_silver.sql`

Then run:

```sql
EXEC silver.load_silver;
```

### 6. Create the Gold layer

Execute `scripts/gold/ddl_gold.sql` to create the dimensional model.

### 7. Run data-quality checks

After the loads, execute:

- `tests/quality_checks_silver.sql`
- `tests/quality_checks_gold.sql`

The scripts contain diagnostic queries. For checks documented as “Expectation: No Results”, investigate any returned rows before relying on the warehouse for reporting. Some standardization queries intentionally return distinct values for manual review rather than asserting zero rows.

## Data model

The Gold layer contains customer and product dimensions and a sales fact table. The fact table links to dimensions using surrogate keys, enabling customer, product and sales analysis.

## Example analytical questions

- Which products and categories contribute the most sales?
- How does revenue vary by customer and product?
- Which customers have the highest purchase activity?
- Are fact rows missing valid dimension references?

## Important implementation notes

- The Bronze procedure truncates and reloads its target tables. Treat it as a batch reload, not an incremental CDC pipeline.
- SQL Server reads files from the database server's filesystem context. The configured path must be accessible to the SQL Server service account.
- The SQL quality-check scripts are manually executed diagnostic queries; they are not an automated CI test suite.
- This is a portfolio and learning implementation. Validate schema changes and row-level results on a disposable database before re-running scripts against important data.

## Future improvements

- Add a repeatable local SQL Server container or documented SQL Server Developer setup.
- Convert diagnostic queries into automated assertions that fail on unexpected rows.
- Add row-count reconciliation between Bronze, Silver and Gold.
- Add incremental load support and audit metadata.
- Add Power BI dashboards with screenshots and documented measures.

## License

See the repository `LICENSE` file for reuse terms.
