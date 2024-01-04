def credential = 'github'
def server = 'team1@103.127.132.84'
def directory = '/home/team1/wayshub-frontend'
def branch = 'main'
def service = 'frontend'

pipeline {
	agent any
	stages {
		stage('pull request'){
			steps {
				sshagent([credential]) {
					sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
					docker compose down ${service}
					cd ${directory}
					git pull origin ${branch}
					exit
					EOF"""
				}
		}
}

                stage('building'){
                        steps {
                                sshagent( [credential]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        docker compose down ${service}
                                        exit
                                        EOF"""
                                }
                }
}

                stage('deploy'){
                        steps {
                                sshagent([credential]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        docker compose up -d ${service}
                                        exit
                                        EOF"""
                                }
                }
}

                stage('test'){
                        steps {
				echo "Test To Discord"
				discordSend description: 'Testing Frontend', 
				footer: 'Frontend-Deploy', 
				image: '', 
				link: 'env.BUILD_URL', 
				result: '', scmWebUrl: '', 
				thumbnail: '', 
				title: 'Frontend', 
				webhookURL: 'https://discord.com/api/webhooks/1192247473805197374/vqEg_eqP--CwJes-jdVXSvIIvW96JmfuacWILoFNnQVQJonzOio1okr6Q6PMdBqW1k4H'
                                }
                }
}
}
