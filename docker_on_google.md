# Docker Cloud
`sudo docker run -v /home/kanwu_wisc:/local python python /local/test.py 2333`   run 

# 新建container 然后 传命令给他执行
```
 9496  docker create -it -v /Users/sherlock/Desktop/:/local --name new-container-1 python
 9497  docker start new-container-1
 9500  docker exec new-container-1 python /local/test.py
```

# 最后我的 script
```
sudo docker create -it -v /home/kanwu_wisc:/local --name test_1 python
sudo docker create -it -v /home/kanwu_wisc:/local --name test_2 python
sudo docker create -it -v /home/kanwu_wisc:/local --name test_3 python

sudo docker start test_1
sudo docker start test_2
sudo docker start test_3

sudo docker exec test_1 python /local/test.py 1
sudo docker exec test_2 python /local/test.py 2
sudo docker exec test_3 python /local/test.py 3
```


# Bucket 使用
https://cloud.google.com/storage/docs/quickstart-gsutil
[Python直接读](https://cloud.google.com/storage/docs/xml-api/gspythonlibrary)



# AWS （直接ssh）
* chmod 400 Cloud-1.pem
* ssh -i "Cloud-1.pem" ubuntu@ec2-35-163-121-62.us-west-2.compute.amazonaws.com

## 安装AWS CML
*  `sudo pip install awscli --ignore-installed six`

## Configure it for use
* `http://docs.aws.amazon.com/cli/latest/userguide/installing.html#install-with-pip`
* `aws configure`
* `aws ec2 create-security-group --group-name my-sg --description "My security group"`
* 使用EC2
    * 创建组：
        * aws ec2 create-security-group --group-name devenv-sg --description "security group for development environment in EC2"
        * "GroupId": "sg-cf3d07b6"
    * 创建 key pair
        * aws ec2 create-key-pair --key-name devenv-key --query 'KeyMaterial' --output text > devenv-key.pem
        * chmod 400 devenv-key.pem
    * launch instance
        * aws ec2 run-instances --image-id ami-a9d276c9 --security-group-ids sg-cf3d07b6 --count 1 --instance-type t2.micro --key-name devenv-key --query 'Instances[0].InstanceId'
            * 得到一个ID
        * aws ec2 describe-instances --instance-ids i-ec3e1e2k --query 'Reservations[0].Instances[0].PublicIpAddress'
            * 得到instance 的ip
    * ssh to it
        * ssh -i devenv-key.pem ubuntu@ip address
    * cp 文件
        * 使用 scp 
        * scp -i devenv-key.pem ./prog.sh ubuntu@35.164.214.213:~
    * 执行文件
        * ssh -i devenv-key.pem ubuntu@35.164.214.213 -- ./prog.sh
    * terminate instance
        * aws ec2 terminate-instances --instance-ids $instance_id
* Use Elastic File system to share 
    * 创建新的group
        * aws ec2 create-security-group \
            --region us-west-2 \
            --group-name efs-walkthrough1-mt-sg \
            --description "Amazon EFS walkthrough 1, SG for mount target" \
            --vpc-id vpc-1cbfcc78
        * "GroupId": "sg-097e7370"
    * configure 可以有inbound network from EC2 instance to EFS
        * aws ec2 authorize-security-group-ingress \
            --group-id ID of the security group created for Amazon EFS mount target \
            --protocol tcp \
            --port 2049 \
            --source-group ID of the security group created for EC2 instance \
            --profile adminuser \
            --region us-west-2 
    * create efs 
        * aws efs create-file-system \
            --creation-token FileSystemForWalkthrough1 \
            --region us-west-2
        * "FileSystemId": "fs-cd5e9864"
    * 在EFS 建一个 我们 mount的点
        * aws efs create-mount-target \
            --file-system-id fs-cd5e9864 \   
            --subnet-id subnet-a95330cd \         
            --security-group sg-097e7370 \                                      
            --region us-west-2
        * subnet id 可以用 aws ec2 describe-instances \
            --instance-ids i-0f28c514bb3b24152 \
            --region us-west-2 | grep subnet 查
    * 在instance 中mount
        * 