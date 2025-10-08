## SELinux module for browsers

By default Fedora/RHEL/CentOS will let your user run unconfined, which means your user and all processes opened by your user have access to almost everything. This is bad for a security point of view. The best way to check if this is the case is to try to open the following links in your browser:

* file:///home/YOUR_USERNAME/.ssh/
* file:///home/YOUR_USERNAME/.gnupg/

If the browser can open the links, it means it has access to data that it should never access. Of course, this could be a problem only if there is a security vulnerability withing the browser, which would allow an attack to access your data.

This policy is designed to create a proper context for the Firefox and Chromium browsers, so that they have limitted access to the system. The policy was designed to protect users running as unconfined_t from possible attacks originating from the browser. This covers far more than the examples above. It also blocks access to the laptop camera.

To enable the policy, all you have to do is `git clone` and (be sure you have some knowledge about the commands before running them, so that you don't consider specific changes as "unexpected"):

```
sudo dnf install selinux-policy-devel make
sudo semodule -i confine-browsers.pp
restorecon -rv /
```

If you have no idea what this stuff means or if you encounter problems with the policy, please contact me or open an issue.

I am open to suggestions, if you feel like the policy needs adjustments.

### Removing the policy

Just do:

```
sudo semodule -r confine-browsers
```

### Upgrading the policy
Just pull the latest version, make and install.
```
git pull
make
sudo semodule -i confine-browsers.pp
```
