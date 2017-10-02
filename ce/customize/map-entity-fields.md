---
title: "Map entity fields (Dynamics 365 Customer Engagement) | MicrosoftDocs"
ms.custom: ""
ms.date: 09/30/2017
ms.reviewer: ""
ms.service: "crm-online"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "Dynamics 365 (online)"
  - "Dynamics 365 Version 9.x"
ms.assetid: 7c5aa1c3-bde9-43f1-a369-fdcdbf14dec0
caps.latest.revision: 33
ms.author: "rdubois"
manager: "brycho"
tags: 
---
# Map entity fields

[!INCLUDE[cc-applies-to-update-9-0-0](../includes/cc_applies_to_update_9_0_0.md)]

<a name="BKMK_mappingEntityFields"></a>   
 
 You can map attributes between entities that have an entity relationship. This lets you set default values for a record that is created in the context of another record. Let’s say that you want to add a new contact record for a person who is an employee for a specific account. You can do this in two different ways:  
  
 You could just navigate to **Sales** > **Contacts** and create a new contact record from scratch. But then you need to set the parent account and enter several items of information (such as address and phone information) which are probably the same as the parent account. This can be time consuming and introduces opportunities for errors.  
  
 The easier way is to start with the account entity and, using the **Contacts** subgrid on the form, click **+** to add a contact. It will first guide you to look up any existing related contacts so you don’t accidentally create a duplicate record. If you don’t find an existing record, you can click **New** and create a new contact record. The difference is that certain items of data from the account record will be copied into the new contact form to set certain default values that you can edit before saving. This can save a lot of time when you are entering data, and help reduce errors.  
 
<!-- 
 [Entity and Attribute mappings](../customize/default-entity-attribute-mappings.md) shows all the default mappings set for [!INCLUDE[pn_dynamics_crm](../includes/pn-dynamics-crm.md)].  -->
  
> [!NOTE]
>  These mappings aren’t applied to related records created using a workflow or dialog process. They aren’t automatically applied to new records created using code, although developers can use a special message called InitializeFromt <!-- (../developer/webapireference/functions/descriptions/initializefrom.md) --> to create a new record using available mappings.  
<!-- Vivek says: This will eventually be https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.initializefromrequest when we publish the MREF content live on docs. 
From Amy: After discussing with Vivek, we decided to go with the new style, not the old .net style. Link is now fixed.-->
>   
>  These mappings only set default values to a record before it is saved. People can edit the values before saving. The data that is transferred is the data at that point in time. It isn’t synchronized. If the information in the primary entity record changes, the related entity record data that was transferred when it was created won’t change.  
  
 The default values set when you create a new record from a list aren’t actually defined within the entity relationships, but they are exposed in the relationship user interface. Not every 1:N entity relationship has them. When you view a list of 1:N (or N:1) entity relationships for an entity, you can filter the relationships shown by type. You can select either **All**, **Custom**, **Customizable**, or **Mappable**. Mappable entity relationships provide access to allow mapping entity fields.  
  
 The following rules show what kinds of data can be mapped.  
  
-   Both fields must be of the same type and the same format.  
  
-   The length of the target field must be equal to or greater than the length of the source field.  
  
-   The target field can’t be mapped to another field already.  
  
-   The source field must be visible on the form.  
  
-   The target field must be a field that a user can enter data into.  
  
-   If the fields are option sets, the integer values for each option should be identical.  
  
-   Address ID values can’t be mapped.  
  
> [!NOTE]
>  If you need to map option set fields, we recommend you configure both fields to use the same global option set. Otherwise, it can be difficult to keep two separate sets of options synchronized manually. If the integer values for each option aren’t mapped correctly you can introduce problems in your data. [!INCLUDE[proc_more_information](../includes/proc-more-information.md)] [Create and edit global option sets](../customize/create-edit-global-option-sets.md)  
  
#### Create or edit mapping between fields  
  
1. [!INCLUDE[proc_settings_customization](../includes/proc-settings-customization.md)]  
  
2.  Click **Customize the System**.  
  
3.  Under **Components**, expand **Entities**, and then expand the entity you want.  
  
4.  Click either **1:N Relationships** or **N:1 Relationships**.  
  
5.  In the main pane, in the **Type** list, select **Mappable**.  
  
6.  Select a mappable relationship. Then, on the Actions toolbar, click **Actions**, and then click **Edit**.  
  
7.  Under **Related**, click **Mappings**.  
  
8.  For each new mapping, on the **Actions** toolbar, click **New**.  
  
9. In the **Create Field Mapping** dialog box, select the source field from **Source Entity Fields**. Select the target field from **Target Entity Fields**.  
  
10. Click **OK**.  
  
11. Click **Save and Close** to close the **Relationship** form.  
  
12. When your customizations are complete, publish them  
  
> [!NOTE]
> - After publishing customizations, these mappings are available for all users. If you reset [!INCLUDE[pn_Internet_Information_Services](../includes/pn-internet-information-services.md)] before you publish customizations, these mappings are available for all users, even though other customizations won’t be available.  
> - If you map to or from a field that isn’t displayed on a form, the mapping won't be done until the field is added to a form.  
  
## Automatically generate field mappings  
 You can also generate mappings automatically but you should use care when doing this with system entities. Use this when you create custom entities and want to leverage mapping. When viewing the list of mappings, in the **More Actions** menu select **Generate Mappings**. This removes any existing mappings and replaces them with suggested mappings that are based only on the fields that have similar names and data types. If you use this on a system entity, you could lose some expected mappings. For custom entities, it helps save time because you can more easily delete any mappings you don’t want and add any others that the generate mappings action didn’t create.  