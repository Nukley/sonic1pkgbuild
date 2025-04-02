pkgname=sonicthehedgehog
_pkgname=SonicTheHedgehog
pkgver=1.0.2
pkgrel=1
pkgdesc="Sonic the Hedgehog game powered by the rsdkv4 engine."
arch=('x86_64' 'aarch64' 'i686')
url="https://github.com/Nukley/sonicthehedgehog"
license=('GPL')
depends=('rsdkv4-git' 'libogg' 'libvorbis' 'wget' 'sdl2' 'unzip' 'yad')
makedepends=('unzip')
source=("https://github.com/Nukley/sonicthehedgehog/releases/download/1.0.2-2/sonicthehedgehog-1.0.2-2.tar")
sha256sums=('abc88a5088bf31326775bcada8d676386777da82f4d9cc39cf5ef77f95a1284a')

package() {
    install -dm755 "$pkgdir/usr/bin"
    install -dm775 "$pkgdir/usr/share/games/$_pkgname"
    install -dm755 "$pkgdir/usr/share/pixmaps"

    # Packaging files
       

    # Check if Data.rsdk exists so it doesn't redownload the file when it doesn't need to.
    FILE="/usr/share/games/$_pkgname/Data.rsdk"
     if test -f "$FILE"
    then
        echo "$FILE exists skipping download."
        cp -r "/usr/share/games/$_pkgname/Data.rsdk" "$pkgdir/usr/share/games/$_pkgname"
    else
        echo "$FILE does not exist, Starting download.."
        cd $srcdir/sonicthehedgehog-$pkgver
        wget "https://archive.org/download/data_20231229_202312/Data.rsdk"
    fi

    cd $srcdir/$pkgname-$pkgver
    cp "$srcdir/$pkgname-$pkgver/sonic.sh" "$pkgdir/usr/bin/sonic"
    cp -r ./ "$pkgdir/usr/share/games/$_pkgname"
    cp sonic.png "$pkgdir/usr/share/pixmaps"

    # Desktop Entry
    install -Dm644 "$srcdir/$pkgname-$pkgver/$_pkgname.desktop" \
    "$pkgdir/usr/share/applications/$_pkgname.desktop"
    sed -i s%/usr/share%/opt% "$pkgdir/usr/share/applications/$_pkgname.desktop"
}
