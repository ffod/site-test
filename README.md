# Freifunk Stormarn Site-Konfiguration

In diesem Repository wird die Gluon Konfiguration für Freifunk Stormarn gepflegt.

## Neuen Dinge hinzufügen

Wenn du etwas Neues zur Konfiguration hinzufügen willst, wie zum Beispiel einen Schlüssel, dann benutze dafür bitte den Master Branch.

## Eine Version hat einen Fehler

Dann behebe den Fehler in dem entsprechenden Branch, ob die Änderungen in Master übernommen werden, prüfen wir später.



## Script Beispiel zum automatischen Erstellen:
#!/bin/bash
start=$(date +%s)
CORES=$(expr $(nproc) + 1)
RELEASE=2017.1.4+t$(date +"%Y%m%d")
BRANCH=testing
make update GLUON_RELEASE=$RELEASE
for TARGET in ar71xx-generic ar71xx-tiny ar71xx-nand brcm2708-bcm2708 brcm2708-bcm2709 mpc85xx-generic x86-generic x86-geode x86-64; do
        echo "################# $(date) start building target $TARGET #################"
        make -j$CORES GLUON_TARGET=$TARGET GLUON_RELEASE=$RELEASE GLUON_BRANCH=$BRANCH || exit 1
done
echo "alle Targets wurden erfolgreich erstellt"
echo -n "finished: "; date
echo "Dauer: $((($(date +%s)-start)/60)) Minuten"
