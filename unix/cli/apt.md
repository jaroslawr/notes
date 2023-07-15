# apt

Update package information:

    apt update

Upgrade existing packages, except upgrades requiring removal of an existing
package:

    apt upgrade

Upgrade existing packages, including upgrades requiring removal of an existing
package:

    apt full-upgrade

List packages matching "fonts":

    apt list "*fonts*"

List all available packages matching "fonts":

    apt list -a "*fonts*"

List all available versions of package golang:

    apt list -a golang

List all installed packages matching "fonts":

    apt list -i "*fonts*"

Remove all packages matching golang:

    apt remove "*golang*"

