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
        USERNAME = sh(script: 'echo $USER', returnStdout: true).trim()  
    }

    stages {
        stage('Deploy Docker Container') {
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
                        -v /media/${USERNAME}/Media/Books:/data \
                        -v /media/${USERNAME}/Media/Downloads:/downloads \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
