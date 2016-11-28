pkgname=eclipse-pleiades
pkgver=1.7.0
pkgrel=1
pkgdesc="A task-focused interface for Eclipse"
arch=('any')
url="https://eclipse.org/mylyn/"
license=('EPL')
depends=('eclipse')
optdepends=('bugzilla: ticketing support')
source=(https://osdn.jp/dl/mergedoc/pleiades_${pkgver}.zip)
md5sums=('d177f92cb0f9aea5ba665d4cf3814347')

prepare() {
  # remove features and plug-ins containing sources
  rm -f features/*.source_*
  rm -f plugins/*.source_*
  # remove gz files
  rm -f plugins/*.pack.gz
}

package() {
  _dest="${pkgdir}/usr/lib/eclipse/dropins/${pkgname/eclipse-}/eclipse"

  # Features
  find features -type f | while read -r _feature ; do
    if [[ "${_feature}" =~ (.*\.jar$) ]] ; then
      install -dm755 "${_dest}/${_feature%*.jar}"
      cd "${_dest}/${_feature/.jar}"
      # extract features (otherwise they are not visible in about dialog)
      jar xf "${srcdir}/${_feature}" || return 1
    else
      install -Dm644 "${_feature}" "${_dest}/${_feature}"
    fi
  done

  # Plugins
  find plugins -type f | while read -r _plugin ; do
    install -Dm644 "${_plugin}" "${_dest}/${_plugin}"
  done
}
