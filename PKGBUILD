# Maintainer: AwesomeHaircut <jesusbalbastro@gmail com>
# Contributor: James An <james@jamesan.ca>
# Contributor: Rein Fernhout <public@reinfernhout.xyz>
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Artem Klevtsov <a.a.klevtsov@gmail.com>

_pkgbase=droidcam
pkgname=(droidcam-bin droidcam-dkms)
pkgver=6.7.5
pkgrel=3
pkgdesc="A tool for using your android device as a wireless/usb webcam"
arch=('x86_64')
url="https://www.dev47apps.com/${_pkgbase}/linuxx"
license=('GPL2')
provides=("${_pkgbase}")
source=("dkms.conf"
        "https://github.com/aramg/${_pkgbase}/raw/master/linux/icon2.png"
        "${_pkgbase}.desktop"
        "Makefile.dkms")
source_i686=("${_pkgbase}.tar.bz2::https://www.dev47apps.com/files/linux/${_pkgbase}_081219_32bit.tar.bz2")
source_x86_64=("${_pkgbase}.tar.bz2::https://www.dev47apps.com/files/linux/${_pkgbase}_081219_64bit.tar.bz2")
md5sums=('9d811a64aed6e972e0a65afa339b8e34'
         '0f0e1d04146dd5be70d5028f144bd0a2'
         '22b9912d96bc7691dfb6b7f82ec0306d'
         '8ec96444a042560a00affa7ce1b4fac4')
md5sums_x86_64=('eb676cd06c92a722ab8b3c4c771baf94')
sha512sums=('48fc8360c2e5defbc510f6cb7bbbbd1ccff5f1bf2e8f38df5cfc336b34a0613880de8b25dff424fdbe1b775c224248db6bd1dc045fc29d0788fe16df68af0067'
            '4cedbc823498a1ff70f6df1d312f29fa609c1316d15bbc8a23c5aa5055b87cb2d156e6da12aefa0195e1adbe65b94e6a79ae799083f9da4a959c21796280c491'
            '38e7e987e71696a209dde7cafe03e0910606d0dfd45aa1829910cbc40a336464bc8299c4fef0a32f0f74914537704f242331f8dae55cdf1884291866ea8a1e4c'
            'cc85312b0c2a2f8eeb39fb66e01da78d797f308d2289d7718fe1fabe8133aa8a7c45f8e113fa6c5fde551267a07c27434aff255e820cc8b7b90f8642cc2be870')
sha512sums_x86_64=('8dc04ed0993ce26dd64161b2d8b2ca434d0773528ef992ab865891e1b367e8f717cb50065c8e877c4d4d481530225cb62235cfe292bc9b7fbe918d8fc5ab2b5d')

prepare() {
  # Extract source from within leading arch-specific folder
  tar --transform='s/-\(32\|64\)bit//' --show-transformed-names -xjf "${_pkgbase}.tar.bz2"
}

package_droidcam-dkms() {
  depends=('dkms')
  # Copy dkms.conf
  install -Dm644 dkms.conf "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"

  # Set name and version
  sed -e "s/@_PKGBASE@/${_pkgbase}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"

  # Copy sources (including Makefile)
  install -Dm644 "${srcdir}/Makefile.dkms" "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/Makefile"
  install -Dm644 "${srcdir}/${_pkgbase}/v4l2loopback/v4l2loopback-dc.c" "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/v4l2loopback-dc.c"
}

package_droidcam-bin() {
  depends=('droidcam-dkms')

  # Install droidcam program files
  install -Dm755 "${srcdir}/${_pkgbase}/${_pkgbase}" "${pkgdir}/usr/bin/${_pkgbase}"
  install -Dm755 "${srcdir}/${_pkgbase}/${_pkgbase}-cli" "${pkgdir}/usr/bin/${_pkgbase}-cli"
  install -Dm644 "${srcdir}/${_pkgbase}/README" "${pkgdir}/usr/share/licenses/${_pkgbase}/LICENSE"
  install -Dm644 "${srcdir}/icon2.png" "${pkgdir}/usr/share/pixmaps/${_pkgbase}.png"
  install -Dm644 "${srcdir}/${_pkgbase}.desktop" "${pkgdir}/usr/share/applications/${_pkgbase}.desktop"

  # Set version on the desktop file
  sed -e "s/@PKGVER@/${pkgver}/" -i "${pkgdir}/usr/share/applications/${_pkgbase}.desktop"
}
