### pfSense-frr-delay
A simple system patch to delay the start of FRR.
#### Warning
This is a hacky solution to an issue I was having with FRR and Wireguard on pfSense. It may help if you're having a similar issue or it might make your firewall burst into flames.
#### Background
The FRR service starts before Wireguard and the interface reconfiguration that Wireguard does on boot seemed to break connectivity with tunnel neighbors until I went into the FRR Global settings and forced a service restart. The patch just adds a 30 second sleep to the beginning of frr.inc to slow down the startup. For me, this fixed the issue. I'm certain there are better ways to do this but I just needed something that would work until Netgate fixed the issue.

#### Update
I rewrote the patch to use rc.start_packages so the delay is only introduced during bootup. The previous version added a 30 second delay every time that I navigated to any FRR page and it was painful.

#### Installation
1. Install the System Patches package in pfSense if you haven't already.
2. Go to System > Patches
3. Click the green Add New Patch button near the top
4. Enter whatever you want in Description
5. Either paste the github URL for frr_delay.patch in the URL box or copy the contents of the file into the Patch Contents box
6. Set Path Strip Count to 1
7. Leave Base Directory as /
8. Uncheck Ignore Whitespace
9. Check Auto Apply if you want
10. Click Save
11. Click Apply to the right of the patch description
