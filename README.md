# waydroid-focus

Script bash qui lance une appli Android dans Waydroid en libérant le GPU et le CPU pour elle,
puis remet tout comme avant quand elle se ferme. Pensé pour le Xiaomi 12T Pro (Adreno 730)
sous Linux avec le pilote DRM msm, mais utilisable sur toute machine où Waydroid tourne.

## Utilisation

    ./waydroid-focus guitartuna              # alias de com.ovelin.guitartuna
    ./waydroid-focus -n guitartuna           # simulation : n'écrit rien
    ./waydroid-focus --gpu-max 500 --size 720x1560 guitartuna

Tant que l'appli tourne :

- les autres processus de l'utilisateur qui utilisent le GPU (Firefox, etc.) sont gelés (SIGSTOP),
  sauf le bureau, le terminal et Waydroid (`--keep REGEX` pour en protéger d'autres,
  `--no-freeze` pour désactiver) ;
- côté Android, les animations sont coupées et les applis en cache arrêtées (`--no-android`
  pour désactiver) ;
- en option, la résolution est réduite (`--size LxH`) et la fréquence max du GPU plafonnée
  (`--gpu-max MHZ`).

Tout est restauré à la fermeture de l'appli ou sur Ctrl+C. `--stop` arrête aussi la session Waydroid.

Le script demande `sudo` (shell Waydroid, fréquence GPU). Pour mesurer l'effet sur le GPU, voir
[u-gputop](https://github.com/rakhenmanoa/u-gputop) (`adreno-smi -l 1`).

## Installation

    sudo install -m755 waydroid-focus /usr/local/bin/

ou, sous Arch Linux (ARM) :

    makepkg -si

## Licence

[BSD Zero Clause (0BSD)](LICENSE).
