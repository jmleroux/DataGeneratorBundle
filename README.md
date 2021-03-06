DataGeneratorBundle
===================

This bundle generates file data in the native Akeneo CSV format.

It's able to generate products and attributes information (including families and attributes options).

So you need a PIM system with channels, locales and currency already setup.

From that, this bundle will generate valid product and attribute data.

Installation
------------
```bash
 $ composer.phar require akeneo/data-generator-bundle dev-master
```
and update your ``app/AppKernel.php`` as follow:

```php
    $bundles[] = new Pim\Bundle\DataGeneratorBundle\PimDataGeneratorBundle();
```

Legacy version
--------------
If you want to use the previous version (with the command lines and options), please use the 0.1 tag.
Note that the current version covers the same feature than the previous one while adding generation
on attributes and families.

Usage
-----
```bash
Usage:
 pim:generate-data <configuration_file_path>

Arguments:
 configuration-file    YAML configuration file
```

Configuration file examples
---------------------------
Generating attributes and families:

```yaml
data_generator:
    output_dir: /tmp/generated_data
    entities:
        attribute:
            count: 200
            identifier_attribute: "sku"
        family:
            count: 30
            attributes_count: 60
            identifier_attribute: "sku"
            label_attribute: "label"
```

Generating products:
```yaml
data_generator:
    output_dir: /tmp/generated_data
    entities:
        product:
            count: 1000
            values_count: 50
            values_count_standard_deviation: 10
            mandatory_attributes: [sku, name]
            delimiter: ,
            force_values:
                - manufacturer = FactoryInc
                - brand = SuperProd
            start_index: 0
            categories_count: 10
```

More configuration examples are available in the ``Resources\examples`` directory.

If not attribute and family are defined, the product generation will use the available attributes in the PIM DB.

How to use the generated attributes and families data
-----------------------------------------------------
The generated files are meant to be used in the fixtures. Only the generated products CSV file
must be imported by the import profiles.

Compatibility
-------------
Tested on PIM CE 1.1, CE 1.2, CE 1.3, EE 1.0 and EE 1.3.

Credits
-------
Thanks @fzaninotto for Faker ! (https://github.com/fzaninotto/Faker)
