# Data Quality Bundle for Pimcore

Depending on user-configurable weighted rules (data quality configuration objects)
one- or multiple quality values are computed and stored in data objects.

-------

## Version

| Bundle Version | PHP | Pimcore |
| ----------- | -----------| ----------- |
| &lt; 2.0 | ^7.3 | ^6.0 |
| &gt;= 2.0 | ^8.0 | ^10.0 |

## Installation
1. Require the bundle using ``composer require basilicom/pimcore-data-quality-bundle``
3. Enable the bundle ``bin/console pimcore:bundle:enable DataQualityBundle``
3. Instakk the bundle ``bin/console pimcore:bundle:install DataQualityBundle``

## Configuration
1. Add a field of type ``number`` to the object class that you want to analyze.
![](documentation/data-quality-field-for-percentage.jpg)

2. Add a new data object of type ``DataQualityConfig`` in your object tree
   * Give it a name
   * Choose a class from the select box and hit ``Save & Publish`` and reload
   * Choose the field you created in step 1 for the data quality percentage
   ![](documentation/data-quality-config-object.jpg)
   
3. Rules
   * Choose the field you want to check
   * Choose the condition you want to check for
      * Some conditions need extra parameters. parameters are ; separated values.
   * Set a weight or use 1 for default weight
      * if you want one field to be double the weight, set to 2
      * set a Group name if you want, or it will be just one group
      ![](documentation/data-quality-rules.jpg)
      
4. Add the new field type ``Data Quality`` from the Layout Components to the chosen object class
   * it works like a panel so use it where ever you like
   * you can configure on DataQualityConfig object id to show only the one or leave it empty to show all configs
   ![](documentation/data-quality-layout-field.jpg)
   * this is the layout inside of the DataQuality Tab
   ![](documentation/data-quality-field.jpg)
   * or just use the Tab that is added by the bundle that shows all configs
   ![](documentation/data-quality-tab.jpg)
 
5. The data quality value field is updated whenever 
   * an object is saved by a normal user (non-system user), or
   * the data quality tab or iframed is displayed, or
   * a full update (re-calculation) of all
     data quality values was performed via the console command:
   ``bin/console dataquality:update --quality-config-id=DQC_OBJECT_ID``
  
6. You can use the "Operator PHP Code" Basilicom\DataQualityBundle\GridOperator\Quality
   on a Data Quality (number) field to get color-coded (red to green) percentages  


-------

**Author:** Conrad Guelzow (Basilicom GmbH), Kerstin Gerull (Basilicom GmbH), Christoph Luehr (Basilicom GmbH),

**License:** GPL v3
