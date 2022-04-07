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
            archiveArtifacts 'Calculator/target/*.jar'
        }
        failure{
            echo '=========================='
            echo 'Build fail!!!!!!!!!!!!!!!!'
            echo '=========================='
        }
    }
}