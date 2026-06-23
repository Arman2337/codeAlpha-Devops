# Task 2: Jenkins Remoting Project

## Overview
This project sets up Jenkins Remoting to connect remote Jenkins nodes. It demonstrates how to distribute build loads securely across different machines, freeing up the Jenkins Master node and utilizing different architectures or specific dependencies installed on remote agents.

## What is Jenkins Remoting?
Jenkins Remoting is a library and mechanism that Jenkins uses to manage distributed builds. The Jenkins Controller (Master) orchestrates the pipelines and UI, but the actual execution of tasks happens on Jenkins Agents (Nodes) via a remoting channel.

## Prerequisites
- Docker and Docker Compose installed.

## Setup Instructions

### 1. Start the Jenkins Master
Run the following command to start just the master node initially:
```bash
docker-compose up -d jenkins-master
```
1. Access Jenkins at `http://localhost:8081/jenkins`.
2. Get the initial admin password from the docker logs: `docker logs jenkins-master`.
3. Complete the initial setup wizard (install suggested plugins).

### 2. Configure Node Isolation & Add Agent
We must configure Jenkins to offload work securely.
1. Go to **Manage Jenkins** -> **Nodes**.
2. Click **New Node**.
3. Node Name: `remote-agent`, Type: Permanent Agent. Click Create.
4. Set Remote root directory: `/home/jenkins/agent`.
5. Labels: `remote-agent`.
6. Usage: **Only build jobs with label expressions matching this node** (This enforces node isolation so jobs don't accidentally run on master).
7. Launch method: **Launch agent by connecting it to the controller**.
8. Save.
9. Jenkins will give you a **secret** token for this node.

### 3. Connect the Remote Agent
1. Open the `docker-compose.yml` file in this directory.
2. Replace `your_agent_secret_here` with the secret token you got from Jenkins.
3. Start the agent:
```bash
docker-compose up -d --build jenkins-agent
```
4. Refresh the Jenkins Node page. The agent should now be connected!

### 4. Run the Distributed Build
1. In Jenkins, create a new **Pipeline** job.
2. Under Pipeline, choose "Pipeline script from SCM" (or just copy-paste the contents of the `Jenkinsfile` provided in this directory).
3. The `Jenkinsfile` explicitly specifies `agent { label 'remote-agent' }`.
4. Run the build. You will see in the console output that the execution happens on the connected remote agent.

## Key Concepts Learned
- **Jenkins Remoting**: Using JNLP/TCP protocols to establish secure controller-agent communication.
- **Node Isolation**: Reserving the Jenkins master only for orchestration and running jobs strictly on designated agents.
- **Load Distribution**: Scaling CI/CD by adding multiple nodes.
