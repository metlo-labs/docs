---
description: All available Data Quality checks
---

# Available Quality Checks

Currently available quality checks are:&#x20;

| Check Name         | Param Name      | Type    | Required               |
| ------------------ | --------------- | ------- | ---------------------- |
| cardinality        | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| average            | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| count              | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| duplicate\_percent | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| max                | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| num\_nulls         | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| min                | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| pct\_nulls         | column          | SQL     | True                   |
|                    | lower\_bound    | float   | True                   |
|                    | upper\_bound    | float   | True                   |
| is\_uuid           | column          | SQL     | True                   |
| regex              | column          | SQL     | True                   |
|                    | pattern         | string  | True                   |
|                    | case\_sensitive | boolean | False (default : True) |
