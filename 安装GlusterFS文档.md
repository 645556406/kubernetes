# 安装GlusterFS文档  

1. ### 依赖安装  

    `yum install glusterfs glusterfs-fuse -y`

2. ### 增加配置  
   
   在kube-apiserver的启动参数中添加：`--allow-privileged=true`  
3. ### 打标签  

	给要部署GlusterFS管理服务的节点打上storagenode=glusterfs标签，是为了将GlusterFS定向部署到安装了GlusterFS的节点上。

4. ### 创建GlusterFS管理服务容器集群  
    `说明：GlusterFS是一种分布式存储，与其类似的还有ceph`  
	创建glusterfs-daemonset.yaml  

5. ### 创建Heketi服务  
    `说明：heketi是一个用来管理GlusterFS卷的框架`  
    创建heketi-rbac.yaml    

6. ### 设置管理集群信息  
    要求：  

    1. 一个GlusterFS集群中至少有三个节点
    2. devices要求是未创建创建文件系统的裸设备（可以有多快盘），以供Heketi自动完成创建PV、VG、LV

    如何创建：  
    1. 创建一个配置文件信息的json文件  
    2. 进入Heketi容器执行  
    `heketi-cli topology load --json=topology.json`  
    