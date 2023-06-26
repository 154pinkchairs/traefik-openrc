# Maintainer: Marcelina Hołub <mholub@tutanota.com>

pkgname=traefik-openrc
pkgver=1.0.0
pkgrel=1
pkgdesc="Modern reverse proxy and load balancer (OpenRC init script)"
arch=('any')
url="https://traefik.io/"
license=('MIT')
depends=('openrc' 'traefik')
source=("https://github.com/154pinkchairs/traefik-openrc/archive/traefik-openrc-v${pkgver}.tar.gz")
sha256sums=('974398b2f291a5a1f96369a58279e7779ef70945a1cbf2244b348b66a794bc4b')

package() {
	cd "$srcdir"

	# Copy the init script and configuration
	install -Dm755 traefik "$pkgdir/etc/init.d/traefik"
	install -Dm644 traefik.confd "$pkgdir/etc/conf.d/traefik"
	install -Dm644 traefik.yaml "$pkgdir/etc/traefik/traefik.yaml" || true

	# Create the user and group
	getent group traefik >/dev/null || groupadd -r traefik
	getent passwd traefik >/dev/null ||
		useradd -r -m -g traefik -d /var/empty -s /usr/bin/nologin -c "Traefik" traefik

	# Create the log directory
	install -d -m 0775 -o traefik -g traefik "$pkgdir/var/log/traefik" || return 1
}
