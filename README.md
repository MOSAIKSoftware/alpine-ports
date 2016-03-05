# APKBUILD guide

## Requirements

This has to be done once, as root:
```
apk add alpine-sdk
sudo mkdir -p /var/cache/distfiles
sudo chmod a+w /var/cache/distfiles
abuild-keygen -a -i
```

## create APKBUILD

As user, do:
```
mkdir ~/myports
cd ~/myports
newapkbuild <arguments> <packagename>
```

newapkbuild options:
* -a Create autotools (use ./configure ...)
* -c Copy a sample init.d, conf.d and install script to new directory
* -d Set package description (pkgdesc) to DESC
* -f Force even if directory already exist
* -h Show this help
* -l Set package license to LICENSE
* -p Create perl package (Assume Makefile.PL is there)
* -y Create python package (Assume setup.py is there)
* -u Set package URL
* -s Use sourceforge source url

### Minimal required modifications

* `_builddir` must be set, often something like `${srcdir}/${pkgname}-${pkgver}`
* `source` must be set and point to the remote tarball
* `pkgver` must be set

### Dependencies

* dynamic link-time dependencies are figured out automatically
* `makedepends` are only build-time dependencies and usually contain stuff like `<libname>-dev`, which provide headers
* `depends` are runtime dependencies, which are not dynamically linked libraries

### Error handling

...is stupid. `|| return 1` must be appended basically everywhere. Not `exit`!

## Build APKBUILD

This will require sudo priviliges:
```
cd ~/myports/<packagename>
abuild -r
```

## Docs

* http://wiki.alpinelinux.org/wiki/Creating_an_Alpine_package
* http://wiki.alpinelinux.org/wiki/APKBUILD_Reference
* http://wiki.alpinelinux.org/wiki/APKBUILD_examples

