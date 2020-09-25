# Udacity DevOps Capstone Project

<h2>Project Overview</h2>

<p> In this project, I applied the skills and knowledge which was developed throughout the Cloud DevOps Nanodegree program. These include:</p>

<ul>
	<li>Working in AWS</li>
	<li>Using Jenkins to implement Continuous Integration and Continuous Deployment</li>
	<li>Building pipelines</li>
	<li>Working with Ansible and CloudFormation to deploy clusters</li>
	<li>Building Kubernetes clusters</li>
	<li>Building Docker containers in pipelines</li>
</ul>

***

<p>I developed a CI/CD pipeline for microservices applications with rolling deployment. I developed Continuous Integration steps, such as typographical checking (aka “linting”). I also developed Contiguous Deployment steps. These includes:</p>

<ul>
	<li>Pushing the built Docker containers to the Docker repository</li>
	<li>Deploying these Docker containers to a small Kubernetes cluster. For Kubernetes cluster I used AWS EKS. To deploy my Kubernetes cluster using Cloudformation. I ran these from Jenkins as an independent pipeline.</li>
</ul>

***

<h2>Environment Setup</h2>

<ul>
  <li>Install Jenkins, Dokcer, kubectl and all the necessary plugins in the EC2 Instance</li>
  <li>Create a Dockerfile</li>
  <li>Create a Jenkinsfile for deploying a cluster</li>
  <li>Create a Jenkinsfile for deploying docker to EKS</li>
</ul>

<h2>Cleaning App</h2>

<ul>
  <li>Run <code>docker system prune</code> to clean up </li>
</ul>

***
GitHub @ https://github.com/GemMaddy/batram-Capstone/
***
DockerHub @ https://hub.docker.com/repository/docker/gemmaddy/capstone
