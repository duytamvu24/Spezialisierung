# Spezialisierung
Zur Auswertung und Korrelation der Spirometriedaten mit den Bild-Daten aus der Echtzeit-Kardio-Bildgebung mit Kombination eines Ergometers. Die Analyse besteht aus 3 Skripten.
1. Spiromodul: Aus den Spirometriedaten werden weiterführende Parameter berechnet
2.1 Korrelation der Spirometrie-Daten mit den EKG-Daten: Die EKG-Daten hat die selbe Abtastrate und LogZeiten wie die Bilder. Eine Korrelation hier ermöglicht es dann auch eine Korrelation zu den Bildern.
2.2 Finetuning: Durch die Korrelation im ersten Schritt werden die relevanten Abschnitte aus der Spirometriedatei gespeichert. Diese können nun mit dem Bauchgurt und einer Signalintensitätskurve aus einer Schicht verglichen werden. Falls nötig können die Spirometriedaten noch genauer mit den Bilddaten korreliert werden.
3. Reinschreiben in die DICOM: Nach Korrelation werden die Spiroergometriedaten (Atemvolumen und Atemfluss) für jedes Bild in die DICOM-Dateien reingeschrieben. Die Atemfluss-, Atemvolumen- und EKG-Daten werden zum Filtern der Bilder genutzt, um Bilder (hier) aus der Endexspiration in 25 verschiedenen EKG-Klassen zu bekommen. Diese Auswahl an Bildern kann dann für weitere Auswertungen in Circle genutzt werden.

# 1. Spiromodul:
Aus den Spirometriedaten werden weiterführende Parameter jeweils in der Ruhe- und Belastungsphase berechnet. Dies geschieht durch Erkennung der jeweiligen Peaks und Valleys, welche dann zu durchschnittlichen Werten, oder zur Bestimmung der Atemfrequenz genutzt werden. 
# Input-Daten:
Spirometriedatei, beinhaltet Atemfluss, O2-, CO2-Volumenanteil und die Logzeit

# Output-Daten:
- Aus dem Spiromodul kommt eine Excel mit ausgewerteten Parametern bzgl. der Spiroergometrie heraus
- durchschnittliches Atemzugvolumen, Atemminutenvolumen, maximaler- und minimaler O2-Volumenanteil, maximales- und minimaler CO2-Volumenanteil, Atemfrequenz

# 2. Korrelation der Spirometrie- und EKG-Daten:
Die EKG-Daten hat die selbe Abtastrate und LogZeiten wie die Bilder. Eine Korrelation hier ermöglicht es dann auch eine Korrelation zu den Bildern. Die Korrelation erfolgt durch die Erkennung von manuellen Zeitstempeln, die am Anfang der Messung "eingezeichnet" wurden. Durch die Korrelation dieser Zeitstempel miteinander werden Spirometrie- und EKG-Daten zeitlich mit einander korreliert.

# Input-Daten:
Spirometriedatei, EKG-Datei

# Output-Daten:
- Gibt Uhrzeit des Zeitstempels an,
- gibt die Indizes vom Zeitstempel in den Spirometrie- und EKG-Daten zurück. Mit diesen können die Daten auf zurecht geschnitten werden, sodass die Datensätze den selben Startzeitpunkt haben

# 2.2 Überprüfung und Finetuning mit Hilfe der Bauchgurtkurve:
Nach der Korrelation von EKG- und Spirometriedaten, kann eine Überprüfung auf richtige Korrelation mit Hilfe der Bauchgurtkurve überprüft werden. Falls nötig, kann eine weitere Verschiebung der Indizes zur besseren Korrelation der Zeitstempel eingetragen werden.

# Input-Daten:
Spirometriedatei, Bauchgurtkurve, Bilddaten

# Output-Daten:
- Indizes der Zeitstempel, mit Hilfe von Finetunung angepasst falls nötig

# 3. Reinschreiben in die Dicom:
Durch die Korrelation können zu jedem Bild aus der Echtzeitsequenz jeweils in der Ruhe- und Belastungsphase nun der Atemfluss und das Atemvolumen eingetragen werden. Durch Eintragen von Atemvolumen und Atemfluss können die Bilder auf Endexspiration gefiltert werden.
Durch Filtern der Bilder auf einen negativen Atemfluss, können die Bilder auf Exspiration (Ausatmung) gefiltert werden.
Es werden zwei Volumengruppen klassifiziert. Einmal ein Volumen unter einem einstellbaren Grenzwert, und einen über dem Grenzwert. Der Grenzwert gibt den Anteil vom durchschnittlichen Atemzugvolumen wieder (hier 30%).
Durch Filtern auf Atemvolumina unter diesem Grenzwert, können Bilder am Ende der Atemphase (bei negativen Atemfluss), auch in Endexspiration filtern.
Außerdem werden die Bilder außerdem in 25 EKG-Gruppen eingeteilt. Die EKG-Gruppe gibt den Zeitpunkt nach der RR-Zacke wieder. Aus den ganzen Bildern in Endexspiration werden für jede Schicht nun ein Bild für jede EKG-Gruppe herausgefiltert. Durch Filtern entsteht eine Bildsequenz eines Herzschlages für jede Schicht während Endexspiration.

Dies ist notwendig, um weiterführende Parameter via Circle auswerten zu können. Diese können dann mit der konventionellen KardioMRT Sequenz verglichen werden. Diese werden bei Endexspiration während Atemanhaltekommandos aufgenommen. Atemanhaltekommandos sind während der Belastungsphase nicht praktisch, weshalb hier diese Filterung erfolgt.

# Input-Daten:
Spirometriedatei, Bilddaten, 

# Output-Daten:
Aus den ganzen Bildern in Endexspiration werden für jede Schicht nun ein Bild für jede EKG-Gruppe herausgefiltert. Durch Filtern entsteht eine Bildsequenz eines Herzschlages für jede Schicht während Endexspiration.

