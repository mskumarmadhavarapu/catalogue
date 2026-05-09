pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }
    environment { 
        appVersion = ""
    }
    options { 
        disableConcurrentBuilds()
        timeout(time: 5, unit: 'SECONDS')
    }
    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }
    stages {
        stage('Read version') {
            steps {
                script {
                    // Reads the file into a Groovy Map
                    def packageJson = readJSON file: 'package.json'
                    
                    // Access specific fields
                    appVersion = packageJson.version
                    echo "Building ${appName} version ${appVersion}"
                }
            }
        }
    stages {
        stage('Build') {
            steps {
                script {
                    sh """
                        npm install 
                    """
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh """
                        echo "Testing"
                         echo "Hello ${params.PERSON}"
                         echo "Biography: ${params.BIOGRAPHY}"
                         echo "Toggle: ${params.TOGGLE}"
                         echo "Choice: ${params.DEPLOY}"
                         echo "Password: ${params.PASSWORD}"
                    """
                }
            }
        }
        stage('Deploy') {
            when {
                expression { "${params.DEPLOY}" == "true"}
            }
            // input {
            //     message "Should we continue?"
            //     ok "Yes, we should."
            //     submitter "alice,bob"
            //     parameters {
            //         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
            //     }
            // }
            steps {
                script {
                    sh """
                        echo "Deploying"
                        echo $COURSE
                    """
                }
            }
        }
    }

    // post build
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success { 
            echo 'pipeline success'

        }
        failure { 
            echo 'pipeline failure'
        }
    }
}