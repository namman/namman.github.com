---
comments: true
date: 2012-08-10 16:22:26
layout: post
slug: binding-controls-to-lightswitch-screens
title: Binding controls to Lightswitch screens
wordpress_id: 112
categories:
- exocortex
---

Create the control as Silverlight User Control.

Make sure there is a dependency property in the control for the data you want to access from the Lightswitch screen.

Add ref to Lightswitich project.

Add code to the ...Created() hook:


```csharp
// The entity for the screen is 'Customer'.
partial void Customer_InitializeDataWorkspace()  // some people use .._Created, but this is actually run after the screen is displayed
 {
    var proxy = this.FindControl("NameOfYourControl");
/** this is the name in the properties view in Lightswitch, not necessarily the class name of the control**/
    proxy.ControlAvailable += OnControlAvailable; // hook up event handler below.  It will fire when Lightswitch initialises the control.

 }
```csharp


Create new event to set up the binding when Lightswitch initialises control:

```csharp
using Microsoft.LightSwitch.Threading;

private void OnControlAvailable(object sender,
 ControlAvailableEventArgs e)
 {
 Dispatchers.Main.BeginInvoke(() =>
 {
YourControlName c = e.Control as YourControlName;

// can fiddle with control here if you like

var b = new Binding("Value");
b.Mode = BindingMode.TwoWay;

rc.SetBinding(YourControlName.NameOfDependencyPropertyYouWantToBindTo, b);
/**Note this is the name of the dependency property in the control.  It has to end in 'Property'.**/
 });
 }
```

"Value" path in Binding: This specifies the path of what we bind to in the Lightswitch screen.

The Data Context is automatically set by Lightswitch.  Usually the custom control content element is attached to a property of the EF-generated Entity for the screen.  So the data context is already narrowed down to an entity.  For example, the entity of the screen could be 'Customer', the table 'Customers'.

The Customer entity has a 'Name' property.  The custom control might be attached to the 'Name' property in the Lightswitch designer.  In this case, then we are binding to the Name.Value.  So when we call SaveChanges() on the data context, the value from the control will go into the database. 
