---
title: "updateRecord (JavaScript API Reference) for Channel Integration Framework (CIF) in Dynamics 365 | MicrosoftDocs"
description: ""
keywords: ""
ms.date: 10/01/2018
ms.service:
  - "dynamics-365-cross-app"
ms.custom:
  - "dyn365-a11y"
  - "dyn365-developer"
ms.topic: reference
applies_to:
  - "Dynamics 365 (online)"
  - "Dynamics 365 Version 9.x"
ms.assetid: 15BD79E6-8B31-4916-A6C7-777D228804A2
author: kabala123
ms.author: kabala
manager: shujoshi
---

# updateRecord (CIF JavaScript API Reference)
> [!Important]
> [!INCLUDE[cc-beta-prerelease-disclaimer](../../../../includes/cc-beta-prerelease-disclaimer.md)] 

[!INCLUDE[updateRecord](includes/updateRecord-description.md)] 

## Syntax

`microsoft-ciframework.updateRecord(entityLogicalName, id, data).then(successCallback, errorCallback);`

## Parameters

<table style="width:100%">
<tr>
<th>Name</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>entityLogicalName</td>
<td>String</td>
<td>Yes</td>
<td>The entity logical name of the record you want to update. For example: &quot;account&quot;.</td>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>Yes</td>
<td>GUID of the entity record you want to update.</td>
</tr>
<tr>
<td>data</td>
<td>Object</td>
<td>Yes</td>
<td><p>A JSON object containing <code>key: value</code> pairs, where <code>key</code> is the property of the entity and <code>value</code> is the value of the property you want to update.</p>
<p>See examples later in this topic to see how you can define the <code>data</code> object for various update scenarios.</td>
</tr>
<tr>
<td>successCallback</td>
<td>Function</td>
<td>No</td>
<td><p>A function to call when a record is updated. An object with the following properties will be passed to identify the updated record:</p>
<ul>
<li><b>entityType</b>: String. The entity type of the updated record.</li>
<li><b>id</b>: String. GUID of the updated record.</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>Function</td>
<td>No</td>
<td>A function to call when the operation fails. An object with the following properties will be passed:
<ul>
<li><b>errorCode</b>: Number. The error code.</li>
<li><b>message</b>: String. An error message describing the issue.</li>
</ul></td>
</tr>
</table>

## Return Value

On success, returns a promise object containing the attributes specified earlier in the description of the **successCallback** parameter.

## Examples

This sample code updates an existing contact record with record ID = a8a19cdd-88df-e311-b8e5-6c3be5a8b200

```JavaScript
//// define the data to update a record
var entityLogicalName = "contact";
var data = {
    "firstname": "Updated Sample",
    "lastname": "Contact",
    "fullname": "Updated Sample Contact",
    "emailaddress1": "contact@contoso.com",
    "jobtitle": "Sr. Marketing Manager",
    "phonenumber": "555-0109",
    "description": "Updated values for this record were set programmatically."
}
// update contact record
Microsoft.CIFramework.updateRecord(entityLogicalName,id,data).then(
    function success (result) {
          console.log("Contact updated with ID: " + result.id);
          //perform operations on record creation
      },
      function (error) {
          console.log(error);
          //handle error conditions
      }
  );
```