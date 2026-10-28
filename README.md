#1 : jira-github-jenkins

go to jira -> space -> crate new (asd practical) ->select kanban -> board -> to do -> assign 5 tasks -> create a github repo -> tick the readme on -> jira -> asd practical -> development -> connect -> github-jira -> go to repo -> commit a change -> back to board -> (development:commit) -> check commits ..(commits will be displayed)...(remember add commit msg with  eg.DEVOPS4 / task key)....aws -> login to aws console ->

...................................................................................................................................................................

#2 : git

To install Git and demonstrate `init`, `add`, `commit`, `push`, `pull`, `branch`, `merge`, and `diff` commands.

Steps to Perform
Check Git Installation
Open PowerShell or Ubuntu terminal and execute:
```bash
git --version
```
If Git is not installed, download it from https://git-scm.com/downloads.
2. Configure Git
Set your Git username and email:
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
3. Create a Project
```bash
mkdir git-practical
cd git-practical
```
Create a file:
```bash
nano file.txt
```
Write some text, then save with `Ctrl + O`, press `Enter`, and exit using `Ctrl + X`.
Initialize Git
```bash
git init
``
This initializes a local Git repository.
Add and Commit Files
```bash
git status
git add file.txt
git commit -m "First commit"
```
- `git add`: Stages changes.
- `git commit`: Saves a snapshot in Git history.
Demonstrate Git Diff
Edit the file again:
```bash
nano file.txt
```
Add another line and save. Then execute:
```bash
git diff
```
This displays changes that have not yet been staged.
7. Create and Switch Branches
```bash
git branch feature
git switch feature
```
Edit `file.txt`, then stage and commit the changes:
```bash
git add file.txt
git commit -m "Added feature"
```
Merge Branches
Switch back to the main branch:
```bash
git switch main
```
If your initial branch is named `master`, use `git switch master` instead.
Merge the feature branch:
```bash
git merge feature
```
Push Code to GitHub
Create an empty GitHub repository named `git-practical`. Then connect your local repository:
```bash
git remote add origin https://github.com/YOUR-USERNAME/git-practical.git
```
If your current branch is `master`, rename it to `main`:
```bash
git branch -M main
```
Push your code:
```bash
git push -u origin main
```
Replace `YOUR-USERNAME` with your GitHub username. Authenticate if prompted.
10. Pull Changes from GitHub
```bash
git pull origin main
```

...................................................................................................................................................................

#3 : jenkins-pipeline


# Practical 3: Continuous Integration Using Jenkins Pipeline

## Aim
To install Jenkins and perform Continuous Integration using a Jenkinsfile stored in a remote GitHub repository, with SCM polling every 5 minutes.

## Steps to Perform

### 1. Start Jenkins
1. Start the Jenkins service on Windows.
2. Open `http://localhost:8080` in your browser.
3. Log in to the Jenkins dashboard.

### 2. Create a GitHub Repository
Create a repository named `jenkins-ci-practical` containing:
- `index.html` – Sample application file
- `Jenkinsfile` – Pipeline definition

