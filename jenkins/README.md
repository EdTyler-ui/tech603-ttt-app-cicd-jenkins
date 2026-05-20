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