pipeline {
	agent {
		node {
			label "built-in"
			customWorkspace "/mnt/kkk"
		}
	}
	
	stages {
		stage ('clone repo') {
			steps {
		                sh "rm -rf /mnt/kkk/*" 
				sh "git clone https://github.com/HEMANT-111/loginwebapp.git"
			}
		}
		
		stage ('create build') {
			steps {
			dir ('/mnt/kkk/loginwebapp') {
			    
			    sh "mvn clean install"
			    	
			
			}
			}
		}
		stage ("chmod") {
			steps {
				dir ("/mnt/kkk/loginwebapp/target") {
					sh "chmod -R 777 LoginWebApp.war"
				}
			}
		}
		
		
		stage ('copy-to-cont'){
			
			steps {
				
				sh "cp /mnt/kkk/loginwebapp/target/*.war /mnt/kkk/loginwebapp"
				}
		}
		
		
		stage ('container'){
			steps {
				dir ("/mnt/kkk/loginwebapp") {
				sh "docker build -t don1 ."
                                sh "docker run --name doncont -itdp 8888:8080 don1"


				}
			}
		}
	}
}
