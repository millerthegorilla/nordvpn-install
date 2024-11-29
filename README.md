# nordvpn-install for RPM-OSTREE

Install the NordVPN client on Fedora Silverblue!    Just download the install.sh, edit it to change the NORD_VERSION environment variable.  Currently it is set to "-3.18.5" so that nordvpn-3.18.5 is installed.  This is because the nordvpn team have not signed the nordvpn rpm correctly and silverblue complains and prevents it from being installed.

The script installs the repo, by downloading nordvpn in a toolbox, which it will make, installing the necessary image if it can't find it.  The toolbox is used to download the repo details.  It then adds the repo to the base image /etc/yum.repos.d/ calls rpm-ostree to install the binary appending the version string which is currently defined by default.  The toolbox is then deleted.

Dependencies are installed, and unfortunately the --idempotent flag to the rpm-ostree install command doesn't seem to work, so I have added --allow-inactive.  This layers the dependencies unnecessarily if they are already layered, I think...
 
The nordvpn rpm client does not install on Silverblue correctly as the rpm package contains files in locations that are immutable on Silverblue.  So, the install adds the repo, and the key manually, and then installs the package and then uses rpm2cpio to unpack the rpm so that the correct nordvpn file structure is created.  This is, of course, a hack, but it works well.

The script may probably be buggy as I haven't tested it properly yet, but it has worked for me.

MIT License attribution etc, and usual disclaimer -  USE AT OWN RISK!!!  (but should work ok)...
