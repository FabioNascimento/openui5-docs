| loio |
| -----|
| 68d0e58857a647d49470d9f92dd859bd |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/68d0e58857a647d49470d9f92dd859bd.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/68d0e58857a647d49470d9f92dd859bd) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/68d0e58857a647d49470d9f92dd859bd)</div>
<!-- loio68d0e58857a647d49470d9f92dd859bd -->

## Instantiating Views

To instantiate views asychronously, OpenUI5 provides the factory method `View.create` defined in module `sap/ui/core/mvc/View`.

To pass the required information for the instantiation, use an object with the following properties:

-   `type`: The type can be `JSON`, `JS`, `XML` or `HTML`. All possible types are declared in the enumeration `sap.ui.core.mvc.ViewType`.

-   `viewName`: View name corresponding to the module concept

-   `viewContent`: Only relevant for XML views and JSON views. Defines the XML or JSON string representation of the view definition. If `viewName` and `viewContent` are given, the `viewName` property is used to load the view definition.

-   `Controller`: Any controller instance; the given controller instance overrides the controller defined in the view definition

-   `viewData`: Only used for JS views; this property contains user-specific data that is available during the whole lifecycle of the view and the controller


All regular properties of a view \(control\) can be passed to the object as usual.

***

### Loading Views

The default mode is the asynchronous loading of a view: The advantage of asynchronous loading compared to synchronous loading is that the UI does not freeze for the duration of the loading process and there is no blockage of functionalities during view initialization.

With the asynchronous loading of views, the instance is not fully available at the moment of creation, instead you may receive a `Promise` via the `View.prototype.loaded` method. The following code snippet shows how the view instance is available in the resolve function of the `promise`.

> Note:
> If you access the view in the controller's `onInit` callback, the view instance is available in any case. The behavior does not change.
> 
> 

```lang-js
// "View" required from "sap/ui/core/mvc/View"
// "coreLibrary" required from "sap/ui/core/library"
// "my.own.controller" was defined earlier
View.create({
    viewName: "my.own.view",
    controller: "my.own.controller",
    type: coreLibrary.mvc.ViewType.XML
}).then(function(oView) {
    // the instance is available in the callback function
    oView.placeAt("uiArea");
});
```

***

#### Synchronous Mode

> Note:
> We do **not** recommend this mode. Use the asynchronous mode instead.
> 
> 

The following code snippet creates a view instance, loads the view source, places the instance to the `uiArea`, and renders it later on.

```lang-js
var oController = sap.ui.controller("my.own.controller");
var oView = sap.ui.view({
    viewName: "my.own.view",
    controller: " my.own.controller",
    type: sap.ui.core.mvc.ViewType.XML
});

// the instance is available now
 oView.placeAt("uiArea");
...
```

***

<a name="loio68d0e58857a647d49470d9f92dd859bd__section_mcg_g5w_vfb"/>

### Lazy Loading for XML Views

The following code snippet shows how to do a lazy loading for XML views:

```lang-xml
<!-- File: view/CustomView.view.xml -->
<mvc:View xmlns="sap.m" xmlns:mvc="sap.ui.core.mvc">
    <Text text="Custom View loaded ..."/>
</mvc:View>
```

```lang-js
// File: controller/MainController.controller.js
sap.ui.require(["sap/ui/core/mvc/XMLView", "sap/ui/core/mvc/Controller"], function(XMLView, Controller) {
	return Controller.extend("samples.controller.MainController", {
		// ...
		onSomeEventTriggered: function() {
			// instantiate view using create-factory
			XMLView.create({
				viewName: "samples.view.CustomView"
			})
			.then(function(oCustomView) {
				// View loaded ...
			})
		}

	});
 });
```

For an example, see the [`sap.ui.core.sample.View.async/preview`](https://openui5.hana.ondemand.com/explored.html#/sample/sap.ui.core.sample.View.async/preview) sample in the Demo Kit.
