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
- les applis Android inutiles que tu as choisies sont désactivées (voir plus bas) ;
- en option, la résolution est réduite (`--size LxH`) et la fréquence max du GPU plafonnée
  (`--gpu-max MHZ`).

Tout est restauré à la fermeture de l'appli ou sur Ctrl+C. `--stop` arrête aussi la session Waydroid.

Le script demande `sudo` (shell Waydroid, fréquence GPU). Pour mesurer l'effet sur le GPU, voir
[u-gputop](https://github.com/rakhenmanoa/u-gputop) (`adreno-smi -l 1`).

## Désactiver des applis Android inutiles

    ./waydroid-focus --list                                   # paquets installés dans Android
    ./waydroid-focus --disable com.exemple.app guitartuna     # pour un lancement
    mkdir -p ~/.config/waydroid-focus
    cp disable.list.example ~/.config/waydroid-focus/disable.list   # puis l'éditer

Pour ne rien avoir à lister, `--bg` désactive d'un coup **toutes les applis tierces** installées
dans Android (sauf l'appli lancée) ; `--keep-app PAQUET` en épargne certaines :

    ./waydroid-focus --list-bg                       # ce qui tourne en ce moment dans Android
    ./waydroid-focus --bg guitartuna
    ./waydroid-focus --bg --keep-app org.fdroid.fdroid guitartuna

Les paquets listés dans `~/.config/waydroid-focus/disable.list` (un par ligne) sont arrêtés
puis désactivés (`pm disable-user`) pendant l'appli, et réactivés à la fermeture.

- Une appli déjà désactivée avant le lancement n'est pas réactivée ensuite.
- Sont toujours ignorés : l'appli lancée, le système Android essentiel (`android`, SystemUI,
  providers, clavier, WebView…) et tout ce qui touche à Waydroid.
- Si la session est interrompue brutalement (batterie, `kill -9`), les applis sont réactivées
  au prochain lancement, ou tout de suite avec `./waydroid-focus --restore`.
- `--no-disable` ignore la liste pour un lancement.

Désactiver des applis système peut en faire planter d'autres : commence par les applis
tierces et teste.

## Installation

    sudo install -m755 waydroid-focus /usr/local/bin/

ou, sous Arch Linux (ARM) :

    makepkg -si

## Licence

[BSD Zero Clause (0BSD)](LICENSE).
