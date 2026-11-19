# Quota and FAQ

## Quota

* Each account has a maximum number of Scheduled Tasks it can create. The current default is **20 tasks per account**.
* Creating or duplicating a task consumes quota; deleting a task releases it.
* You can check your current quota directly in the O&M interface.

{% hint style="info" %}
**Note:** If you see a quota-exceeded message when creating a task, delete tasks you no longer need or contact VNG Cloud support to raise your quota.
{% endhint %}

## Frequently asked questions

### My task did not run at the scheduled time. Why?

Check in order: (1) the task is still **ACTIVE** (a CANCELED or EXPIRED task never runs); (2) the current time falls inside the effective window (effective from/until); (3) the service activation status is **ACTIVE**. If all three are correct and the task still does not run, contact support with the task name and the scheduled time.

### What does the SA\_BROKEN activation status mean?

Your Service Account is broken — usually because it was deleted or its permissions were changed unintentionally. Just click **Re-activate** and the system repairs it. Your existing tasks are not lost; schedules resume once activation succeeds.

### I deleted a VM in vServer. Will my task fail?

No. Before each execution the system reconciles the target list against vServer and drops any deleted VM. The task continues to run normally on the remaining VMs.

### An execution reported PARTIAL\_FAILED. What should I do?

Open the execution details to inspect each VM — the failing ones carry a specific error message. Resolve the underlying cause (for example a VM in a state that does not allow the operation), then click **Run now** to retry if needed.

### Does a manual run shift the automatic schedule?

No. A manual run (**MANUAL**) is independent of the schedule; the next automatic run still happens at its scheduled time.

### How do I pause a task for a while?

Use **Cancel** to stop the schedule — the history is preserved. When you need it again, create a new task or use **Duplicate** on the cancelled task to restore its configuration quickly.

### Can one task cover VMs in multiple regions?

Not yet. In this Beta each task belongs to a single region. If you have VMs in both **HCM-03** and **HAN-01**, create a separate task per region.

## Feedback and support

While using the Beta, if you run into an issue or want to suggest a feature, please contact VNG Cloud support through your existing support channel. Your feedback is an important input as we refine the product ahead of general availability.