### 3. Create the Jenkinsfile
Create a file named `Jenkinsfile` in the repository and add:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'echo Building application...'
                bat 'if not exist index.html exit /b 1'
            }
        }

        stage('Test') {
            steps {
                bat 'echo Testing application...'
                bat 'git --version'
            }
        }

        stage('Integration Complete') {
            steps {
                bat 'echo Continuous Integration Successful!'
            }
        }
    }
}
```

Commit and push the files to GitHub.

### 4. Create a Jenkins Pipeline Job
1. Open Jenkins and click **New Item**.
2. Enter the job name `CI-Pipeline`.
3. Select **Pipeline** and click **OK**.
4. Under Pipeline, select **Pipeline script from SCM**.
5. Select **Git** as SCM.
6. Enter your GitHub repository URL.
7. Set Branch Specifier to `*/main`.
8. Set Script Path to `Jenkinsfile`.
9. Click **Save**.

### 5. Enable Poll SCM
1. Open the job's **Configure** page.
2. Under **Build Triggers**, enable **Poll SCM**.
3. Enter this schedule:

```text
H/5 * * * *
```

4. Click **Save**.

This tells Jenkins to check the remote repository approximately every 5 minutes. A new build is triggered when Jenkins detects relevant SCM changes.

### 6. Run the Pipeline
1. Open the `CI-Pipeline` job.
2. Click **Build Now**.
3. Open the latest build and select **Console Output**.
4. Verify that the Checkout, Build, Test, and Integration Complete stages succeed.

### 7. Test Automatic Change Detection
1. Open the GitHub repository.
2. Edit `index.html` and commit the change.
3. Wait for the next SCM polling check.
4. Open Jenkins and verify that a new build starts after the change is detected.




...................................................................................................................................................................

#4 : lambda-dynamodb tbl

...................................................................................................................................................................

#5 : ansible

# Practical 5: Software Provisioning and Configuration Using Ansible

## Aim
To install Ansible and perform software provisioning and configuration on the localhost machine.

## Steps to Perform

### 1. Update Ubuntu Packages

Open the Ubuntu terminal and execute:

```bash
sudo apt update
```

### 2. Install Ansible

```bash
sudo apt install -y ansible
```

Verify installation:

```bash
ansible --version
```

### 3. Create a Project Folder

```bash
mkdir ansible-practical
cd ansible-practical
```

### 4. Create an Inventory File

```bash
nano inventory
```

Write:

```ini
[local]
localhost ansible_connection=local
```

Save using `Ctrl + O`, press `Enter`, and exit using `Ctrl + X`.

### 5. Create an Ansible Playbook

```bash
nano playbook.yml
```

Enter the following YAML code:

```yaml
---
- name: Configure localhost
  hosts: localhost
  connection: local
  become: true

  tasks:
    - name: Install Nginx web server
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: true

    - name: Create a web page
      ansible.builtin.copy:
        dest: /var/www/html/index.html
        content: |
          <h1>Ansible Practical 5</h1>
          <p>Localhost configured successfully.</p>
        mode: "0644"
```

Save and exit Nano.

### 6. Check the Playbook Syntax

```bash
ansible-playbook -i inventory playbook.yml --syntax-check
```

Expected output:

```text
playbook: playbook.yml
```

### 7. Execute the Playbook

```bash
ansible-playbook -i inventory playbook.yml --ask-become-pass
```

Enter your Ubuntu password when prompted for the privilege-escalation password.

Ansible will install Nginx and create the web page.

### 8. Verify the Configuration

Check whether Nginx is installed:

```bash
nginx -v
```

Check whether the web page was created:

```bash
cat /var/www/html/index.html
```

If Nginx is running and port 80 is accessible, open `http://localhost` in your browser to view the page. If it is not running, start it with:

```bash
sudo service nginx start
```

### 9. Check the Playbook Again

Run the playbook a second time:

```bash
ansible-playbook -i inventory playbook.yml --ask-become-pass
```
Ansible should report that the configuration is already in the desired state wherever no changes are needed.


...................................................................................................................................................................


#6 : docker-ecommerce-app

Deploy an E-Commerce Website Using Docker
To install Docker and deploy an e-commerce web application consisting of at least two web pages.

Steps to Perform
1. Create a Project Folder
Open Ubuntu and execute:

```bash
mkdir ecommerce-app
cd ecommerce-app
```
2. Create the Home Page
```bash
nano index.html
```
Write the HTML code for the home page. Save using `Ctrl + O`, press `Enter`, and exit using `Ctrl + X`.
3. Create the Products Page
```bash
nano products.html
```
Write the HTML code to display products, prices and descriptions. Save and exit using `Ctrl + O`, `Enter`, and `Ctrl + X`.
4. Create the Dockerfile
```bash
nano Dockerfile
```
Enter the following code:

```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
```
Save and exit.
5. Build the Docker Image
Ensure Docker Desktop is running, then execute:

```bash
docker build -t ecommerce-image .
```
6. Run the Docker Container
```bash
docker run -d --name ecommerce-container -p 8091:80 ecommerce-image
```
7. Verify Deployment
Open these URLs in your browser:

- Home page: `http://localhost:8091`
- Products page: `http://localhost:8091/products.html`

8. Check the Container
```bash
docker ps
```
Confirm that `ecommerce-container` is running.
Successfully created a two-page e-commerce web application and deployed it using Docker.

....index.html code

<!DOCTYPE html>
<html>
<head>
    <title>My E-Commerce Store</title>
</head>
<body>
    <h1>Welcome to My E-Commerce Store</h1>
    <p>Shop for your favorite products!</p>

    <h2>Our Store</h2>
    <p>We offer quality products at affordable prices.</p>

    <a href="products.html">View Products</a>
