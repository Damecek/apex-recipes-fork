# InboundEmailHandlerRecipes

`SUPPRESSWARNINGS`

Demonstrates how to use the inboundEmailHandler
interface to create custom logic and automation on the reception
of an email. This class demonstrates saving the email
to an EmailMessage Object along with Attachments.

NOTE: This class *does not* specify a sharing model.
This is on purpose - When this class is executed, by the inbound
email system, it will execute in a system context and pieces of
this class need to be able to *read* all contacts - which is a
common use case. Because of this, we're suppressing the PMD
ApexSharingViolation warning.


**Implemented types**

[Messaging.InboundEmailHandler](Messaging.InboundEmailHandler)


**Group** Email Recipes


**See** [Safely](https://github.com/trailheadapps/apex-recipes/wiki/Safely)


**See** [FilesRecipes](https://github.com/trailheadapps/apex-recipes/wiki/FilesRecipes)

## Methods
### `public Messaging.InboundEmailResult handleInboundEmail(Messaging.InboundEmail email, Messaging.InboundEnvelope envelope)`

Messaging.InboundEmailHandler interface has one required
method - handleInboundEmail. This method must return an
Messaging.InboundEmailResult object, and you should take care to set that
object's success property. This method is where you will write business
logic to ... do whatever it is you want to do with the incoming email.
Here you can attach the email to the contact record who sent it, a case
or ... The sky's the limit.

#### Parameters

|Param|Description|
|---|---|
|`email`|This is an Messaging.InboundEmail Object that is dependency injected by the system at runtime. Aside from testing, you should not need to call this method or worry about its params.|
|`envelope`|This is an Messaging.InboundEnvelope object that is dependency injected by the system at runtime. Aside form testing, you should not need to call this method or worry about its params.|

#### Returns

|Type|Description|
|---|---|
|`Messaging.InboundEmailResult`|`Messaging.InboundEmailResult`|


**See** [FilesRecipes](https://github.com/trailheadapps/apex-recipes/wiki/FilesRecipes)

### `private void createFilesByEmailAttachments(List<Messaging.inboundEmail.BinaryAttachment> inboundAttachments, Id contactId)`

This helper method bulk saves attachments from
the incoming email. It relies on FilesRecipes.cls to do the actual
creation of the Files attachments as well as publishing the file to the
specified record.

#### Parameters

|Param|Description|
|---|---|
|`inboundAttachments`||
|`contactId`||

### `private Contact getContactBySender(Messaging.InboundEmail email)`

Determines if we have an existing contact record
with an email address that matches the sender of this email.
If we do not have a contact that matches, return a new contact object
with the email address set.

#### Parameters

|Param|Description|
|---|---|
|`senderAddress`||

#### Returns

|Type|Description|
|---|---|
|`Contact`|`Contact`|

### `private void createEmailRecord(Contact sender, Messaging.InboundEmail email)`

Creates a Salesforce Email record and relates that email to
the sender's contact record. This surfaces the Email record on the
contact object.

#### Parameters

|Param|Description|
|---|---|
|`sender`||
|`email`||

---
## Classes
### InboundEmailHandlerRecipesException

**Inheritance**

InboundEmailHandlerRecipesException


---
