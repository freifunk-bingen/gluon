In diesem Verzeichnis wird die "Stable" Version gebacken.

Abh�ngigkeiten installieren:
apt-get install git subversion build-essential gawk unzip libncurses-dev libz-dev

Checkout der Original-Firmware
git clone https://github.com/freifunk-gluon/gluon.git gluon -b v2015.1.x

Im Verzeichnis "site/" site.conf und site.mk anlegen. Derzeit die von FFMZ:
https://github.com/freifunk-mwu/site-ffmwu
Dateien in site/i18n/anpassen (Text nach Router-Installation)

Anpassungen site.conf:
site_name = 'Freifunk Bingen'
ssid = 'Freifunk Bingen'
mirrors = { 'http://freifunk-bingen.de/firmware/stable/sysupgrade', -- combined (DNS) }

 pubkeys = {
 good-keys=1 # Es wird nur eine gültige Signatur gebraucht
...
'be8032ec4ddb4bbc0da9032dbec29372f24f7ca9af46186bceaccc2bcea9a93f', -- ffbin-stefan
...
}

Anpassungen site.mk:
Vorerst keine, später würde ich das Build-Datum aus dem Dateinamen herausnehmen und das Aktualisierungsintervall von 0 auf z.B. 3 Tage erhöhen



ECDSA -Keys zum signieren liegen in ~fwbuilder/ecdsakeys


cd ~fwbuilder/source/stable
make update                        # Get other repositories used by Gluon
make GLUON_TARGET=ar71xx-generic   # Build Gluon

Weitere Targets:
 * ar71xx-generic
 * ar71xx-nand
 * mpc85xx-generic
 * x86-generic
 * x86-kvm_guest

Das Makefile verlangt die version 1.0.2.c von openssl, unter der eingetragenen Adresse gibt es aber nur die Version 1.0.2.d. Die alte Version von
https://www.openssl.org/source/old/1.0.2/openssl-1.0.2c.tar.gz
herunterladen und nach openwrt/dl/ kopieren.

