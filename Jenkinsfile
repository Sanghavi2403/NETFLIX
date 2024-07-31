pipeline{
agent any
	stages{
		stage("CLeaning working space"){
			steps{
				sh 'rm -rf *'
				sh 'rm -rf /var/www/html/*'
				}
		}
		stage("Clone source code"){
			steps{
				sh 'git clone https://gitlab.com/sanghavij243/netflix.git -b master'
			      }
			}
		stage("Create Tar"){
			steps{
                sh 'cp -r /var/lib/jenkins/workspace/webload1/netflix/* /var/lib/jenkins/workspace/webload1/'
				sh 'tar -czvf sanghavi.tar.gz *'
				}
			}
		stage("Build Image"){
			steps{
				sh 'docker stop contproj'
				sh 'docker rm contproj'
				sh 'docker rmi sanghavi'
				sh 'docker build -t sanghavi:s1 -f /var/lib/jenkins/workspace/webload1/netflix/Dockerfile .'
				}
			}
		stage("Run Image"){
			steps{
				sh 'docker run -d --name contproj -p 80:80 sanghavi:s1'
				}
		}
}
}