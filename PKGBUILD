# Maintainer: Olivier Farges <farges.olivier@gmail.com>

pkgname=sunswarm
pkgver=20131003
pkgrel=1
pkgdesc="Tool to optimize solar central receiver"
arch=('any')
url="http://www.starwest.ups-tlse.fr"
license=('GPL3')
depends=('starlight' 'gnuplot' 'texlive-core' 'texlive-bibtexextra' 'texlive-fontsextra' 'texlive-formatsextra' 'texlive-games' 'texlive-genericextra' 'texlive-htmlxml' 'texlive-humanities' 'texlive-latexextra' 'texlive-music' 'texlive-pictures' 'texlive-plainextra' 'texlive-pstricks' 'texlive-publishers' 'texlive-science')
makedepends=('git')
conflicts=()
provides=()
install=

source=()
md5sums=()

_gitroot="http://gitlab.red-pill.fr/sunswarm/sunswarm.git"
_gitname="sunswarm"

build() {
  
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."
  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  if [ "$GNUPLOT_DRIVER_DIR" == "" ]; then
    echo 'export GNUPLOT_DRIVER_DIR=/usr/bin' >> ~/.bashrc
    source ~/.bashrc
  fi
  cd "$srcdir/$_gitname-build"
  mkdir objs

  make

}

package() {
  cd "$srcdir/$_gitname-build"
  mkdir -p "$pkgdir/usr/bin"
  if [[ ! -d "$HOME/sunswarm" ]]; then
    mkdir -p "$HOME/$_gitname"
    cp $srcdir/$_gitname/run/* $HOME/$_gitname/
  fi
  cp $srcdir/$_gitname/run/settings.txt.template $HOME/$_gitname/settings.txt
  cp $srcdir/$_gitname/run/notice.txt $HOME/$_gitname/.
  make prefix="$pkgdir/usr" install
 }