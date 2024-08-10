CI/CD : Jenkins Setup and Pipeline Creation
1. Install Jenkins


   • Objective: Set up Jenkins on your server to manage CI/CD pipelines.


    • Steps:
        ◦ Install Jenkins on your server or virtual machine.
        ◦ Ensure Jenkins is running and accessible via its web interface.
        ◦ Install necessary Jenkins plugins for Docker and Git integration.



3. Create a Freestyle Pipeline
    • Objective: Create a Jenkins Freestyle job to manage basic Docker container operations.
    • Steps:
        ◦ Create a Freestyle project in Jenkins.
        ◦ Configure the job to execute shell commands for listing and pulling Docker containers (e.g., Nginx).
        ◦ Save and run the job to verify it executes correctly.



4. Create a Parameterized Pipeline with Jenkinsfile
    • Objective: Set up a Jenkins Pipeline to build and push a Docker container, with a parameter for the Docker image tag, triggered by changes in the Test branch.
    • Steps:
        ◦ Create a new Pipeline job in Jenkins.
        ◦ Configure the job to pull the Jenkinsfile from the Test branch of your Git repository.
        ◦ Set up the pipeline to include a parameter for the Docker image tag.
        ◦ Save and run the job, specifying the Docker image tag during execution.
