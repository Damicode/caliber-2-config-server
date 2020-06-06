

node{

 def MAVEN_HOME = tool name: 'maven-3', type: 'maven'

stage ('Clonning from git'){

   
        git 'https://github.com/Damicode/caliber-2-config-server.git'
 
    

}

stage('Version'){
      
            sh 'mvn --version'
        
}
stage ("initialize") {

sh '''
echo "PATH = ${PATH}"
echo "M2_HOME = ${M2_HOME}"
echo "MAVEN_HOME"
'''

}


stage('install'){
     
   sh "mvn package"
        
}




}
