# Maintainer: PapyElGringo <adrien@pesler.be>
pkgname=veshell-git
pkgver=alpha.1.r135.gd613d93
pkgrel=1
pkgdesc="An innovative not-desktop environment for Linux made with modern technologies like Flutter and Rust."
arch=('x86_64' 'aarch64')
url="https://github.com/free-explorers/veshell"
license=('GPL3')
depends=(
  'fontconfig'
  'libseat.so'
  'libinput'
  'libxcb'
  'libxkbcommon'
  'mesa'
  'pixman'
  'systemd'
  'wayland'
)
makedepends=(
    'cargo' 
    'git'
)
source=("git+https://github.com/free-explorers/veshell.git")
sha256sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  export CARGO_HOME=${srcdir}/${pkgname%-git}/.cargo    # Use downloaded earlier from src directory, not from ~/.cargo
  export CARGO_TARGET_DIR=target                        # Place the output in target relative to the current directory
  cd ${pkgname%-git}
  cargo build --release
}

package() {
  cd ${pkgname%-git}

  install -Dm755 target/release/${pkgname%-git}                    -t ${pkgdir}/usr/bin/
  install -Dm755 extra/assets/${pkgname%-git}-session                    -t ${pkgdir}/usr/bin/
  install -Dm644 extra/assets/${pkgname%-git}.desktop                    -t ${pkgdir}/usr/share/wayland-sessions/
  install -Dm644 extra/assets/${pkgname%-git}-portals.conf               -t ${pkgdir}/usr/share/xdg-desktop-portal/
  install -Dm644 extra/assets/${pkgname%-git}{.service,-shutdown.target} -t ${pkgdir}/usr/lib/systemd/user/
}
