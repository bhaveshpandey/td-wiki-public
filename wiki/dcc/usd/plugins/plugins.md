# Plugins

This subwiki documents how we can extend USD's functionality by creating custom plugins.

## Registering Custom Metadata to be tracked in USD files

We can embed arbitrary kinds of data inside USD files by extending the SDFMetadata using the **plugInfo.json** file as shown below.

```json

{
    "Plugins":[
        {
            "Name": "metadata_extention_plugin",
            "Type": "resource",
            "Info": {
                "SdfMetadata": {
                    "my_custom_metadata": {
                        "type": "asset",
                        "appliesTo": "layers",
                        "default": ""
                    }
                }
            }
        }
    ]
}

```

This file is placed in a path specified by **PXR_PLUGINPATH_NAME** so DCCs can locate the USD plugins.

```shell

export PXR_PLUGINPATH_NAME=/path/to/directory/containing/plugInfo.json
```

## Resources

* [Adding Custom Metadata to USD items](https://github.com/ColinKennedy/USD-Cookbook/blob/master/references/working_with_plugins.md#Extend-Metadata)
