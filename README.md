# named-resolver

This is an ISC `bind` (named) DNS slave. As an exomaple, it mirrors the ROOT zone.
To get it to mirror the zones you want, simply change the `extra.conf` file.

It runs in a `chroot` which is a little unnecessary, but its not hard, so why not.

The default is to allow **ANYBODY** to send queries to this server. If it is on a
public IP, you should probabyl have some kind of mechanism to throttle queries, or it
may be D/DoS'd.

Alternatively, is you only want certain IPs/subnets to be able to query this slave, then
you can change this line ...

	acl allowed-nets { any; };

so instead of `any` you have a semi-colon separated list of the IPs / subnets you want permission
to query this server.


## IPv6 ##

NOTE: this is currently configured to only support IPv4. This is becuase `bind` is really laggy if
it is configured for IPv6, but IPv6 connectivity is not available.

To re-enabled IPv6, remove the `-4` in the `inittab` file, and change the line

	listen-on-v6 { none; };

to

	listen-on-v6 { any; };
