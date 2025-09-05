pkgname=freetype2
pkgver=2.13.3
pkgrel=2
pkgdesc="Font rasterization library"
arch=('x86_64')
url="https://www.freetype.org/"
license=('FTL OR GPL-2.0-or-later')
depends=(
    'bash'
    'brotli'
    'bzip2'
    'harfbuzz'
    'libpng'
    'which'
    'zlib'
)
source=(https://downloads.sourceforge.net/${pkgname/2/}/${pkgname/2/}-${pkgver}.tar.xz
    https://downloads.sourceforge.net/${pkgname/2/}/${pkgname/2/}-doc-${pkgver}.tar.xz)
sha256sums=(0550350666d427c74daeb85d5ac7bb353acba5f76956395995311a9c6f063289
    b7b66149bea769e226fd3d6d1eee6160e5b6beb4249b088071434fbe85fd1070)

prepare() {
    cd ${pkgname/2/}-${pkgver}

    sed -ri "s:.*(AUX_MODULES.*valid):\1:" modules.cfg

    sed -r "s:.*(#.*SUBPIXEL_RENDERING) .*:\1:" \
        -i include/freetype/config/ftoption.h
}

build() {
    cd ${pkgname/2/}-${pkgver}

    local configure_args=(
        --enable-freetype-config
        --with-zlib=yes
        --with-bzip2=yes
        --with-png=yes
        --with-brotli=yes
        --with-harfbuzz=yes
        --disable-static
        ${configure_options}
    )

    ./configure "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname/2/}-${pkgver}

    make DESTDIR=${pkgdir} install

    install -vdm755 ${pkgdir}/usr/share/doc/${pkgname/2/}-${pkgver}
    cp -v -R docs -T ${pkgdir}/usr/share/doc/${pkgname/2/}-${pkgver}
    rm -v ${pkgdir}/usr/share/doc/${pkgname/2/}-${pkgver}/freetype-config.1
}