</body>
</html>


....products.html

<!DOCTYPE html>
<html>
<head>
    <title>Our Products</title>
</head>
<body>
    <h1>Our Products</h1>

    <h2>Product 1: Headphones</h2>
    <p>Price: Rs. 999</p>
    <p>High-quality headphones for music lovers.</p>

    <h2>Product 2: Smart Watch</h2>
    <p>Price: Rs. 1499</p>
    <p>A stylish smartwatch for everyday use.</p>

    <h2>Product 3: Backpack</h2>
    <p>Price: Rs. 799</p>
    <p>A durable backpack for college and travel.</p>

    <a href="index.html">Back to Home</a>
</body>
</html>



...................................................................................................................................................................

#7 : terraform ec2

...................................................................................................................................................................

#8 : lambda-date-time

...................................................................................................................................................................

#9 : airflow
in ubuntu terminal :
sudo apt update
sudo apt install -y python3 python3-venv python3-pip python3-dev build-essential
python3 --version
mkdir -p ~/airflow-practical
cd ~/airflow-practical
python3 -m venv venv
source venv/bin/activate
python -m pip install --upgrade pip
AIRFLOW_VERSION=3.3.2
PYTHON_VERSION="$(python -c 'import sys; print(f"{sys.version_info.major}.{sys.version_info.minor}")')"
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
airflow version
....
export AIRFLOW_HOME=~/airflow
airflow standalone
...if 8080 doesnt work- 
cd ~/airflow-practical -> source venv/bin/activate -> export AIRFLOW_HOME=~/airflow 
(airflow api-server --port 8081)..type this in other ubuntu terminal
now open http://localhost:8081 and login 
use this to get credentials : cat ~/airflow/simple_auth_manager_passwords.json.generated
.....create a DAG file:
nano ~/airflow/dags/date_time_dag.py
{

import pendulum
from airflow.sdk import dag, task


@dag(
    dag_id="date_time_dag",
    schedule="30 9 * * 3",
    start_date=pendulum.datetime(
        2026, 10, 28, tz="Asia/Kolkata"
    ),
    catchup=False,
    tags=["practical"]
)
def date_time_dag():

    @task
    def display_date_time():
        current_time = pendulum.now("Asia/Kolkata")
        print("Current Date:", current_time.date())
        print("Current Time:", current_time.strftime("%H:%M:%S"))

    display_date_time()


date_time_dag()

}
->airflow dags list
...check date_time_dag. appears in the list
next go to airflow page refresh and check for date_time_dag.
run and trigger 

...................................................................................................................................................................


#10 : jenkins-docker
(Status: Downloaded newer image for nginx:alpine)...run in powershell when build fails

Jenkins Pipeline to Deploy a Web Application Using Docker
To create a Jenkins pipeline using a Jenkinsfile stored in a remote GitHub repository and deploy a web application using Docker.

Steps to Perform

1. Create GitHub Repository
Create a repository named `docker-jenkins-app` containing:
- `index.html` – Web page
- `Dockerfile` – Docker image configuration
- `Jenkinsfile` – Pipeline script

2. Create the Dockerfile
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
```

3. Create the Jenkins Pipeline
1. Open Jenkins at `http://localhost:8080`.
2. Click **New Item** and select **Pipeline**.
3. Under Pipeline Definition, select **Pipeline script from SCM**.
4. Select Git and enter the GitHub repository URL.
5. Set the branch to `*/main` and Script Path to `Jenkinsfile`.
6. Save the configuration.

4. Run the Pipeline
1. Start Docker Desktop and ensure Docker Engine is running.
2. If Docker Hub image pulling fails, test with:
   ```powershell
   docker pull nginx:alpine
   ```
3. Open the Jenkins job and click **Build Now**.
4. Check **Console Output** for successful execution.

 Verify Deployment
1. Open PowerShell and run:
   ```powershell
   docker ps
   ```
2. Verify that the `devops-store` container is running.
3. Open `http://localhost:8090` in a browser.
4. Confirm that the web application is displayed.
   
1. **Checkout:** Fetch source code from GitHub.
2. **Build:** Build the Docker image.
3. **Test:** Verify the Docker image and HTML file.
4. **Deploy:** Run the application inside a Docker container.

