# rpm-lxc
Build lxc rpms for EL9

## Install build tools
As root:
```
dnf --enablerepo=crb install ninja-build
dnf install pip rpm-build rpmdevtools
```
As nonprivileged user:
```
pip install meson  # meson shipped with EL9 is too old
```

## Build RPM
As nonprivileged user:
```
rpmdev-setuptree
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc.spec -o $HOME/rpmbuild/SPECS/lxc.spec
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc-net -o $HOME/rpmbuild/SOURCES/lxc-net
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc-2.0.7-fix-init.patch -o $HOME/rpmbuild/SOURCES/lxc-2.0.7-fix-init.patch
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc-4.0.1-fix-lxc-net.patch -o $HOME/rpmbuild/SOURCES/lxc-4.0.1-fix-lxc-net.patch
curl https://linuxcontainers.org/downloads/lxc/lxc-5.0.2.tar.gz -o $HOME/rpmbuild/SOURCES/lxc-5.0.2.tar.gz
pushd $HOME/rpmbuild/SPECS/
  rpmbuild -bb lxc.spec --define "with_liburing 1"
popd
```
## Binaries
Available at:
https://copr.fedorainfracloud.org/coprs/ppira/lxc/
