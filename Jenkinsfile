pipeline {
    agent any
    // Trigger the build every 1 minute
    triggers {
        cron('H/60 * * * *')
    }

    // Build with the Maven tool we set up in the Jenkins 
    tools{
        maven "Maven_3"
    }
    // Clain Stages in the pipeline
    stages{
        stage('clean up') {
            steps {
                // clean up the bianry files existed
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
                // run unit tests
                sh 'mvn -f ./Calculator/pom.xml test'
            }
        }

        stage('SonarQube analyize') {
            steps {
            sh 'mvn -f ./Calculator/pom.xml clean verify sonar:sonar \
            -Dsonar.projectKey=QM_HW3_Scientific_Calculator \
            -Dsonar.host.url=http://192.168.56.21:9000 \
            -Dsonar.login=3d8fab59134d384be0a0d2fa42e6f599478e453f'
            }
        }

        // stage('SonarQube analyize') {
        //     steps {
        //         sh 'mvn -f ./Calculator/pom.xml clean verify sonar:sonar \
        //             -Dsonar.projectKey=demo \
        //             -Dsonar.host.url=http://192.168.56.21:9000 \
        //             -Dsonar.login=6aaabd1f3e402b0b4e76801a7b7f54e01d004e2f'
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