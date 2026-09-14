# Projet Keil – STM32F103RB

## Présentation

Ce projet est simplement un **projet de base initialisé sous Keil µVision** afin de pouvoir commencer à programmer un microcontrôleur **STM32F103RB**.

Il ne contient volontairement aucune fonctionnalité particulière.

L'objectif est uniquement de disposer d'un environnement déjà configuré pour :

- écrire du code en C ;
- compiler le programme avec Keil ;
- utiliser les fichiers de démarrage du STM32 ;
- accéder aux registres et périphériques du microcontrôleur ;
- programmer et déboguer la carte avec un **ST-Link** ;
- servir de base pour de futurs projets embarqués.

---

## Microcontrôleur utilisé

Le projet est configuré pour :

- **Fabricant :** STMicroelectronics
- **Microcontrôleur :** STM32F103RB
- **Architecture :** ARM Cortex-M3
- **Famille :** STM32F1

Le Device Family Pack utilisé par le projet est :

```text
Keil.STM32F1xx_DFP.2.4.1
```

---

## Environnement de développement

Le projet est prévu pour être utilisé avec :

- **Keil µVision / MDK-ARM**
- le pack STM32F1 correspondant ;
- un programmateur/débogueur **ST-Link** pour envoyer le programme dans le microcontrôleur.

Le fichier principal du projet Keil est :

```text
projet_keil_neuf.uvprojx
```

Il suffit d'ouvrir ce fichier avec Keil µVision pour charger le projet.

---

## Organisation du projet

```text
Projet_keil_neuf/
│
├── main.c
├── projet_keil_neuf.uvprojx
├── projet_keil_neuf.uvoptx
│
├── RTE/
│   └── Device/
│       └── STM32F103RB/
│           ├── startup_stm32f10x_md.s
│           ├── system_stm32f10x.c
│           └── RTE_Device.h
│
├── DebugConfig/
├── Objects/
├── Listings/
├── Driver_stlink/
└── Tuto_initialisation.pdf
```

### `main.c`

Il s'agit du point d'entrée du programme.

Le projet contient actuellement un programme volontairement minimal :

```c
#include "stm32f10x.h"

void init_proc(void)
{
}

int main(void)
{
    init_proc();

    while (1)
    {
    }
}
```

La fonction :

```c
init_proc();
```

est prévue pour accueillir les futures initialisations du microcontrôleur, par exemple :

- configuration des GPIO ;
- activation des horloges ;
- configuration des timers ;
- configuration de l'UART ;
- configuration de l'ADC ;
- configuration du SPI ou de l'I2C ;
- configuration des interruptions.

La boucle :

```c
while (1)
{
}
```

correspond à la boucle principale du programme embarqué.

---

## Fichiers de démarrage

Le dossier :

```text
RTE/Device/STM32F103RB/
```

contient notamment les fichiers nécessaires au démarrage du STM32.

### `startup_stm32f10x_md.s`

Ce fichier assembleur contient notamment :

- la table des vecteurs d'interruption ;
- le point d'entrée après le reset ;
- les différents gestionnaires d'interruptions.

### `system_stm32f10x.c`

Ce fichier contient les éléments liés à l'initialisation système du STM32, notamment la configuration de base de l'horloge système.

Ces fichiers permettent au microcontrôleur d'arriver correctement jusqu'à la fonction :

```c
main()
```

---

## Compiler le projet

1. Installer **Keil µVision / MDK-ARM**.
2. Installer le pack STM32F1 si nécessaire.
3. Ouvrir :

```text
projet_keil_neuf.uvprojx
```

4. Vérifier que la cible sélectionnée est :

```text
STM32F103RB
```

5. Compiler le projet avec **Build** dans Keil.

Les fichiers générés lors de la compilation sont placés principalement dans :

```text
Objects/
```

et :

```text
Listings/
```

---

## Programmer le microcontrôleur

Le projet peut être utilisé avec un **ST-Link** pour programmer et déboguer le STM32.

Un dossier :

```text
Driver_stlink/
```

est présent dans le projet et contient le package d'installation des pilotes ST-Link utilisé lors de la mise en place de l'environnement.

Une fois le ST-Link correctement installé et configuré dans Keil, il est possible de :

1. connecter le ST-Link au microcontrôleur ;
2. compiler le projet ;
3. télécharger le programme dans la mémoire Flash du STM32 ;
4. lancer ou arrêter l'exécution ;
5. utiliser le débogueur de Keil.

---

## But de ce dépôt

Ce dépôt ne correspond pas à un programme final.

Il constitue uniquement une **base de projet fonctionnelle pour le STM32F103RB sous Keil**.

L'idée est d'éviter de devoir recréer et reconfigurer entièrement un projet Keil à chaque nouveau développement.

À partir de cette base, il est possible de développer progressivement les différents pilotes et fonctionnalités nécessaires au projet :

```text
Projet Keil de base
        │
        ├── GPIO
        ├── Timers
        ├── UART
        ├── ADC
        ├── PWM
        ├── SPI
        ├── I2C
        ├── Interruptions
        └── Application finale
```

---

## État actuel

À l'heure actuelle :

- le projet Keil est créé ;
- le STM32F103RB est sélectionné ;
- les fichiers de démarrage sont présents ;
- le projet peut être compilé ;
- une fonction `init_proc()` est prévue pour les futures initialisations ;
- aucune fonctionnalité applicative n'est encore implémentée.

Le projet sert donc simplement de **point de départ propre et réutilisable pour programmer le STM32F103RB avec Keil µVision**.
