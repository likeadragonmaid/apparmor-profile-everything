# Full system AppArmor policy #

This is an AppArmor policy to confine all user space processes on the system which
allows one to enforce a strong security model and follow principle of least privilege.
An AppArmor policy for the init, systemd is loaded in the initramfs which then
applies to all other processes. Specific policies for many system services/applications
are also enforced.

This follows design ideas already present in other operating systems such as Android
and attempts to make something similar available on desktop Linux.

In addition to locking down user space, this also protects the kernel as it restricts
access to kernel interfaces like `/proc` or `/sys`, making kernel pointer and other
leaks much less likely.

This does not and cannot confine the kernel or initramfs.

This is expected to be used in combination with other security technologies such as
a hardened kernel, strong sandboxing architecture, verified boot and so on.

apparmor-profile-everything supports different boot modes: aadebug and superroot.
aadebug allows certain permissions necessary for advanced debugging and superroot
relaxes the policy substantially, even making bypasses possible. It is highly
recommended to stick to the default boot mode.

It also contains a wrapper to restrict apt as apt requires permissions that may
be abused to circumvent the policy. When updating or installing applications, you
must use the `rapt` command.

This is still in development and breakage is likely. This should only be used by
developers for now.

For now, please only use this development discussion forum thread:
https://forums.whonix.org/t/apparmor-for-complete-system-including-init-pid1-systemd-everything-full-system-mac-policy/8339

This package is produced independently of, and carries no guarantee from,
The Tor Project.

## How to install `apparmor-profile-everything` using apt-get ##

1\. Download the APT Signing Key.

```
wget https://www.kicksecure.com/derivative.asc
```

Users can [check the Signing Key](https://www.kicksecure.com/wiki/Signing_Key) for better security.

2\. Add the APT Signing Key..

```
sudo cp ~/derivative.asc /usr/share/keyrings/derivative.asc
```

3\. Add the derivative repository.

```
echo "deb [signed-by=/usr/share/keyrings/derivative.asc] https://deb.kicksecure.com bullseye main contrib non-free" | sudo tee /etc/apt/sources.list.d/derivative.list
```

4\. Update your package lists.

```
sudo apt-get update
```

5\. Install `apparmor-profile-everything`.

```
sudo apt-get install apparmor-profile-everything
```

## How to Build deb Package from Source Code ##

Can be build using standard Debian package build tools such as:

```
dpkg-buildpackage -b
```

See instructions.

NOTE: Replace `generic-package` with the actual name of this package `apparmor-profile-everything`.

* **A)** [easy](https://www.kicksecure.com/wiki/Dev/Build_Documentation/generic-package/easy), _OR_
* **B)** [including verifying software signatures](https://www.kicksecure.com/wiki/Dev/Build_Documentation/generic-package)

## Contact ##

* [Free Forum Support](https://forums.kicksecure.com)
* [Professional Support](https://www.kicksecure.com/wiki/Professional_Support)

## Donate ##

`apparmor-profile-everything` requires [donations](https://www.kicksecure.com/wiki/Donate) to stay alive!
