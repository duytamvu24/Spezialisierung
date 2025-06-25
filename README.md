# Spezialisierung
Zur Auswertung und Korrelation der Spirometriedaten mit den Bild-Daten aus der Echtzeit-Kardio-Bildgebung mit Kombination eines Ergometers. Die Analyse besteht aus 3 Skripten.
1. Spiromodul: Aus den Spirometriedaten werden weiterführende 
2.1 Korrelation der Spirometrie-Daten mit den EKG-Daten: Die EKG-Daten hat die selbe Abtastrate und LogZeiten wie die Bilder. Eine Korrelation hier ermöglicht es dann auch eine Korrelation zu den Bildern.
2.2 Finetuning: Durch die Korrelation im ersten Schritt werden die relevanten Abschnitte aus der Spirometriedatei gespeichert. Diese können nun mit dem Bauchgurt und einer Signalintensitätskurve aus einer Schicht verglichen werden. Falls nötig können die Spirometriedaten noch genauer mit den Bilddaten korreliert werden.
3. Reinschreiben in die DICOM: Nach Korrelation werden die Spiroergometriedaten (Atemvolumen und Atemfluss) für jedes Bild in die DICOM-Dateien reingeschrieben. Die Atemfluss-, Atemvolumen- und EKG-Daten werden zum Filtern der Bilder genutzt, um Bilder (hier) aus der Endexspiration in 25 verschiedenen EKG-Klassen zu bekommen. Diese Auswahl an Bildern kann dann für weitere Auswertungen in Circle genutzt werden.

# Input-Daten:
Spirometriedatei, beinhaltet Atemfluss, O2-, CO2-Volumenanteil und die Logzeit
EKG-Datei, beinhaltet 4 Ableitungen
Bauchgurtdatei
Bilddaten der Echtzeitbildgebung, transponiert mit Hilfe vom Dicom-Translator von Ludger Radke

# Output-Daten:
- Aus dem Spiromodul kommt eine Excel mit ausgewerteten Parametern bzgl. der Spiroergometrie heraus
- Satz von korrelierten, auf Endexspiration gefilterte Bilddaten für jede EKG-Klasse
