# Maintainer: David Andersen <arch@davidandersen.us>
pkgname=gitlab-git
pkgver=5.0.0
pkgrel=6
pkgdesc="Self hosted Git management software"
arch=(x86_64)
url="http://gitlab.org"
license=('MIT')
install='gitlab.install'
depends=(
	'ruby-bundler'
	'gitlab-shell'
	'nginx'
	'icu'
	'redis'
	'libxslt'
	'git'
	'postgresql-libs'
	'libmysqlclient'
)

optdepends=(
	'postgres'
	'mysql'
)

provides=('gitlab')

backup=(
	'etc/gitlab/gitlab.yml'
	'etc/gitlab/database.yml'
	'etc/nginx/sites-enabled/gitlab.conf'
)

#options=('!strip')

_branch=5-0-stable
build() {
	if [ ! -d "gitlab" ]
	then
		git clone -b $_branch https://github.com/gitlabhq/gitlabhq.git gitlab
	fi

	cd gitlab
	bundle install --without development test --deployment
}

_homedir="home/git/gitlab"
_etc="etc/gitlab"
package() {
	#gitlab
	mkdir -p "$pkgdir/$_homedir"
	mkdir -p "$pkgdir/$_homedir/tmp/pids"
	mkdir -p "$pkgdir/$_homedir/tmp/sockets"
	cp -rT "$srcdir/gitlab" "$pkgdir/$_homedir"
	#    rm -rf "$pkgdir/$_homedir/.git"
	rm  "$pkgdir/$_homedir/.gitignore"
	chmod 750 "$pkgdir/$_homedir"
	chown -R git:git "$pkgdir/$_homedir"

	#config
	install -Dm0644 "$srcdir/gitlab/config/database.yml.postgresql" "$pkgdir/$_etc/database.yml"
	install -Dm0644 "$srcdir/gitlab/config/gitlab.yml.example" "$pkgdir/$_etc/gitlab.yml"
	ln -s "/etc/gitlab/database.yml" "$pkgdir/$_homedir/config/database.yml"
	ln -s "/etc/gitlab/gitlab.yml" "$pkgdir/$_homedir/config/gitlab.yml"

	#systemd
	install -D -m0644 "$startdir/gitlab.service" "$pkgdir/usr/lib/systemd/system/gitlab.service"
	install -D -m0644 "$startdir/sidekiq.service" "$pkgdir/usr/lib/systemd/system/sidekiq.service"

	#nginx
	install -D -m0644 "$startdir/gitlab.conf" "$pkgdir/etc/nginx/sites-enabled/gitlab.conf"
}
