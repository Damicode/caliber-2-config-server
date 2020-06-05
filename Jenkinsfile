

pipeline{

agent any
enrironement{
    dockerRegister ="damier85"
    dockerRegisterCrudendtial ="Mydocker20"
    dockerImage =""
}

stage ('Clonning from git'){

    steps{
        git "https://github.com/Damicode/caliber-2-config-server.git"
    }
    

}

stage('clean'){
        steps{
            sh 'mvn clean compile'
        }
}

stage('install'){
        steps{
            sh 'mvn install'
        }
}

stage('Test'){
        steps{
            sh 'mvn test'
        }
}


stage('Build the image'){

        steps{
            script{

                dockerImage = docker.Build dockerRegister + ":$BUILD_NUMBER"
            }
        }
}

stage ('Deploy image to DockerHub'){

        steps{
            script{

                docker.withResgistry('' , dockerRegisterCrudendtial)
                dockerImage.push()
            }
        }

}

stage ("Remove unUsed docker image"){
    steps{

        sh "docker rmi $dockerRegistry:$BUILD_NUMBER"
    }
}






}