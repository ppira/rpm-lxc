# rpm-lxc
Build lxc rpms for EL9

## Install build tools
```
dnf --enablerepo=crb install ninja-build
dnf install pip rpm-build rpmdevtools
pip install meson  # meson shipped with EL9 is too old
```

## Build RPM
```
rpmdev-setuptree
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc.spec -o $HOME/rpmbuild/SPECS/lxc.spec
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc-net -o $HOME/rpmbuild/SOURCES/lxc-net
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc-2.0.7-fix-init.patch -o $HOME/rpmbuild/SOURCES/lxc-2.0.7-fix-init.patch
curl https://raw.githubusercontent.com/ppira/rpm-lxc/main/lxc-4.0.1-fix-lxc-net.patch -o $HOME/rpmbuild/SOURCES/lxc-4.0.1-fix-lxc-net.patch
pushd $HOME/rpmbuild/SPECS/
  rpmbuild -bb lxc.spec
popd
```
