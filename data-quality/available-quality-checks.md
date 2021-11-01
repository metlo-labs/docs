---
description: All available Data Quality checks
---

# Available Quality Checks

Currently available quality checks are:&#x20;

| Check Name         | Param Name      | Type    | Required               |
| ------------------ | --------------- | ------- | ---------------------- |
| Cardinality        | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Average            | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Count              | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Duplicate\_percent | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Max                | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Num\_nulls         | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Min                | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Pct\_nulls         | column          | SQL     | True                   |
|                    | lower\_count    | float   | True                   |
|                    | upper\_count    | float   | True                   |
| Is\_uuid           | column          | SQL     | True                   |
| Regex              | column          | SQL     | True                   |
|                    | pattern         | string  | True                   |
|                    | case\_sensitive | boolean | False (default : True) |
