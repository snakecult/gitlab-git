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

_gitroot="git://gitorious.org/gitorious/mainline.git"
_gitname="gitorious"

build() {
	if [ ! -d "gitlabhq" ] 
	then
		git clone https://github.com/gitlabhq/gitlabhq.git
	fi
	cd gitlabhq
	bundle install --without development test --deployment
}

package() {
	echo x
}
