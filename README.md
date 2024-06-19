"# unraidsortierscript" 
#!/bin/bash

# Pfade anpassen
QUELLORDNER="Quellpfad"
ZIELORDNER_R="Pfad_Ordenr_F"
ZIELORDNER_F="Pfad_Ordner_F"

# Erstelle die Zielordner, falls sie noch nicht existieren
mkdir -p "$ZIELORDNER_R"
mkdir -p "$ZIELORDNER_F"

# Durchlaufe alle Dateien im Quellordner
for DATEI in "$QUELLORDNER"/*; do
    if [ -f "$DATEI" ]; then
        DATEINAME=$(basename "$DATEI")
        
        # Extrahiere den vorletzten Buchstaben des Dateinamens (R oder F)
        LETZTER_BUCHSTABE="${DATEINAME: -5:1}"  # Prüfen des vorletzten Buchstabens

        echo "Bearbeite Datei: $DATEINAME"

        if [ "$LETZTER_BUCHSTABE" == "R" ]; then
            echo "Verschiebe Datei $DATEINAME nach $ZIELORDNER_R"
            mv "$DATEI" "$ZIELORDNER_R/"
        elif [ "$LETZTER_BUCHSTABE" == "F" ]; then
            echo "Verschiebe Datei $DATEINAME nach $ZIELORDNER_F"
            mv "$DATEI" "$ZIELORDNER_F/"
        else
            echo "Datei $DATEINAME passt nicht zu 'R' oder 'F'. Überspringe."
        fi
    fi
done

echo "Dateien wurden sortiert."
