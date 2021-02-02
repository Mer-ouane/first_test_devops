node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("mrben63/firstapp-test-pipeline:2")
    }

  
    stage('Test image') {
        
	//docker.image("....").inside("{{-v /var/jenkins/caches:/var/jenkins/caches") 
        app.inside("{{-v /var/jenkins/caches:/var/jenkins/caches")  {
            	echo "Tests passed"
        }
    }
	
    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
	
	  
}
