http://insurance.lab.local:8082

<img width="1536" height="1024" alt="a_clean_documentation_style_presentation_slide png" src="https://github.com/user-attachments/assets/39a5b211-21ec-41c8-95b0-6f4097d2ce03" />

```
Started by user Developer 
Obtained Jenkinsfile from git https://github.com/arkinfotech24/insurance-site.git
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/jenkins_home/workspace/insurance-site-pipeline
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Checkout SCM)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
Cloning the remote Git repository
Cloning repository https://github.com/arkinfotech24/insurance-site.git
 > git init /var/jenkins_home/workspace/insurance-site-pipeline # timeout=10
Fetching upstream changes from https://github.com/arkinfotech24/insurance-site.git
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
 > git fetch --tags --force --progress -- https://github.com/arkinfotech24/insurance-site.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/arkinfotech24/insurance-site.git # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
Avoid second fetch
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision b5df5b1543eccccf4eb23338774f79c0bf65d6ce (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f b5df5b1543eccccf4eb23338774f79c0bf65d6ce # timeout=10
Commit message: "Force Jenkins to use only deploy SSH key"
 > git rev-list --no-walk b5df5b1543eccccf4eb23338774f79c0bf65d6ce # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] withEnv
[Pipeline] {
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Checkout)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/insurance-site-pipeline/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/arkinfotech24/insurance-site.git # timeout=10
Fetching upstream changes from https://github.com/arkinfotech24/insurance-site.git
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
 > git fetch --tags --force --progress -- https://github.com/arkinfotech24/insurance-site.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision b5df5b1543eccccf4eb23338774f79c0bf65d6ce (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f b5df5b1543eccccf4eb23338774f79c0bf65d6ce # timeout=10
Commit message: "Force Jenkins to use only deploy SSH key"
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Validate Files)
[Pipeline] sh
+ pwd
/var/jenkins_home/workspace/insurance-site-pipeline
+ ls -la
total 20
drwxr-sr-x 3 jenkins jenkins 4096 Jun 30 18:30 .
drwxr-sr-x 6 jenkins jenkins 4096 Jun 30 18:29 ..
drwxr-sr-x 8 jenkins jenkins 4096 Jun 30 18:30 .git
-rw-r--r-- 1 jenkins jenkins 2144 Jun 30 18:30 Jenkinsfile
-rw-r--r-- 1 jenkins jenkins 1028 Jun 30 18:30 index.html
+ test -f index.html
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Verify SSH Key)
[Pipeline] sh
+ ls -l /var/jenkins_home/.ssh/insurance_deploy_key
-rw------- 1 jenkins jenkins 411 Jun 30 17:53 /var/jenkins_home/.ssh/insurance_deploy_key
+ chmod 600 /var/jenkins_home/.ssh/insurance_deploy_key
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Deploy to Web Server)
[Pipeline] sh
+ echo Deploying Insurance Website...
Deploying Insurance Website...
+ scp -F /dev/null -i /var/jenkins_home/.ssh/insurance_deploy_key -o IdentityAgent=none -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PubkeyAuthentication=yes -o PasswordAuthentication=no -o StrictHostKeyChecking=no index.html sysadmin@192.168.1.181:/tmp/index.html
+ ssh -F /dev/null -i /var/jenkins_home/.ssh/insurance_deploy_key -o IdentityAgent=none -o IdentitiesOnly=yes -o PreferredAuthentications=publickey -o PubkeyAuthentication=yes -o PasswordAuthentication=no -o StrictHostKeyChecking=no sysadmin@192.168.1.181 sudo cp /tmp/index.html /var/www/html/index.html && sudo systemctl restart httpd
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Declarative: Post Actions)
[Pipeline] cleanWs
[WS-CLEANUP] Deleting project workspace...
[WS-CLEANUP] Deferred wipeout is used...
[WS-CLEANUP] done
[Pipeline] echo
Insurance website deployed successfully.
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
```
<img width="1909" height="912" alt="image" src="https://github.com/user-attachments/assets/c507b452-20cb-4a87-9ace-bd26136d8695" />
