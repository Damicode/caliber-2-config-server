

pipeline{

agent any

environment{
    Register ="damier85/damier-raymond"
    RegisterCrudendtial ="Mydocker20"
    dockerImage =""
   
 
}
 tools{
 maven 'maven-3'

 }
stages{

stage ('Clonning from git'){

    steps{
       echo "Something"
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
stage('install'){
        steps{
            
            sh "mvn clean package"
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

                docker.build("my-image:test")
            }
        }
}

stage ('Deploy image to DockerHub'){

        steps{
            script{

                docker.withResgistry('' , RegisterCrudendtial)
                dockerImage.push()
            }
        }

}

stage ("Remove unUsed docker image"){
    steps{

        sh "docker rmi $Registry:$BUILD_NUMBER"
    }
}



}


}
