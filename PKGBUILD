# Maintainer: thebastl
# Contributor: Det
# Contributor: Achilleas Pipinellis <axilleas@archlinux.info>
# Contributor: speed145a <speed145a(at)hotmail(dot)com>
# Contributor: Schnouki

pkgname=firefox-beta-bin-de
_basever=34.0b10
#_rc=2
#pkgver=${_basever}rc${_rc}
#pkgver=33.0b9
pkgver=${_basever}
pkgrel=1
pkgdesc="Standalone web browser from mozilla.org - German Beta (All the hard work is done by Det -> firefox-beta-bin)"
arch=('i686' 'x86_64')
url="https://www.mozilla.org/de/firefox/"
license=('MPL' 'GPL' 'LGPL')
depends=('alsa-lib' 'dbus-glib' 'desktop-file-utils' 'gtk2' 'hicolor-icon-theme'
         'icu' 'libevent' 'libvpx' 'libxt' 'mime-types' 'nss' 'sqlite')
optdepends=('gst-plugins-base: vorbis decoding, ogg demuxing'
            'gst-plugins-good: webm and mp4 demuxing'
            'gst-plugins-bad: aac, vp8 and opus decoding'
            'gst-plugins-ugly: h.264 and mp3 decoding'
            'gst-libav: more decoders'
            'libpulse: PulseAudio driver'
            'networkmanager: Location detection via available WiFi networks')
_arch=x86_64  # Workaround for mkaurball: https://bugs.archlinux.org/task/40711
[[ $CARCH = i686 ]] && _arch=i686
install=$pkgname.install
#source=("https://ftp.mozilla.org/pub/mozilla.org/firefox/candidates/$_basever-candidates/build$_rc/linux-$_arch/de/firefox-$_basever.tar.bz2"
source=("https://ftp.mozilla.org/pub/mozilla.org/firefox/releases/$pkgver/linux-$_arch/de/firefox-$pkgver.tar.bz2"
        "$pkgname.desktop"
        "$pkgname-safe.desktop")
#md5sums=(`curl -sL ${source/.t*}.checksums | grep tar | grep md5 | cut -d " " -f1`
md5sums=(`curl -sL ${source/li*}/MD5SUMS | grep linux-$_arch/de | grep tar | cut -d ' ' -f1`
          '9fb9aa7aa37f7e8bb5caa54356159ba4'
          'c391a9cf84de505b3b977de2e5d259b1')
          
package() {
  # Create directories
  mkdir -p "$pkgdir"/{usr/{bin,share/{applications,icons/hicolor/128x128/apps}},opt}

  # Install
  cp -r firefox/ "$pkgdir"/opt/$pkgname-$pkgver

  # /usr/bin link
  ln -s /opt/$pkgname-$pkgver/firefox "$pkgdir"/usr/bin/$pkgname

  # Desktops
  install -m644 *.desktop "$pkgdir"/usr/share/applications/

  # Icons
  for i in 16 32 48; do
    install -d "$pkgdir"/usr/share/icons/hicolor/${i}x$i/apps/
    ln -s /opt/$pkgname-$pkgver/browser/chrome/icons/default/default$i.png \
          "$pkgdir"/usr/share/icons/hicolor/${i}x$i/apps/$pkgname.png
  done

  ln -s /opt/$pkgname-$pkgver/browser/icons/mozicon128.png \
        "$pkgdir"/usr/share/icons/hicolor/128x128/apps/$pkgname.png
}
