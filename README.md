# Stripe 

This package models Stripe data from [Fivetran's connector](https://fivetran.com/docs/applications/stripe). It uses data in the format described by [this ERD](https://docs.google.com/presentation/d/1DgcGgNNcH8KPiAjaFNkvT6nEpY6hJd6DZ7ux_CdIF8A/edit).

This package enables you to better understand your Stripe transactions. The main focus is to enhance the balance transaction entries with useful fields from related tables. Additionally, the metrics tables allow you to better understand your account activity over time or at a customer level. These time based metrics are available on a daily, weekly, monthly and quarterly level.


### Models
This package contains transformation models, designed to work simultaneously with our [Stripe source package](https://github.com/fivetran/dbt_stripe_source). A depenedency on the source package is declared in this package's packages.yml file, so it will automatically download when you run dbt deps. The primary outputs of this package are described below. Intermediate models are used to create these output models.
| **model**                  | **description**                                                                                                                                               |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| stripe\_balance\_transactions             | Each record represents a change to your account balance, enriched with data about the transaction                                             |
| stripe\_customer\_overview     | Each record represents a customer, enriched with associated data about metrics of it's purchases. |
| stripe\_daily\_overview     | Each record represents a single day, enriched with metrics about balances, payments, refunds, payouts, and other transactions.                              |
| stripe\_weekly\_overview    | Each record represents a single week, enriched with metrics about balances, payments, refunds, payouts, and other transactions.                               |
| stripe\_monthly\_overview   | Each record represents a single month, enriched with metrics about balances, payments, refunds, payouts, and other transactions.                             |
| stripe\_quarterly\_overview | Each record represents a single quarter, enriched with metrics about balances, payments, refunds, payouts, and other transactions.                           |




## Installation Instructions
Check [dbt Hub](https://hub.getdbt.com/) for the latest installation instructions, or [read the docs](https://docs.getdbt.com/docs/package-management) for more information on installing packages.

## Configuration
By default this package will look for your Hubspot data in the `stripe` schema of your [target database](https://docs.getdbt.com/docs/running-a-dbt-project/using-the-command-line-interface/configure-your-profile). If this is not where your Stripe data is, please add the following configuration to your `dbt_project.yml` file:

```yml
# dbt_project.yml

...
config-version: 2

vars:
  stripe_source:
    stripe_database: your_database_name
    stripe_schema: your_schema_name 
```

For additional configurations for the source models, please visit the [Stripe source package](https://github.com/fivetran/dbt_stripe_source).

### Disabling models

When setting up your Stripe connection in Fivetran, it is possible that not every table this package expects will be synced. This can occur because you either don't use that functionality in Stripe or have actively decided to not sync some tables. In order to disable the relevant functionality in the package, you will need to add the relevant variables. By default, all variables are assumed to be `true`. You only need to add variables for the tables you would like to disable:  

```yml
# dbt_project.yml

...
config-version: 2

vars:
  stripe:
    using_subscriptions: false
    using_invoices: false
    using_payment_method: false
```


### Contributions ###

Additional contributions to this package are very welcome! Please create issues
or open PRs against `master`. Check out 
[this post](https://discourse.getdbt.com/t/contributing-to-a-dbt-package/657) 
on the best workflow for contributing to a package.

### Resources:
- Learn more about Fivetran [here](https://fivetran.com/docs)
- Check out [Fivetran's blog](https://fivetran.com/blog)
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](http://slack.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices

