# Maintainer: watchthelight
pkgname=pin-hwmon
pkgver=1.1.0
pkgrel=1
arch=('any')
depends=('bash' 'coreutils' 'awk' 'sed' 'grep' 'systemd')
optdepends=('waybar: show temps with helper' 'lm_sensors: extra tools' 'prometheus-node-exporter: textfile collector')
license=('MIT')
install='pin-hwmon.install'
source=(
  'pin-hwmon'
  'pin-hwmonctl'
  'cpu-temp-waybar'
  'gpu-temp-waybar'
  'temps-waybar'
  'pin-hwmon-metrics'
  'pin-hwmon.service'
  'pin-hwmon.path'
  'pin-hwmon-metrics.service'
  'pin-hwmon-metrics.timer'
  '99-pin-hwmon.rules'
  'pin-hwmon.tmpfiles'
  'pin-hwmon.hook'
  'system-sleep/pin-hwmon'
  'LICENSE'
  'README.md'
  'man/pin-hwmon.1'
  'man/pin-hwmonctl.1'
  'pin-hwmon.conf.example'
)
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')

package() {
  install -Dm755 "${srcdir}/pin-hwmon" "${pkgdir}/usr/bin/pin-hwmon"
  install -Dm755 "${srcdir}/pin-hwmonctl" "${pkgdir}/usr/bin/pin-hwmonctl"
  install -Dm755 "${srcdir}/cpu-temp-waybar" "${pkgdir}/usr/bin/cpu-temp-waybar"
  install -Dm755 "${srcdir}/gpu-temp-waybar" "${pkgdir}/usr/bin/gpu-temp-waybar"
  install -Dm755 "${srcdir}/temps-waybar" "${pkgdir}/usr/bin/temps-waybar"
  install -Dm755 "${srcdir}/pin-hwmon-metrics" "${pkgdir}/usr/bin/pin-hwmon-metrics"

  install -Dm644 "${srcdir}/pin-hwmon.service" "${pkgdir}/usr/lib/systemd/system/pin-hwmon.service"
  install -Dm644 "${srcdir}/pin-hwmon.path" "${pkgdir}/usr/lib/systemd/system/pin-hwmon.path"
  install -Dm644 "${srcdir}/pin-hwmon-metrics.service" "${pkgdir}/usr/lib/systemd/system/pin-hwmon-metrics.service"
  install -Dm644 "${srcdir}/pin-hwmon-metrics.timer" "${pkgdir}/usr/lib/systemd/system/pin-hwmon-metrics.timer"

  install -Dm644 "${srcdir}/99-pin-hwmon.rules" "${pkgdir}/usr/lib/udev/rules.d/99-pin-hwmon.rules"
  install -Dm644 "${srcdir}/pin-hwmon.tmpfiles" "${pkgdir}/usr/lib/tmpfiles.d/pin-hwmon.conf"
  install -Dm755 "${srcdir}/system-sleep/pin-hwmon" "${pkgdir}/usr/lib/systemd/system-sleep/pin-hwmon"

  install -Dm644 "${srcdir}/pin-hwmon.hook" "${pkgdir}/usr/share/libalpm/hooks/pin-hwmon.hook"

  install -Dm644 "${srcdir}/man/pin-hwmon.1" "${pkgdir}/usr/share/man/man1/pin-hwmon.1"
  install -Dm644 "${srcdir}/man/pin-hwmonctl.1" "${pkgdir}/usr/share/man/man1/pin-hwmonctl.1"

  install -Dm644 "${srcdir}/README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -Dm644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  install -Dm644 "${srcdir}/pin-hwmon.conf.example" "${pkgdir}/usr/share/pin-hwmon/pin-hwmon.conf.example"
}