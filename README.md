# Jenkins Pipeline with Docker Compose

This project involves setting up a Jenkins pipeline to automate the build, testing, and deployment process of a Python Flask weather application. The pipeline utilizes Docker Compose for creating a child environment, runs unit tests, pushes the built image to a Docker repository, and deploys both the application and nginx to a remote virtual machine using a Docker daemon ([Configure remote access for Docker daemon](https://docs.docker.com/config/daemon/remote-access/)). Additionally, the pipeline integrates with Slack to send notifications about the pipeline status.
![Image](GitHub-Docker.png "Architecture of the project")

## Badges

![Jenkins](https://img.shields.io/badge/jenkins-%232C5263.svg?style=for-the-badge&logo=jenkins&logoColor=white)

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)

![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white)

![Slack](https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white)

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
