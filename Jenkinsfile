

pipeline{

agent any

environment{
    Register ="damier85/damier-raymond"
    RegisterCrudential ="Mydocker20"
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

               dockerImage = docker.build("damier85/damier-raymond:my-image")
            }
        }
}

stage ('Deploy image to DockerHub'){

        steps{
            script{
                withCredentials([usernamePassword(credentialsId: 'Mydocker20', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
      echo ''' ${USERNAME}
              "pasword ${PASSWORD}"
              "testing" '''
              
              docker.withRegistry('', RegisterCrudential)
              
              {
                  sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                  dockerImage.push()
              }
              
              echo ''' ${USERNAME}
              "pasword ${PASSWORD}"
              "testing" '''

        }
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
