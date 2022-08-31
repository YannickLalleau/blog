# UNISON : Suppression des fichiers temporaires cachés

Via la commande :
find [Working directory] -name '.unison.*.tmp' -exec rm -rf \{} \;

Exemple :
find /data -name '.unison.*.tmp' -exec rm -rf \{} \;

