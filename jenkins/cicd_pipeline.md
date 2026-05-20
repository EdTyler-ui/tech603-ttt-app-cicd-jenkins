- [set up and test ssh push to github](#set-up-and-test-ssh-push-to-github)
  - [overview of how to setup](#overview-of-how-to-setup)
    - [generating ssh key for git hub](#generating-ssh-key-for-git-hub)
    - [register the padlock](#register-the-padlock)
    - [add private key to ssh register](#add-private-key-to-ssh-register)
    - [create a test repo](#create-a-test-repo)
  - [CICD pipeline with jenkins](#cicd-pipeline-with-jenkins)
    - [create a repo for app v1.2](#create-a-repo-for-app-v12)
    - [starting job 1 (test)](#starting-job-1-test)
    - [add a webhook](#add-a-webhook)



# set up and test ssh push to github

## overview of how to setup
![ssh_into_github](imagess/ssh_github.png)

### generating ssh key for git hub
- cd into your ssh folder
- `ssh-keygen -t rsa -b 4096 -C "edwardtyler2002@gmail.com"` : using key rsa with 4096 bits
  - when prompted, enter 'edward-github-key'
  - asks for passphrase: press enter key
  - asks again: press enter key
- `ls` to see new folder containing ssh key

### register the padlock
- go to github -> profile -> ssh and gpg keys --> new ssh key
- name: 'edward-github-key'
- add the edward-github-key.pub to the description

### add private key to ssh register
- `eval 'ssh-agent -s'` : starts ssh agent in terminal and outputs private key
- `ssh-add edward-github-key` : adds private key to running ssh agent, uses key for authentication
- `ssh -T git@github.com` : tests your ssh connection to github
  - press yes to confirm

### create a test repo
- create a new repo with a readme (name: test_repo)
- move to github folder and use git clone
  - BUT! use the ssh link, not https
- edit the readme file and push it
- if push is successful, ssh github repo setup

## CICD pipeline with jenkins

### create a repo for app v1.2
- 'tech603-ttt-app-cicd-jenkins' : contains app folder with readme
- need to set up secure ssh deploy key
  - `ssh-keygen -t rsa -b 4096 -C "edwardtyler2002@gmail.com"` 
  - enter name of folder to keep private key
  - enter for passphrase
- go to settings in repo and deploy keys
  - add deploy key
  - give appropriate name 
  - copy public key into description
  - ALLOW READ/WRITE
  - sav key
  
### starting job 1 (test)
- log onto jenkins server -> new item
- enter item name -> click freestlye project -> ok
- configure page
  - give a description of your test
  - 'discard old builds' 
    - 'max # of builds to keep' = 5
  - click 'GitHub project'
    - provide url of HTTPS, REMOVE .GIT 
      - 'https://github.com/EdTyler-ui/tech603-ttt-app-cicd-jenkins/'
  - in 'source code management' -> press git
    - use ssh url for 'repository URL'
      - 'git@github.com:EdTyler-ui/tech603-ttt-app-cicd-jenkins.git'
    - now 'add' credentials
      - dropdown press jenkins
      - 'kind' : ssh username with private key
      - 'ID' : file name for private key (edward-jenkins-github-key)
      - 'Username' : same as ID
      - click private key and enter private key into text box (start with 5-, ends with 5-)
      - 'Passphrase' : leave blank
    - change brand specifier to 'dev' in branches to build
  - in build triggers
    - click 'GitHub hook trigger for GITScm polling'
  - build environment
    - click 'provide node and npm bin/folder to PATH'
  - build steps
    - execute shell
    - use following commands
      - cd app
      - npm ci
      - npm test
  - press save
- click 'build test'

### add a webhook
- go to webhooks in settings of repo in github
- 'add webhook'
- copy jenkins url
  - http://34.254.6.118:8080/github-webhook/
  - click add webhook