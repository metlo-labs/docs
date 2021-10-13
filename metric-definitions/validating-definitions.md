# Validating Definitions

You can validate the metric definitions you have made using the `metlo` command line tool. Run the validate subcommand like this: `metlo validate -d <definition_directory>`

```bash
$ metlo validate -d metric_definitions
Validating metric_definitions/sales_definition.yaml
PASSED
Validating metric_definitions/events_definition.yaml
PASSED
Validating metric_definitions/covid_definitions.yaml
PASSED
```

If any definition fails validation checks you will see output that looks similar to this:

```bash
$ metlo validate -d metric_definitions
Validating metric_definitions/sales_definition.yaml
PASSED
Validating metric_definitions/events_definition.yaml
PASSED
Validating metric_definitions/covid_definitions.yaml
1 validation error for Definition
metrics -> 0
  __init__() got an unexpected keyword argument 'nam' (type=type_error)
```
