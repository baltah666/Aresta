// Powered by Infostretch 

timestamps {

node () {

	stage ('ArestaLab_1_GIT - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'baltah666', url: 'https://github.com/baltah666/Aresta']]]) 
	}
	stage ('ArestaLab_1_GIT - Build') {
 			// Shell build step
sh """ 
cd 	ansible-arista-evpn-lab
ansible all -m ping 
 """ 
	}
}
}