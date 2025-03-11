pipeline {
    agent any

    environment {
        CONTAINER_NAME = 'readarr'
        DOCKER_IMAGE = 'ghcr.io/hotio/readarr'
        PUID = '1000'
        PGID = '1000'
        UMASK = '002'
        TZ = 'Etc/UTC'
        CONFIG_PATH = '/home/docker/readarr/config'
        BOOKS_PATH = '/mnt/Media/Books'
        DOWNLOADS_PATH = '/mnt/Media/Downloads'
    }

    stages {
        stage('Deploy Docker Container') {
            steps {
                script {
                    sh """
                    docker run --rm \
                        --name ${CONTAINER_NAME} \
                        -p 2727:2727 \
                        -e PUID=${PUID} \
                        -e PGID=${PGID} \
                        -e UMASK=${UMASK} \
                        -e TZ=${TZ} \
                        -v ${CONFIG_PATH}:/config \
                        -v ${BOOKS_PATH}:/data \
                        -v ${DOWNLOADS_PATH}:/downloads \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
