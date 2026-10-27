# Robotics Lab 2026 - Classwork 0 (napolitano_rl26)

Configurazione dell'ambiente di sviluppo Docker per ROS 2 Humble con persistenza del codice tramite bind mount.

## Prerequisiti
- Sistema operativo Linux (Ubuntu 22.04)
- Docker installato e configurato per l'esecuzione senza privilegi di root (utente nel gruppo docker)
- Git installato

## Struttura del Repository
    napolitano_rl26/
    ├── docker_scripts/
    │   ├── Dockerfile
    │   ├── docker_build_image.sh
    │   ├── docker_run_container.sh
    │   └── docker_connect.sh
    ├── src/
    │   └── .gitkeep
    └── README.md

## Istruzioni di Setup ed Esecuzione (da macchina pulita a container attivo)

1. Clonare il repository nella propria directory HOME e impostare i permessi di esecuzione:
    cd ~
    git clone [https://github.com/](https://github.com/)<matteoznapolitano-c>/napolitano_rl26.git
    cd ~/napolitano_rl26
    chmod +x docker_scripts/*.sh

2. Costruire l'immagine Docker:
    ./docker_scripts/docker_build_image.sh rl2026

3. Avviare il container montando la cartella src/ del progetto:
    ./docker_scripts/docker_run_container.sh rl2026 rl2026_cont napolitano_rl26/src

4. Aprire una shell aggiuntiva nel container in esecuzione (da un altro terminale sull'host):
    ./docker_scripts/docker_connect.sh

## Verifica dell'Ambiente e Persistenza (Task 2)

1. Verifica dell'installazione di ROS 2 Humble (dentro il container):
    echo $ROS_DISTRO   # Output atteso: humble
    ros2 pkg list      # Elenco dei pacchetti ROS 2 installati

2. Test di persistenza del volume (src/):
    touch /home/user/ros2_ws/src/test_persistence.txt
    exit

   Verificando sull'host dopo la chiusura/rimozione del container (docker container prune -f):
    ls -la ~/napolitano_rl26/src/
   il file test_persistence.txt risulta presente nella cartella src/ dell'host, confermando la persistenza dei file.
