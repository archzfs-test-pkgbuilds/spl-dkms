# Maintainer: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
#
pkgname="spl-dkms"
pkgdesc="Solaris Porting Layer kernel modules."

pkgver=0.7.8
pkgrel=1
makedepends=("git")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("https://github.com/zfsonlinux/zfs/releases/download/zfs-0.7.8/spl-0.7.8.tar.gz"
        "60-spl-dkms-install.hook"
        "spl-dkms-alpm-hook")
sha256sums=("f6c9fe37d149da7fec34ee3bf32302a16b4cfcd84b8c6aa3d764ceb816587636"
            "15f71a9ceccf795cdac65743bee338e9987ec77e217721f32d55099be6ecf3d7"
            "836002f310b9e1d4b1a0e5c30d5b0ac5aa120d335b3ea223228a0b9f037ef8b8")
license=("GPL")
depends=("spl-utils-common=0.7.8" "dkms")
provides=("spl")
groups=("archzfs-dkms")
conflicts=('spl-dkms-git' 'spl-archiso-linux' 'spl-archiso-linux-git' 'spl-linux-hardened' 'spl-linux-hardened-git' 'spl-linux-lts' 'spl-linux-lts-git' 'spl-linux' 'spl-linux-git' 'spl-linux-vfio' 'spl-linux-vfio-git' 'spl-linux-zen' 'spl-linux-zen-git'  )

build() {
    cd "${srcdir}/spl-0.7.8"
    ./autogen.sh
}

package() {
    # install alpm hook
    install -D -m 644 ${srcdir}/60-spl-dkms-install.hook ${pkgdir}/usr/share/libalpm/hooks/60-spl-dkms-install.hook
    install -D -m 755 ${srcdir}/spl-dkms-alpm-hook ${pkgdir}/usr/lib/dkms/spl-dkms-alpm-hook
    dkmsdir="${pkgdir}/usr/src/spl-0.7.8"
    install -d "${dkmsdir}"
    cp -a ${srcdir}/spl-0.7.8/. ${dkmsdir}
    cd "${dkmsdir}"
    find . -name ".git*" -print0 | xargs -0 rm -fr --
    scripts/dkms.mkconf -v 0.7.8 -f dkms.conf -n spl
    chmod g-w,o-w -R .
}
