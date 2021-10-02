pipeline{
	agent{
		label 'master'
	}
	environment{
		PATH= "usr/share/maven/bin:$PATH"
		registry = "anand7kumar65" 
	   registryCredential = 'docker_hub' 
	   dockerImage=''

	   }
	stages{
		stage('checkout'){
			steps{
                  git 'https://github.com/anand7kumar65/ValaxyTech-hello-world.git'
			}
		}
		stage('maven build'){
			steps{
			sh "mvn clean install package"
			}
		}
		stage('docker build'){
			steps { 
                script { 
                      dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                     }
               }  
		}
		stage('uploading to hub'){
		    steps{
		          script { 
                       docker.withRegistry( '', registryCredential ) { 
                       dockerImage.push() 
                        }
		          }
		    }
	    }
	}
