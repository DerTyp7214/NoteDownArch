_pkgname=Notedown
pkgname=notedown-desktop
pkgver=1.0.7
pkgrel=1
pkgdesc="Notedown - Markdown editor for the desktop"
arch=('x86_64')
url="https://github.com/DerTyp7214/NoteDownElectron"
license=('MIT')
makedepends=('git' 'nodejs' 'npm' 'pnpm')

source=("git+https://github.com/DerTyp7214/NoteDownElectron.git")
sha256sums=('SKIP')

provides=("notedown-desktop")

prepare() {
    cd "${srcdir}/NoteDownElectron"
    # If there's a specific tag you want to build, checkout here:
    # git checkout v${pkgver}
    git submodule update --init --recursive
    pnpm install
}

build() {
    cd "${srcdir}/NoteDownElectron"
    pnpm run build:unpack
}

package() {
    install -Dm755 -d "${pkgdir}/usr/bin"                  # Create the directory
    install -Dm755 -d "${pkgdir}/usr/share/icons"          # Create the directory
    install -Dm755 -d "${pkgdir}/usr/share/applications"   # Create the directory
    install -Dm755 -d "${pkgdir}/usr/lib/notedown-desktop" # Create the directory

    # Install the contents of the linux-unpacked directory
    cp -r "${srcdir}/NoteDownElectron/dist/linux-unpacked/." "${pkgdir}/usr/lib/notedown-desktop"

    # Create a symlink to the executable
    ln -s "${pkgdir}/usr/lib/notedown-desktop/notedown" "${pkgdir}/usr/bin/notedown-desktop" # Link to 'notedown'

    install -Dm644 "${srcdir}/NoteDownElectron/resources/icon.png" "${pkgdir}/usr/share/icons/notedown.png"

    #install -Dm755 "${srcdir}/NoteDownElectron/dist/notedown-${pkgver}.AppImage" "${pkgdir}/usr/bin/notedown-desktop"
    # Optional: Install a .desktop file if available or create one
    install -Dm644 "${startdir}/Notedown.desktop" "${pkgdir}/usr/share/applications/notedown-desktop.desktop"
}
