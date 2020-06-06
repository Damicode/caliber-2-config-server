

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
    
    stage('Building '){
        steps{
            
            sh 'mvn build'
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
              docker.withRegistry('', RegisterCrudential)
              
              {
                  
                  dockerImage.push()
              }
            }
            
        }

}

stage ("Remove unUsed docker image"){
    steps{

        sh "docker rmi ${Register}:my-image"
    }
}



}


}
