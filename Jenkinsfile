pipeline{
	agent any
	environment{
		LANG='en_US.UTF-8'
		LC_ALL='en_US.UTF-8'
		}
	tools{
		maven:'Maven'
		}
	stages{
		stage('checkout'){
			steps{
				git branch:'main',
				url:"https://github.com/NiranjanGK/Ansible.git"
				}
			}
		stage('Build'){
			steps{
				sh 'mvn clean install'
				}
			}
		stage('Test'){
			steps{
				sh 'mvn test'
				}
			}
		stage('archive'){
			steps{
				archiveArtifats artifacts:'target/*.war',
				fingerprint:true
				}
			}
		stage('Deploy'){
			steps{
				sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
				}
			}
		}
	post{
		success{
			echo 'BUILD SUCCESS'
			}
		failure{
			echo 'BUILD FAILURE'
			}
		}
}
