#!groovy​

stage("Intro"){
        node {
            sh "echo 'Hola'"
        }
}

if (env.BRANCH_NAME =~ ".*release/.*" || env.BRANCH_NAME =~ ".*feature/.*") {
    stage("CI"){
        node {
            sh "echo 'INTEGRACION'"
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
