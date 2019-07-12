| loio |
| -----|
| e2e6f4127fe4450ab3cf1339c42ee832 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/e2e6f4127fe4450ab3cf1339c42ee832.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/e2e6f4127fe4450ab3cf1339c42ee832) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/e2e6f4127fe4450ab3cf1339c42ee832)</div>
<!-- loioe2e6f4127fe4450ab3cf1339c42ee832 -->

## Binding Syntax

You bind UI elements to data of a data source by defining a binding path to the model that represents the data source in the app.

***

When defining a binding path for a control, a binding context is created which connects this control to a data model. The UI control then gets the data through that context and displays it on the screen.

![](loio493c875d822445458e0b56e0cc6451b2_LowRes.png)

-   [Views](Views_91f27e3.md)
-   [Binding Path](Binding_Path_2888af4.md)
-   [Models](Models_e1b6259.md)

***

<a name="loioe2e6f4127fe4450ab3cf1339c42ee832__section_ezj_nhr_5cb"/>

### Simple Binding

To reference model data in a view , you can use the simple binding syntax "`{*/path/to/data*}`":

```lang-xml
<Input value="{/firstName}"/>
```

You can add other properties like formatters or data types:

-   Data type:

```lang-xml
<Input value="{path: '/firstName', type: 'sap.ui.model.type.String'}"/>
```

-   Formatter:

```lang-xml
<Input value="{path: '/firstName', formatter:'my.globalFormatter'}"/>
```


For more information, see [Binding Path](Binding_Path_2888af4.md).

For more information about data types and formatters, see [Formatting, Parsing, and Validating Data](Formatting,_Parsing,_and_Validating_Data_07e4b92.md).

***

<a name="loioe2e6f4127fe4450ab3cf1339c42ee832__section_njl_ypr_5cb"/>

### Composite Binding

If a control requires data from multiple different model properties, you use a `parts` array of `path`s to define composite binding paths:

```lang-xml
<TextField value="{
	parts: [
		{path:'birthday/day'},
		{path:'birthday/month'},
		{path:'birthday/year'}
	], 
	formatter:'my.globalFormatter'
}"/>
```

For more information, see [Composite Binding](Composite_Binding_a2fe8e7.md) and [Examples for Data Binding in Different View Types](Examples_for_Data_Binding_in_Different_View_Types_25ab54b.md).

***

<a name="loioe2e6f4127fe4450ab3cf1339c42ee832__section_htn_jqr_5cb"/>

### Expression Binding in XML Views

Expression binding is a simple way to calculate values directly in the view. For example, if you want to change the color of the price depending on whether it is above or below some threshold. With expression binding you don't have to declare a separate formatter:

```lang-xml
<ObjectStatus state=="{= ${products>UnitPrice}  > ${/priceThreshold} ? 'Error' : 'Success' }"/>
```

For more information, see [Expression Binding](Expression_Binding_daf6852.md).

***

<a name="loioe2e6f4127fe4450ab3cf1339c42ee832__section_kft_lqr_5cb"/>

### Property Metadata Binding for OData Services

With metadata binding, you can bind properties of a control to the corresponding property that is defined in the metadata of an OData service:

```lang-xml
<Input maxLength="{/#Company/ZipCode/@maxLength}"/>
```

For more information, see [Property Metadata Binding](Property_Metadata_Binding_f5aa4bb.md).

**Related information**  


[API Reference: `sap.ui.base.ManagedObject.bindProperty`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/bindProperty)

[API Reference: `sap.ui.base.ManagedObject.bindAggregation`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/bindAggregation)

[API Reference: `sap.ui.base.ManagedObject.bindObject`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/bindObject)
