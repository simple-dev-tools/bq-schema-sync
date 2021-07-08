# bq-schema-sync
A CLI to manage BigQuery schema as code

This is a tool used for CI/CD process to ensure the BigQuery table/view definition exact
same as the required. Once there is a change to the table, eg. adding a new column, the
developers need to update the declaration file in the repo, and run the CI/CD process to
promote changes to BigQuery.

Since the table schema change are much more complicate than adding a column, so this tool
is not designed for significant update of the schema. 

## Key Features

- Create brand new `Dataset`, `Table` and `Veiw` in BigQuery based on declaration files.
- Identify the difference of existing schema and update them by using latest declaration files.
- Force re-create BigQuery objects (drop and create a table)


## How it look like?

```bash
# init a new project, create a bss_schema_infomation dataset to keep the state
bsscli init --project your-project-id

# if table1 is not exist, create it, otherwise compare if the existing table1 has
# the latest signiture of `table1.yaml`
bsscli --project your-project-id --file table1.yaml 

# drop table1 and recreate it anyway
bsscli --project your-project-id --file table1.yaml --force

# check if table1 is up-to-date
bsscli --project your-project-id --file table1.yaml  --check
```