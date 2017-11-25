pipeline {
    agent any 

    stages {
        stage('Checkout'){
            steps {
		checkout scm
            }
        }
        
        stage('test fastlane actions') { 
            steps { 
                sh 'fastlane actions' 
            }
        }
        
        stage('Gradle Test'){
            steps {
                sh "gradle -v"
            }
           
        }
        
        stage('Android Test'){
            steps {
                sh "android"
            }
           
        }
        
        stage('test Fastfile') { 
            steps { 
                sh 'fastlane example' 
            }
        }
        
    }//end stages
}//end pipeline    
        
        
