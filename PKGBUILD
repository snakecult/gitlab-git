# Maintainer: David Andersen <arch@davidandersen.us>
pkgname=gitlab-git
pkgver=5.0.0pre
pkgrel=1
pkgdesc="Gitorious aims to provide a great way of doing distributed opensource code collaboration (git version)"
arch=(i686 x86_64)
url="http://gitorious.org/gitorious"
license=('AGPLv3')
 
depends=('ruby-bundler' 
         'gitlab-shell'
         'nginx'
         'icu'
)
makedepends=('git' 'postgresql-libs' 'libmysqlclient')
optdepends=(
	'postgres'
	'mysql'	)

backup=('etc/gitlab/gitlab.yml'
        'etc/gitlab/database.yml')
#options=('!strip')
build() {
	if [ ! -d "gitlab" ] 
	then
		git clone https://github.com/gitlabhq/gitlabhq.git gitlab --depth=1
	fi
	cd gitlab
	bundle install --without development test --deployment
}

_homedir="$pkgdir/home/git/gitlab"
_etc="$pkgdir/etc/gitlab"

package() {
    #gitlab
    mkdir -p "$_homedir"
    cp -rT "$srcdir/gitlab" "$_homedir"
    rm -rf "$_homedir/.git"
    rm  "$_homedir/.gitignore"
    chown -R git:git "$_homedir"

    #config
    install -Dm0644 "$srcdir/gitlab/config/database.yml.postgresql" "$_etc/database.yml"
    install -Dm0644 "$srcdir/gitlab/config/gitlab.yml.example" "$_etc/gitlab.yml"
    ln -s "/etc/gitlab/database.yml" "$_homedir/config/database.yml"
    ln -s "/etc/gitlab/config.yml" "$_homedir/config/config.yml"

    #systemd
    install -D -m0644 "$startdir/gitlab.service" "$pkgdir/usr/lib/systemd/system"
    install -D -m0644 "$startdir/sidekiq.service" "$pkgdir/usr/lib/systemd/system"

    #nginx
    install -D -m0644 "$startdir/gitlab.conf" "$pkgdir/etc/nginx/sites-enabled"
}
