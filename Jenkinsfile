

node{



stage ('Clonning from git'){

    steps{
        git 'https://github.com/Damicode/caliber-2-config-server.git'
    }
    

}

stage('Version'){
        steps{
            sh 'mvn --version'
        }
}
stage ("initialize") {
steps {
sh '''
echo "PATH = ${PATH}"
echo "M2_HOME = ${M2_HOME}"
'''
}
}
stage('Clean'){
    def  MAVEN_HOME = tool name: 'maven-3', type: 'maven'
        steps{
            sh "${MAVEN_HOME}/bin/mvn build"
        }
}

stage('Test'){
        steps{
            sh "mvn package"
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
