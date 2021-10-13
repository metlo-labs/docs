---
description: >-
  Metlo's Python SDK makes it very easy to pull metrics in any Python
  application, including Jupyter Notebooks.
---

# Installing Python

Metlo's Python SDK can be installed via pip from PyPI.

```
$ pip install metlo
```

After installing the SDK you need to provide the following information:

1. **API Key** - A key is used to authenticate with Metlo. Generate a new API Key in the Settings tab in Metlo's Web UI.
2. **Metlo Host** - The domain your instance of Metlo is deployed to (i.e. `yourcompany.metlo.com`)

Make a file at `~/.metlo/credentials` with the necessary credentials:

```bash
METLO_API_KEY="<YOUR_API_KEY>"
METLO_HOST="http://yourcompany.metlo.com"
```

Alternatively you can run the following command to have Metlo setup your credentials for you:

```
$ metlo setup
Enter your API Key: ***********
Enter your Metlo Host: yourcompany.metlo.com
```

Note: You can also set `METLO_API_KEY`  and `METLO_HOST` as environment variables. This may be useful in a production environment.
