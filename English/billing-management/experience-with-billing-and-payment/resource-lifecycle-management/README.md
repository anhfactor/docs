# Resource lifecycle management

Use this document to understand more about the resources you are using.

Here, we provide information about the resource lifecycle and the user or system actions that can change the state of a resource.

The resource lifecycle models below give you an overview of how a resource moves between states, and how resources are linked to invoices.

### Resource lifecycle model for prepaid users

* **New → Active:** When the user successfully creates the resource, it becomes Active and the corresponding invoice is generated.
* **Active ⇄ Stopped:** The user performs Start, Reboot / Stop on the resource to switch between these two states.
* **Active / Stopped → Suspended:** A resource that expires without being renewed is suspended. Its data is kept.
* **Suspended → Active:** The user renews the resource during the suspension period to continue using it.
* **Active / Stopped → Deleted:** The user deletes the resource.
* **Suspended → Deleted:** If the resource is still not renewed when the suspension period ends, it is permanently deleted and cannot be restored.
* **Invoice generation:** An invoice is generated whenever the user creates, resizes or renews the resource, or when the system auto-renews it.

For the detailed timeline after a resource expires, see Renew expiring resources.

### Resource lifecycle model for postpaid users

* **New → Active:** When the user successfully creates the resource, it becomes Active.
* **Active ⇄ Stopped:** The user performs Start, Reboot / Stop on the resource to switch between these two states.
* **Active → Deleted:** The user deletes the resource.
* **Invoice generation:**
  * Invoices are generated at the end of each month, recording the resource's usage during the month.
  * When the user deletes the resource, the system records the time usage stopped, and the cost up to that time is included in the end-of-month invoice.
