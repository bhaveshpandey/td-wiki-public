# jsonschema

`jsonschema` provides a functionalities for validating typed `Json` documents.

```python

schema = {
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "title": "Configuration",
    "description": "Configurations for data Ingestion.",
    "type": "object",
    "properties": {
        "globals": {
            "type": "array",
            "items": {"type": "string"},
        },
        "job": {"type": "object"},
        "mount": {"type": "string"},
        "ingest_source_dir": {"type": "string"},
        "parsers": {"type": "object"},
        "formatters": {"type": "object"},
        "classifiers": {"type": "object"},
        "processors": {
            "type": "array",
            "items": {"type": "string"},
        },
    },
    "required": ["parsers", "formatters", "classifiers"],
}
```


## References

* [jsonschema documentation](https://python-jsonschema.readthedocs.io/en/stable/validate/)
