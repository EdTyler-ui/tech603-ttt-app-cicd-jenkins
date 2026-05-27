- [using jenkins](#using-jenkins)
  - [what is CI? Benefits?](#what-is-ci-benefits)
    - [Benefits](#benefits)
  - [what is CD? Benefits?](#what-is-cd-benefits)
  - [what is jenkins](#what-is-jenkins)
  - [why use jenkins? pros and cons](#why-use-jenkins-pros-and-cons)
  - [stages of jenkins](#stages-of-jenkins)
  - [what alternatives are there for jenkins](#what-alternatives-are-there-for-jenkins)
  - [why build a pipeline? business value?](#why-build-a-pipeline-business-value)


# using jenkins 
- access jenkins server through ec2 instance on aws
- http://34.254.6.118:8080 : public ip for server 1 of jenkins
  - tech603-tf-ramon-jenkins-for-trainees-server1
- to create a project:
  - new item: give a name and freestyle project
  - configurations 
  - add linux coding to new build
  - confirm changes and press build project 
  - link to other projects

## what is CI? Benefits?

- continuous integration
- merging code
- triggered by: developers frequently pushing the code changes to a shared repository
- where to have manual approval and automate it
- tests are run automatically on code to see if it can be approved for production (integrated)

### Benefits
- help you identify and resolve bugs
  - acts as an extra saftey net
  - reduces costs
- helps to maintain a stable and functional software build

## what is CD? Benefits?

- continuous delivery (manual signoff/approval)
  - ensure software is always in a deployable state, ready/ can be pused to production at any time
  - often involves producing deployable artifact (package of code)
  - requires a manual release decision

- OR continuous deployment (automatically deploys code to production)
  - extends continuous delivery by automating the final step of deploying to production 
  - no manual intervention required
  - benefit which is also a disadvantage
    - human intervention is often safer
    - relies entirely on automated processes

## what is jenkins

- automation server
- open source
- primary used for cicd, but can automate much more

## why use jenkins? pros and cons

- benefits:
  - automation
  - extensibility: jenkins has over 1000 plugins
  - scalability: uses nodes and agents to distribute workload (run jobs)
  - community support
  - cross- platform: works across windows, linux, MacOS

- disadvantages
  - complex setup for beginners
  - maintenance overhead
  - resource- intensive when running multiple jobs (depends how optimised it is)
  - UI is outdated

## stages of jenkins

- typical CICD pipeline involves the following:
  - source code management (SCM), need to get the code from somewhere (git)
  - build: compile the code, build into executable artifact
  - test: automated tests (unit, integration, etc)
  - packaged: packaged into deployable artifact
  - if using continuous deployment, package is deployed to targert environment (testing, production)
  - monitor: observe performance, log issues after deployment

## what alternatives are there for jenkins

- gitlab ci
- github actions
- circle ci
- travis ci
- bamboo
- teamcity
- GoCD
- Azure pipelines

## why build a pipeline? business value?

- cost savings - automating repetitive processes
- faster time to market
- reduced risk 
- improved quality through continuous feedback and improvement

