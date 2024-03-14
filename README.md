# sshauth_namp_checking
Script to check ssh_auth in batch via nmap 

## Project Description
This project aim to performing ssh_auth checking for the subnet in batch. 
It will implement with Docker and Kuburnetes(minikube) for running the task as an application periodically. 

## File and Folder Structure

1. **dataset:**
- data/subnet.txt  /// to contain the subnet that want to check ssh_auth 
- data/output/  /// directory that contain ssh_auth result in .csv file format

2. **kubernetes**
- deployment.yaml /// for testing purpose that the container can run to perform ssh_auth checking task
- cronjob.yaml /// for performing ssh_auth checking task periodically (every 8 hours)

3. **Dockerfile**
- create a docker image for checking ssh_auth with python script as a application

4. **nmapscanning_subnet.py**
- python script for running ssh_auth checking based on the subnet in the dataset


## for setting up docker image in linux
1. install docker
2. docker build -t ssh .   /// this will create docker images in docker
3. docker run -v host/to/directory:/container/to/directory <docker image>    // run docker image with mount directory from host to container
   exmaple: docker run -v /home/hspe/Subnet_SSHauth/data/output/:/app/data/output ssh

occur error: 
Error16: PERMISSION DENIED 
solution: before building docker image, make sure the "output" directory is writable. Can check via ls -l and perform chmod 777 to the directory. 


## for setting up kurbunetes in linux 
1. install kubectl and minikube
   https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
   https://minikube.sigs.k8s.io/docs/start/
2. create minikube in docker
   minikube start --drive=docker
3. To mount the local machine to kurbenetes container
   minikube mount ~/Subnet_SSHauth/data/output/:/home/hspe/Subnet_SSHauth/data/output
   ** local/to/directory/:/kurbenetes/to/directory/
4. Pull the docker image from local machine to kurbenetes container
   eval $(minikube docker-env) ///enter using kurbenetes env
   go to the directory which contain DockerFile
   docker build -t ssh .
   docker images /// check the docker image is built
   eval $(minikube docker-env -u) ///exit the kurbenetes env
6. create deployment and cronjob
   kubectl apply -f cronjob.yaml
   kubectl apply -f deployment.yaml

occur error: 
1. PullFailure in kurbenetes
- you can check via minikube ssh and try to pull image in minikube container
- Authorized error when pulling docker, it can be solved by adding credential to docker
- grep docker /etc/group <<
- sudo usermod -aG docker <username>

2. Connection error, unable to perform docker build
- need to export NO_PROXY to bypass the connection
- export NO_PROXY=localhost,127.0.0.1,10.96.0.0/12,192.168.59.0/24,192.168.49.0/24,192.168.39.0/24

