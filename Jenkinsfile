// Powered by Infostretch 

timestamps {

node () {

	stage ('Check_SSh_Connectivity - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'baltah666', url: 'https://github.com/baltah666/Aresta']]]) 
	}
	stage ('Check_SSh_Connectivity - Build') {
 			// Shell build step
sh """ 
ansible all -m ping 
 """ 
	}
	stage ('check_version_of_code_running - Build') {
 			// Shell build step
sh """ 
ansible spines -m eos_command -a "commands='show version'"
ansible leafs -m eos_command -a "commands='show version'" 
 """ 
	}
	stage ('deploy_evpn - Build') {
 			// Shell build step
sh """ 
ansible-playbook deploy_evpn.yml 
 """ 
	}
	stage ('check_EVPN_deployed - Build') {
 			// Shell build step
sh """ 
ansible spines -m eos_command -a "commands='show bgp evpn summary'"
ansible leafs -m eos_command -a "commands='show bgp evpn summary'" 
 """ 
	}
	stage ('Deploy_L2_and_L3_VXLANs_Services - Build') {
 			// Shell build step
sh """ 
ansible-playbook deploy_l2vxlan.yml -l 'vtep1,vtep2' -e "vlan_name=ansible_test vlan_id=40" 
 """ 
	}
	stage ('Deploy_tenant_VRF_all_Leafs - Build') {
 			// Shell build step
sh """ 
ansible-playbook deploy_vrf.yml -l leafs -e "vrf_name=ansible vrf_id=1" 
 """ 
	}
	stage ('Checking_vrf_leaf - Build') {
 			// Shell build step
sh """ 
ansible spines -m eos_command -a "commands='show vrf'"  
ansible leafs -m eos_command -a "commands='show vrf'" 
 """ 
	}
}
}