pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ghcr.io/hotio/readarr'
        CONTAINER_NAME = 'readarr'
        PUID = '1000'
        PGID = '1000'
        UMASK = '002'
        TZ = 'America/Monterrey'
        CONFIG_PATH = '/home/docker/readarr/config'
        BOOKS_PATH = '/mnt/Media/Books'
        DOWNLOADS_PATH = '/mnt/Media/Downloads'
    }

    stages {
        stage('Deploy ReadArr Docker Image') {
            steps {
                script {
                    sh """
                    docker run -d \
                        --restart always \
                        --name ${CONTAINER_NAME} \
                        -p 2727:2727 \
                        -e PUID=${PUID} \
                        -e PGID=${PGID} \
                        -e UMASK=${UMASK} \
                        -e TZ=${TZ} \
                        -v ${CONFIG_PATH}:/config \
                        -v ${BOOKS_PATH}:/Books \
                        -v ${DOWNLOADS_PATH}:/downloads \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
