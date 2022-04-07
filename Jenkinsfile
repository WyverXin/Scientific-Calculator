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

        stage('compile project') {
            steps {
            
                sh 'mvn -f ./Calculator/pom.xml install'
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