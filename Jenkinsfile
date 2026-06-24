pipeline {
    agent {
        docker
        { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }

    parameters {
        booleanParam(name: 'Collection', defaultValue: true, description: 'Lancer la collection')

        choice(name: 'Environnement', choices: ['E2E', 'Preprod', 'Test'], description: 'Choisir l\'environnement')

    }


    stages {
        stage('lancer le test') {

            steps {
                script {
                    if (params.Collection) {
                        sh 'newman run collection.json'
                     } 

                    if (params.Environnement == 'Test') {
                        sh 'newman run Collection3.json -e envs/test2_env.json'
                    } else if (params.Environnement == 'E2E') {
                        sh 'newman run Collection2.json -e envs/e2e_env.json'
                    } else {
                        sh 'newman run Collection2.json -e envs/preprod2_env.json'
                    }
                }
            }
        }
    }
}
