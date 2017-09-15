pipeline {
	agent any
	stages{
		stage('构建镜像') {
			steps {
				script {
					if(params.SKIP_BUILD_IMAGE){
						println "跳过构建镜像"
					}
					else
					{
						echo "构建镜像"
					}
				}
			}
		}
		stage('推送内部私有仓') {
			steps {
				script {
					if(params.SKIP_BUILD_IMAGE){
						println "跳过推送镜像"
					}
					else
					{
						echo "推送镜像"
					}
				}
			}
		}
		stage('删除上次本地镜像') {
			steps {
				script {
					if(params.SKIP_BUILD_IMAGE){
						println "跳过删除上次镜像"
					} 
					else
					{
						echo '删除上次镜像'
					}
				}
			}
		}
                stage('发布测试环境') {
			steps {
				script {
					if(params.SKIP_DEPLOY_TEST){
						println "跳过发布测试镜像"
					}
					else    
					{
						echo '发布测试镜像'
					}
				}
			}
		}
		stage('远程发布正式环境') {
			steps {
				script {
					def deployToProduction = true
					def userInput = true
					def didTimeout = false
					try{
						timeout(time: 60, unit: 'SECONDS') {
							input '是否发布'
						}
					}catch(err){
						echo '选择了取消发布'
						def timeout = err.getCauses()[0].getUser()
						if ('SYSTEM' == timeout.toString()) {
							echo '原因:选择超时取消'
						}
						deployToProduction = false
					}
				
					if(deployToProduction){
						echo '发布正式环境'
					}
					else{
						println "已取消发布"
					}
				}
			}
		}
	}
}
