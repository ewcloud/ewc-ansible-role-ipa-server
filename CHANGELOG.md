# Changelog

All notable changes to this project are documented in this file. See
[Conventional Commits](https://conventionalcommits.org) for commit guidelines.

# 1.0.0 (2025-09-05)


### Bug Fixes

* Condition checking for initial play run vs replays ([145cafb](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/145cafb5de5e69d94576165c315bbba2fe243ffb))
* Remove VM RAM validation to prevent false positives during role replay ([35c1593](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/35c159387996bf20a5b29715d40e7860fab12f8f))


### Features

* Automatic OpenStack subnet setup ([c772d3a](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/c772d3a1dd9fee291a01b4cf685ba61b0c2d553c))
* Automatic security patch rollout via built-in RockyLinux functionality ([68fcbf2](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/68fcbf254f9fbf349d3fb316f4c00f46959c9b3e))
* Condition idM system module enablement only to RockyLinux 8 ([5a03b70](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/5a03b70234e9dd953659de5411912afbfb4f9936))
* Configure IPA server based on user input ([fded201](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/fded2014ea6dcbeacc66d9945a43f457f3da5e40))
* Default IPA admin replaced by user-defined admin without password expiration ([758048d](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/758048d3f1aad75899dcfc864f99f4f37aa325cf))
* Disable automatic security patching ([49bc684](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/49bc6848f3b10cff745012f383e373961e7ec1da))
* Disabled root SSH access to reduce attack surface ([ebb16ed](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/ebb16ed31fcaeabc025c16249c2a6d17353b61d7))
* Downgrade Security Enhanced Linux access control policies to simplify IPA setup ([6e5e231](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/6e5e231c1816e37dc1a7f9a846b47624bc1d6a6a))
* Downgrade supported distributions to Rocky 9.5 ([acf780b](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/acf780ba4addd5c7c822cffa40d0440155d16c2d))
* Enable replay by skipping initial IPA admin setup on subsequent runs ([72d1c8b](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/72d1c8bc1356398186a4e4675d02d45825522f9f))
* Ensure configured services stay operational between VM reboots ([04c7b90](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/04c7b90f513bd35d3011b57505ff26c6980ce53f))
* Include details of validated security group in execution summary ([6a8bb64](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/6a8bb643fde914e0657aeefc10f37d5bfcf77885))
* Install and list versions of core requirements ([e9e14e2](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/e9e14e2d061fe3e01fd8707ab860e46e4ef7df6e))
* Linux distro check to ensure deployment on RockyLinux 8 and 9 only ([e7be122](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/e7be1227403c634ae241bd66b1d6c4c4688bd7b8))
* Override DNS config for the IPA server to resolve its own IP ([a7645fb](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/a7645fb7dbb57a56fd8a597b9c524ea5de550ecc))
* Overwrite domain name and host name according to user input ([89b9f2d](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/89b9f2dae991c24f5402ba66d39371f0502ef3f1))
* Pin packages versions ([ff95c0b](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/ff95c0bf5992896b33ae339451c6dbc0cc0a8d40))
* Prevent credential leaks into logs upon task failure ([afa26d8](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/afa26d853d76b1a63845fd40eb5510d29b63e5e1))
* Restrict supported Linux distros down to the minor version ([7c4e4c4](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/7c4e4c4f2dc5585e927823984dd82c1d84ea9000))
* Simplify user input spec and auto-validate networking ([16cf259](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/16cf2597927d2035ed47496e38af9cc092aa56e3))
* Validate inputs to prevent IPA breakdown and remove input defaults ([b2be87e](https://github.com/ewcloud/ewc-ansible-role-ipa-server/commit/b2be87e95bcfdeaf13a438e314e3256d373f7975))
