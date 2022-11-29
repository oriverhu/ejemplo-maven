#!groovy

stage("Intro"){
        node {
            sh "echo 'Hola'"
        }
}

if (env.BRANCH_NAME =~ ".*release/.*" || env.BRANCH_NAME =~ ".*feature/.*") {
    stage("Paso 1: Compliar"){
        node {
            sh "echo 'Compile Code! oriverhu'"
            sh "./mvnw clean compile -e"
        }
    }
    stage("Paso 2: Testear"){
        node {
            script {
            sh "echo 'Test Code!'"
            // Run Maven on a Unix agent.
            sh "./mvnw clean test -e"
            }
        }
    }
    stage("Paso 3: Build .Jar"){
        node {
            try {
                script {
                sh "echo 'Build .Jar!'"
                // Run Maven on a Unix agent.
                sh "./mvnw  clean package -e"
                }
            }catch (e) {
                echo 'This will run only if failed'
                throw e
            }
            finally {
                // if (currentBuild.result == 'UNSTABLE') {
                //     echo 'This will run only if the run was marked as unstable'
                // }
                echo 'current result: ' currentBuild.result
            } 
        }
    }
    stage("Paso 4: Análisis SonarQube"){
        node {
            withSonarQubeEnv('sonarqube') {
                sh "echo 'Calling sonar Service in another docker container!'"
                // Run Maven on a Unix agent to execute Sonar.
                sh './mvnw  clean verify sonar:sonar -Dsonar.projectKey=ejemplo-maven'
            }
        }
    } 
}


if (env.BRANCH_NAME =~ ".*master" || env.BRANCH_NAME =~  ".*development") {
    stage("CD"){
        node {
            sh "echo 'DESPLIEGUE'"
        }
    }   
}
