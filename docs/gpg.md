# GPG Keys

## Summary

After our security incident in July 2014, we planned to try and contain the scope of our GPG keys to avoid resigning lots of content if (or rather, when) a key is compromised or has to be revoked.

* Time based keys: for use with Debian archives. Cycled every two years.
* Release based keys: for use with tarballs, RPMs. Expiry of one year.

## Generating a new key

`generate_gpg` from [theforeman-rel-eng](https://github.com/theforeman/theforeman-rel-eng/) can be used to generate new keys.

See [Generating a new GPG Key for a X.Y release](https://github.com/theforeman/theforeman-rel-eng/#generating-a-new-gpg-key-for-a-xy-release) and [Generating a new GPG Key for signing the Debian repository](https://github.com/theforeman/theforeman-rel-eng/#generating-a-new-gpg-key-for-signing-the-debian-repository) for documentation how to do so.

## Distributing keys

### Release based keys

RPM users are told in install & upgrade documentation to install foreman-release from the new release, which can contain the keys for that release, making distribution easy.

### Time based keys

Debian archives can be signed with multiple keys (by setting those in `freight.conf`), but key distribution to users is manual right now.

To make our infrastructure aware of the new keys, one needs to:

* Export private key to `freight{,stage,archive}@web01`
* Configure it in `puppet/modules/freight/templates/freight.conf.erb`, examples:
  * 7680053 - Add 2016 archive key, thus using two keys for a period of time
  * 9f50f62 - Remove 2014 archive signing GPG key
