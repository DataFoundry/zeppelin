#内容简介
本例演示如果通过datafoundry提供spark后端服务来为zeppelin提供所需的计算资源，同时演示了如果基于中间镜像构建新应用镜像
##  构建spark基础镜像  
oc new-build https://github.com/datafoundry/zeppelin.git --context-dir=spark  

##  生成spark后端服务
 oc new-backingserviceinstance spark-inst --backingservice_name=spark --planid=BackingServicePlanGuid  

##  基于spark基础镜像构建zeppelin镜像  
oc new-app https://github.com/datafoundry/zeppelin.git --context-dir=zeppelin  


##  讲spark服务绑定到zeppelin应用中
 oc bind spark-inst zeppeline  
 oc env dc/zeppelin SPARKBSI=spark-inst BSITYPE=SPARK
