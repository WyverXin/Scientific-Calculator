pipeline {
    agent any

    tools{
        maven "M3"
    }

    stages{
        stage('clean up') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('compile project') {
            steps {
            
                sh 'mvn install'
            }
        }

        // stage('SonarQube analyize') {
        //     steps {
        //         withSonarQubeEnv('YuxinsSonar') {
        //             withMaven {
        //                 sh './mvnw sonar:sonar'
        //             }
        //         }
        //     }
        // }
    }
    post{
        success{
            archiveArtifacts 'target/*.jar'
        }
        failure{
            echo '=========================='
            echo 'Build fail!!!!!!!!!!!!!!!!'
            echo '=========================='
        }
    }
}