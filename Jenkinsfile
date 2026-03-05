pipeline {
    agent  {
        label 'Agent-1'
       
    }
    environment {
        course = 'jenkins'
    }
    options {
                // Timeout counter starts BEFORE agent is allocated
                timeout(time: 10, unit: 'SECONDS')
                disableConcurrentBuilds()
            }

     parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    // Build
    stages {
        stage('Build') {
            steps {
               script {
                sh """
                echo "Hello Build"
                SLEEP 10
                env
                """
                echo "Hello ${params.PERSON}"
               }
            }
        }
        stage('Test') {
            steps {
                 script {
                echo 'Building'
               }
            }
        }
        stage('Deploy') {
             input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            steps {
                script {
                echo "Hello, ${PERSON}, nice to meet you."
                echo 'Building'
               }
            }
        }
        
    }
     post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {
            echo 'Hello Sucess'
        }
        failure {
            echo 'Hello Failure'
        }
    }

}