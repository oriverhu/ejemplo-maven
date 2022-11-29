#!groovy

stage("Intro"){
        node {
            sh "Hola"
        }
}

if (env.BRANCH_NAME =~ ".*release/.*" || env.BRANCH_NAME =~ ".*feature/.*") {
    stage("CI"){
        node {
            sh "INTEGRACION"
        }
    }   
}


if (env.BRANCH_NAME =~ ".*master" || ".*development") {
    stage("CD"){
        node {
            sh "DESPLIEGUE"
        }
    }   
}
