# Maintainer: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>

pkgname=gitlab-git
pkgver=20130311
pkgrel=1
pkgdesc="Gitorious aims to provide a great way of doing distributed opensource code collaboration (git version)"
arch=(i686 x86_64)
url="http://gitorious.org/gitorious"
license=('AGPLv3')

depends=('ruby-bundler')
makedepends=('git' 'postgresql-libs' 'libmysqlclient' )
optdepends=(
	'postgres'
	'mysql'	)

backup=('home/git/gitlab/config/gitlab.yml'
        'home/git/gitlab/config/database.yml')

build() {
	if [ ! -d "gitlab" ] 
	then
		git clone https://github.com/gitlabhq/gitlabhq.git gitlab
	fi
	cd gitlab
	bundle install --without development test --deployment
}

package() {
	pwd
	install -vdD "$pkgdir/home/gitlab"	
	cp -r "$srcdir/gitlab" "$pkgdir/home/git/gitlab"	
	cp "$srcdir/gitlab/config/database.yml.postgressql" "$pkgdir/gitlab/config/database.yml"
	cp "$srcdir/gitlab/config/config.yml.example" "$pkgdir/gitlab/config/config.yml"
}
