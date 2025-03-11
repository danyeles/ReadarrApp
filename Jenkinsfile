pipeline {
    agent any

    environment {
        CONTAINER_NAME = 'readarr'
        DOCKER_IMAGE = 'ghcr.io/hotio/readarr'
        PUID = '1000'
        PGID = '1000'
        UMASK = '002'
        TZ = 'Etc/UTC'
        CONFIG_PATH = '/<host_folder_config>' // Replace with your host config folder
        DATA_PATH = '/<host_folder_data>' // Replace with your host data folder
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
                        -v ${DATA_PATH}:/data \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
