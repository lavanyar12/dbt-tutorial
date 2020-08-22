Welcome to your new dbt project!

### Using the starter project

Try running the following commands:
- dbt run
- dbt test


### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](http://slack.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices

Useful commands

https://docs.getdbt.com/reference/model-selection-syntax/

dbt run --models my_dbt_project_name   # runs all models in your project
dbt run --models my_dbt_model          # runs a specific model
dbt run --models path.to.my.models     # runs all models in a specific directory
dbt run --models my_package.some_model # run a specific model in a specific package
dbt run --models tag:nightly           # run models with the "nightly" tag
dbt run --models path/to/models        # run models contained in path/to/models
dbt run --models path/to/my_model.sql  # run a specific model by its path

# multiple arguments can be provided to --models
dbt run --models my_first_model my_second_model

# these arguments can be projects, models, directory paths, tags, or sources
dbt run --models tag:nightly my_model finance.base.*


Run schema tests only#
$ dbt test --schema
Run data tests only#
$ dbt test --data
Run tests on a particular model#
# syntax
$ dbt test --models model_name
# example
$ dbt test --models customers
Run tests on models#
These should feel somewhat familiar if you're used to executing dbt run with the --models option to build parts of your DAG.

Check out the more in-depth examples of the model selection syntax above for more details:

# Run tests on a model
$ dbt test --models customers

# Run tests on all models in the models/staging/jaffle_shop directory
$ dbt test --models staging.jaffle_shop

# Run tests downstream of a model
$ dbt tests --models stg_customers+

# Run tests upstream of a model
$ dbt tests --models +stg_customers

# Run tests on all models with a particular tag
$ dbt test --models tag:my_model_tag

Run tests on all sources#
$ dbt test --models source:*
Run tests on one source#
# syntax
$ dbt test --models source:<source_name>
# example
$ dbt test --models source:jaffle_shop
Run tests on one source table#
# syntax
$ dbt test --models source:<source_name>.<table_name>
# example
$ dbt test --models source:jaffle_shop.customers
Run tests on everything but sources#
$ dbt test --exclude sources:*
Run tests on seeds / snapshots only#
Currently it is not possible to:

Run tests on all seeds, OR
Run tests on all snapshots
Instead, you will have to provide the name of the resource as the argument to the --models option:

$ dbt test --models orders_snapshot
Run tests on tagged columns#
models/<filename>.yml
version: 2

models:
  - name: orders
    columns:
      - name: order_id
        tests:
        tags: [my_column_tag]
          - unique

$ dbt test --models tag:my_column_tag
Run tagged tests only#
models/<filename>.yml
version: 2

models:
  - name: orders
    columns:
      - name: order_id
        tests:
          - unique:
              tags: [my_test_tag]

$ dbt test --models tag:my_test_tag


$ dbt docs generate
[dbt CLI only] Execute dbt docs generate to generate the documentation for your project. dbt introspects your project and your warehouse to generate a json file with rich documentation about your project.

$ dbt docs serve
[dbt CLI only] Execute dbt docs serve to launch the documentation in a local website.
