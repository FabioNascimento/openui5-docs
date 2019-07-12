| loio |
| -----|
| 335848ac1174435c901baaa55f6d7819 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/335848ac1174435c901baaa55f6d7819.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/335848ac1174435c901baaa55f6d7819) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/335848ac1174435c901baaa55f6d7819)</div>
<!-- loio335848ac1174435c901baaa55f6d7819 -->

## Using Factory Functions

The factory function is a more powerful approach for creating controls from model data. The factory function is called for each entry of a control’s aggregation, and the developer can decide whether each entry shall be represented by the same control with different properties or even by a completely different control for each entry.

The factory function comes with the parameters `sId`, which should be used as an ID for the new control, and `oContext`, which is for accessing the model data of the entry. The returned object must be of type `sap.ui.core.Element`. Here’s how this scenario can be realized in an XML view and a controller using our JSON model data:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:l="sap.ui.layout"
	xmlns:mvc="sap.ui.core.mvc">
	<l:VerticalLayout
		content="{ path: '/companies', factory: '.createContent'}"
		class="sapUiContentPadding"
		width="100%"/>
</mvc:View>
```

Please note the `'.'` in `factory: '.createContent'`. The class `App.controller.js` contains the implementation of our factory method:

```lang-js
sap.ui.define([
	"sap/ui/core/mvc/Controller",
	"sap/ui/model/json/JSONModel",
	"sap/ui/model/type/String",
	"sap/ui/model/type/Float",
	"sap/m/Input",
	"sap/m/Text",
	"sap/m/CheckBox"
], function (Controller, JSONModel, StringType, Float, Input, Text, CheckBox ) {
	"use strict";
	return Controller.extend("sap.ui.sample.App", {
		onInit : function () {
		…
		},
		createContent: function (sId, oContext) {
		var oRevenue = oContext.getProperty("revenue");
			switch(typeof oRevenue) {
				case "string":
					return new Text(sId, {
						text: {
							path: "revenue",
							type: new StringType()
						}
					});
  
				case "number":
					return new Input(sId, {
						value: {
							path: "revenue",
							type: new Float()
						}
					});
				
				case "boolean":
					return new Checkbox(sId, {
						checked: {
							path: "revenue"
						}
					});
			}
		},
	});
});
```

If you would like to avoid using the XML view, you would proceed as follows:

```lang-js
oVerticalLayout.bindAggregation("content", "/companies", function (sId, oContext) {
	var oRevenue = oContext.getProperty("revenue");
	switch(typeof oRevenue) {
			case "string":
				return new sap.m.Text(sId, {
					text: {
						path: "revenue",
						type: new sap.ui.model.type.String()
					}
				});
  
			case "number":
				return new sap.m.Input(sId, {
					value: {
						path: "revenue",
						type: new sap.ui.model.type.Float()
					}
				});
				
			case "boolean":
				return new sap.m.Checkbox(sId, {
					checked: {
						path: "revenue"
					}
				});
			}
		}
});
```

**Related information**  


[Tutorial Step 15: Aggregation Binding Using a Factory Function](Step_15_Aggregation_Binding_Using_a_Factory_Function_284a036.md)
