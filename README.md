# FreeBSD relayd

## Building

```
env LIBCRYPTO=... LIBSSL=... LOCALBASE=... OPENSSLINCDIR=... PREFIX=... ./configure
make
```

## Compatibility

The latest tested LibreSSL version is 3.3.5.

## FreeBSD relayd release proecss

Create a new branch called `OPENBSD_VER.LATEST_COMMIT_DATE` (e.g.,
`5.6.2014.08.10`)_ where `OPENBSD_VER` is OpenBSD version returned by `make -f
share/mk/sys.mk -v OSREV` and `LATEST_COMMIT_DATE` is the commit date of the
latest OpenBSD commit (e.g., `2014.08.10`).

