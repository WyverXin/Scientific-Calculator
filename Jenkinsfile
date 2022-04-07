pipeline {
    agent any

    tools{
        maven "M3"
    }

    stages{
        stage('clean up') {
            steps {
                sh 'mvn -f ./Calculator/pom.xml clean'
            }
        }

        stage('compile & build project') {
            steps {
                // create .jar file in the target fodler
                sh 'mvn -f ./Calculator/pom.xml package'
            }
        }

        stage('unit tests'){
            steps{
                sh 'mvn -f ./Calculator/pom.xml test'
            }
        }

        stage('SonarQube analyize') {
            steps {
                sh 'mvn -f ./Calculator/pom.xml clean verify sonar:sonar \
                    -Dsonar.projectKey=demo \
                    -Dsonar.host.url=http://192.168.56.21:9000 \
                    -Dsonar.login=6aaabd1f3e402b0b4e76801a7b7f54e01d004e2f'
            }
        }
    }
    post{
        success{
            archiveArtifacts 'Calculator/target/*.jar'
        }
        failure{
            echo '=========================='
            echo 'Build fail!!!!!!!!!!!!!!!!'
            echo '=========================='
        }
    }
}