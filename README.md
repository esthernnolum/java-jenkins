# java-jenkins
Build and Deploy simple java webapp using Jenkins and Ansible respectively

After initiating the simple-webapp pipeline, it proceeds to construct the application as per the directives outlined in the Jenkinsfile. It sequentially progresses through each stage delineated in the Jenkinsfile. Upon reaching the deployment stage, it initiates a freestyle Jenkins job, which employs an Ansible script (deploy.yml) to execute the artifact deployment process.
<img width="849" alt="image" src="https://github.com/esthernnolum/java-jenkins/assets/24988381/245169b5-bda5-4e47-b3b4-ca5e7a639dfa">
