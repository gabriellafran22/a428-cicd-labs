node {
    checkout scm
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
                withEnv(["CI=true"]){
                        stage('Build') {
                                sh 'npm install'
                        }
                        stage('Test') {
                                sh './jenkins/scripts/test.sh'
                        }
			stage('Manual Approval'){
	    			input message: 'Approval dibutuhkan, Deploy app?', ok: 'Proceed'
    			}
			stage('Deploy') { 
				sh './jenkins/scripts/deliver.sh'
				input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
		        //        sh 'sleep 1m'
				sh './jenkins/scripts/kill.sh' 
			}
                }
        }
}
