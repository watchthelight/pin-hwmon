# Maintainer: watchthelight
pkgname=pin-hwmon
pkgver=1.0.0
pkgrel=1
arch=('any')
depends=('bash' 'coreutils' 'awk' 'systemd')
optdepends=('waybar: show temps with helper' 'lm_sensors: extra tools')
license=('MIT')
install='pin-hwmon.install'
source=('pin-hwmon' 'cpu-temp-waybar' 'pin-hwmon.service' 'LICENSE' 'README.md')
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')

package() {
  install -Dm755 "${srcdir}/pin-hwmon" "${pkgdir}/usr/bin/pin-hwmon"
  install -Dm755 "${srcdir}/cpu-temp-waybar" "${pkgdir}/usr/bin/cpu-temp-waybar"
  install -Dm644 "${srcdir}/pin-hwmon.service" "${pkgdir}/usr/lib/systemd/system/pin-hwmon.service"
  install -Dm644 "${srcdir}/README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -Dm644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}