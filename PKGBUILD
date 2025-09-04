# Maintainer: Your Name <your.email@example.com>
pkgname=pin-hwmon
pkgver=1.0.0
pkgrel=1
pkgdesc="Pin hwmon paths for stable CPU/GPU temperature access"
arch=('x86_64')
url="https://github.com/user/pin-hwmon"
license=('MIT')
depends=('bash' 'systemd' 'awk' 'coreutils')
optdepends=('waybar: display the temp using the helper script'
            'lm_sensors: additional hwmon tools')
install='pin-hwmon.install'
source=('pin-hwmon'
        'pin-hwmon.service'
        'cpu-temp-waybar'
        'LICENSE'
        'README.md')
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP')

package() {
  install -Dm755 pin-hwmon "$pkgdir/usr/bin/pin-hwmon"
  install -Dm755 cpu-temp-waybar "$pkgdir/usr/bin/cpu-temp-waybar"
  install -Dm644 pin-hwmon.service "$pkgdir/usr/lib/systemd/system/pin-hwmon.service"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}
