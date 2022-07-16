## Good Day Everyone!

Hope you’re all doing well.

I’m writing this article to share my learnings while working on different projects involving multiple skills in Telecommunications and Information Technology domains.

Recent project has enabled me with the skills such as GitLab, Ansible, Docker, and Shell script.

## Use case
Package management on multiple Linux machines using GitLab pipeline

## Tools
Following DevOps tools were used in implementing the CD pipeline

- GitLab — Version control, project repository, CD pipeline

- GitLab-Runner — Trigger the pipeline stages

- Linux Machines — Centos VMs for controller node and target nodes

- Ansible — Implements changes on the target nodes

- Shell Scripting — Execute playbooks, used in the pipeline stages

## Architecture
Below is a high level architecture of the setup

![Architecture](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7c3gb9k9w6x7ckzsw3sz.png)

## Prerequisites

- [GitLab ](https://gitlab.com)account where you can store your project and configure CD pipeline.

- [Gitlab-runner](https://docs.gitlab.com/runner/install/) package downloaded and installed on the controller node, which is basically a Linux machine.

![Gitlab-runner](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/axfsxne247lin1tkxb5l.png)

- Gitlab-runner for the project has been registered on the controller node. Navigate to **GitLab → Project → Settings → CI/CD → Runners**. Scroll down to the steps where it shows the steps to register gitlab-runner on the controller node.

![register-process](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cjcopff6fl07vc8p4usu.png)

- Register the runner on the controller node with the details mentioned above. For this exercise, shell executor for gitlab-runner is used to trigger the gitlab jobs on the target machines.

![register-runner](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kx4dsndxt83ppfmj8nw8.png)

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed on the controller node. For testing purpose, inventory file consists of the entry for the localhost

```
targetvm1 ansible_host=127.0.0.1 ansible_user=root
```

![ansible](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ks2y94y3q5pjasdr0gb4.png)

- [SSH password-less connectivity](https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/) established between the controller node (gitlab-runner user) and target nodes (any user)(linux machines)

![ssh-connection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qmd1n3v1yrndgh5049du.png)

- [Git](https://git-scm.com/download/linux) is installed on your local machine to clone, pull, & push the changes in your local repository

![git](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fn4ebrf1ug8tn7346v0t.png)

## Implementation

- Clone the project from the [Github](https://github.com/prabhatsingh014/pkg-mgmt.git) on your local machine

![github](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z7vybo8ljrc16yu20xvv.png)

- Change to the directory and edit the variables.yml and provide values against the parameters mentioned

![variables](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6eumbrfayvzi5dq1rhh7.png)

- Commit the changes to your local repository and push to the remote repository

![commit-change](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6ei6xdf9paq9yc7wsrcb.png)

![push-change](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vxgwl01fangf0zndl5lp.png)

- As soon as you push the changes, a pipeline will be triggered on GitLab. Navigate to **GitLab → Project → CI/CD → Pipelines**.

- Stages include in the pipeline: prechecks, prebackup, activity, postbackup, postchecks.

![pipeline-stages](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8nnzbabke0qboib5bbpm.png)

![pipeline-status](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/f83osiw32jhulb84otwe.png)

Ansible playbooks can further be modified for different operating systems, system checks, system backup before and after the installation, upgrade, & removal of the packages.
