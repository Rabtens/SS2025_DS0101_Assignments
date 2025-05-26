pipeline {
	agent any
	tools {
    	nodejs 'NodeJS 24.0.2'
	}

	stages {
    	// Stage 1: Checkout Code
    	stage('Checkout') {
        	steps {
            	git branch: 'main',
            	url: 'https://github.com/Rabtens/SS2025_DS0101_Assignments'
        	}
    	}

    	// Stage 2: Install Dependencies
    	stage('Install') {
        	steps {
            	sh 'npm install' 
        	}
    	}

    	// Stage 3: Build (if applicable, e.g., for React/TypeScript)
    	stage('Build') {
        	steps {
            	sh 'npm run build' 
        	}
    	}

    	// Stage 4: Run Unit Tests
    	stage('Test') {
        	steps {
            	sh 'npm test'  // Runs "test" script (Jest/Mocha)
        	}
        	post {
            	always {
                	junit 'junit.xml'  // Publish test results
            	}
        	}
    	}

    	// Stage 5: Deploy (Docker Example)
    	stage('Deploy') {
        	steps {
            	script {
                	// Build Docker image
                	docker.build('rabtens/node-app:latest')
               	 
                	// Push to Docker Hub (requires credentials)
                	docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-password') {
                    	docker.image('rabtens/node-app:latest').push()
                	}
            	}
        	}
    	}
	}
}