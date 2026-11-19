# Restart Instance

Restarting a VM is equivalent to rebooting the operating system. In most cases, it only takes a few minutes to restart your virtual server.

When you restart the server, it will retain the following:

* Public DNS name (IPv4)
* Private IPv4 address
* Public IPv4 address
* IPv6 address (if applicable)

And any data on its storage volume.

Restarting the server does not start a new billing cycle (with a minimum fee of one minute), unlike stopping and starting your server.

We can schedule restarts of your instance for necessary maintenance, such as applying updates requiring a restart. You don't need to take any action; we advise you to wait for the scheduled restart process to occur in the scheduled window.

We recommend using the vServer Portal dashboard, command-line tool, or API to restart your instance. If you use the vServer Portal dashboard, command-line tool, or API to restart your server, we will perform a hard restart if the instance doesn't shut down completely within a few minutes.<br>

***

**To restart a server using the dashboard:**

1. Open the vServer dashboard at: [https://hcm-3.console.greennode.ai/vserver/](https://hcm-3.console.greennode.ai/vserver/)
2. In the navigation pane, select the Server tab.
3. Select the desired Server and choose Actions, then select Restart from the drop-down list.
4. Confirm when prompted to restart.
5. The server will then be in the Rebooting state.
