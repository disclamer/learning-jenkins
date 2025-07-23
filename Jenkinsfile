node {
    try {
        stage('Checkout Code') {
            checkout scm
        }

        stage('Install Dependencies') {
            sh 'npm install'
        }

        stage('Run App') {
            // Kill any previous instance of the app
            sh 'pkill -f "node app.js" || true'

            // Start the app using nohup so it doesn't exit when the pipeline finishes
            sh 'node app.js > app.log 2>&1 &'

            sleep 30  // Give it some time to start

            // Verify that it's running
            sh 'curl http://localhost:3002'
        }
    } finally {
        echo 'Cleaning up...'
    }
}