---
project: awless
stars: 4980
description: A Mighty CLI for AWS
url: https://github.com/wallix/awless
---

`awless` is a powerful, innovative and small surface command line interface (CLI) to manage Amazon Web Services.

Twitter | Wiki | Changelog

Why awless
==========

`awless` stands out by having the following characteristics:

-   small and hierarchical set of commands
-   a simple/powerful text templating language to create and **revert** fully-fledged infrastructures
-   wrapping/composing AWS API calls when necessary to enrich behaviour. Ex: ensure smart defaults, security best practices, etc.
-   local log of all your cloud modifications done through `awless` to list/revert past actions
-   sync to a local graph storage of your cloud representation
-   exploration of your cloud infrastructure and resources interrelations, **even offline** using the local graph storage
-   clearer and flexible terminal output's with: numerous formats (machine/human friendly), enriched resources's properties/relations when feasible
-   connect easily using awless' **smart SSH** to your private & public instances

For more read our FAQ below (how `awless` compares to other tools, etc.)

Install
=======

Choose one of the following options:

1.  On macOS, use homebrew: `brew tap wallix/awless; brew install awless`
2.  With `curl` (macOS/Linux), run: `curl https://raw.githubusercontent.com/wallix/awless/master/getawless.sh | bash`
3.  Download the latest `awless` binaries (Windows/Linux/macOS) from Github
4.  If you have Golang already installed, install from the source with: `go get -u github.com/wallix/awless`

If you have previously used the AWS CLI or aws-shell, you don't need to configure anything! Your config will be automatically loaded (i.e. ~/.aws/{credentials,config}) and `awless` will prompt for any missing info (more at our getting started).

Main features
=============

  
_Note that the video above is in APNG and requires a recent browser._

-   **Aliasing of resources through their natural name** so you don't have to always use cryptic ids that are impossible to remember
    
-   `awless show` : Explore the properties, relations, dependencies of a specific resource (even offline thanks to the sync) given only a _name_ (or id/arn).
    
    ```
    $ awless show jsmith --local
    ```
    
-   `awless list` : Clear and easy listing of multi-region cloud resources (subnets, instances, users, buckets, records, etc.) on AWS EC2, IAM, S3, RDS, AutoScaling, SNS, SQS, Route53, CloudWatch, CloudFormation, Lambda, etc. Listing filters via _resources properties_ or _resources tags_.
    
    ```
    $ awless list instances --sort uptime --local
    $ awless list users --format csv --columns name,created
    $ awless list volumes --filter state=use --filter type=gp2
    $ awless list volumes --tag-value Purchased
    $ awless ls vpcs --tag-key Dept --tag-key Internal --format tsv
    $ awless ls instances --tag Env=Production,Dept=Marketing
    $ awless ls instances --filter state=running,type=micro --format json
    $ awless ls s3objects --filter bucket=pdf-bucket -r us-west-2
    $ ...
    (see awless ls -h)
    ```
    
-   `awless run` : Create, update and delete complex infrastructures with smart defaults and sound auto-complete through awless templates.
    
    ```
    $ awless run ~/templates/my-infra.aws
    $ awless run https://raw.githubusercontent.com/wallix/awless-templates/master/linux_bastion.aws
    etc.
    ```
    
-   **Hundreds of powerful CRUD CLI one-liners** integrated in the awless templating engine:
    
    ```
    $ awless create instance -h
    $ awless create vpc -h
    $ awless attach policy -h
    $ ...
    (see awless -h)
    ```
    
-   `awless log` : Detailled and easy reporting of all the CLI template executions
    
-   `awless revert` : Revert of executed templates and resources creation
    
-   Create instances straight from a distro name. No need to know the region or AMI ;) (_free tier community bare distro only_, see `awless create instance -h`)
    
    ```
    $ awless create instance distro=debian
    $ awless create instance distro=coreos
    $ awless create instance distro=redhat::7.2 type=t2.micro
    $ awless create instance distro=debian:debian:jessie lock=true
    $ awless create instance distro=amazonlinux:amzn2
    etc.
    ```
    
-   Leveraging AWS `userdata` to provision instance on creation from remote (i.e http) or local scripts: `awless create instance ... userdata=/home/john/...`
    
-   `awless ssh` : Clean and simple SSH to public & private instances using only a name
    
    ```
    $ awless ssh my-production-instance
    $ awless ssh redis-prod --through jump-server
    $ awless ssh 34.215.29.221
    $ awless ssh db-private --private
    $ awless ssh 172.31.77.151 --port 2222 --through my-proxy --through-port 23
    $ ...
    (see awless ssh -h)
    ```
    
-   `awless switch` : Switch easily between AWS accounts (i.e. profile) and regions
    
    ```
    $ awless switch admin eu-west-2
    $ awless switch us-west-1
    $ awless switch mfa
    etc.
    ```
    
-   `awless` transparently syncs cloud resources locally to a graph representation in order for the CLI to leverage data and their relations in other awless commands and in an offline manner (more on the sync)
    
-   `awless sync` : Explicit and manual command to fetch & store resources locally. Then query & inspect your cloud offline
    
-   Output listing formats either human (**default display is Markdown-compatible tables**) or machine readable (csv, tsv, json, ...): `--format`
    
-   `awless inspect` : Leverage **experimental** and community inspectors which are interface implementation utilities to run analysis on your cloud resources graphs
    
    ```
    $ awless inspect -i bucket_sizer
    (see awless inspect -h)
    ```
    
-   `awless completion` : CLI autocompletion for Unix/Linux's bash and zsh
    

Getting started
===============

Take the tour at Getting Started (wiki) or read the introductory blog post about awless.

More articles:

-   Simplified Multi-Factor Authentication for AWS
-   Simplified user management for AWS
-   InfoWorld: Production-grade deployment of WordPress
-   Easy create & tear down of a multi-AZ CockroachDB cluster
-   Deploy Vuls.io to an AWS instance and scan for vulnerabilities

Awards
======

-   Top 50 Developer Tools of 2017
-   InfoWorld Bossie Awards 2017

FAQ
===

Here is a compilation of the question we often answer (thanks for asking them so that we can make things clearer!):

**There are already some AWS CLIs. What is `awless` unique approach?**

Three things that differentiates `awless` from other AWS CLIs:

-   It has its own **compiled and very simple templating language** to build AWS infrastructures.
-   Commands are made of _VERB + ENTITY \[+ param=value\]_ and are actually valid lines of the template language.
-   It transparently syncs to a local graph a representation of the cloud resources and their relations.

Leveraging and combining the points above, `awless` lays some strong foundations for plenty of current/future features/characteristic such as:

-   Wrapping AWS API calls to enrich them with before/after behaviour when interacting with the cloud
-   Having a small and hierarchical set of commands to intuitively interact with AWS
-   Enriching listing of resources using the local model and relations that are not calculated with other CLIs
-   Referencing and finding resources quickly avoiding cryptic IDs in favor of names, etc.
-   Exposing in the terminal relation between resources: lineage, siblings, etc.
-   Performing local analysis of your cloud
-   Having a smart SSH to easily connect to instances
-   etc.

**How do you create infrastructure with `awless`?**

You build infrastructure using `template files` or `command one-liners` that get compiled and run through `awless` builtin engine. See what the templating language looks like. Learn more about the way templates work

Note that all your actions against the cloud are logged. Templates are revertible/rollbackable.

**How does `awless` compares to `aws-shell` or `saws`?**

(Points above should also help answering this question)

`aws-shell` and `saws` are directly mapped to the official AWS CLI. Their **only** objective is to make you productive and help you manage exhaustively the sheer number of AWS services, options, etc.

`awless` addresses this UI/productivity concern differently: small and hierarchical set of commands; favoring enriched listing with relations showing over AWS exhaustive outputting of properties; more useful human/machine formats.

The main point is that **the UI/productivity concern is just a feature of awless and not its primary or only one**, so there is much more to the tool.

Also `aws-shell` and `saws` are exhaustive in their support of AWS services. `awless` is so far more infrastructure centric, with an emphasis on enriching the information about your real infrastructure. `awless` is able to add any new AWS service quickly if that fits and make sense (see wiki on how to add a new AWS service).

**How does `awless` compares to Terraform?**

Terraform is a great product! `awless` is much younger than Terraform and Terraform is much broader in scope.

The approach is different though. When creating insfrastructure `awless`:

-   favors simplicity with a straight forward, compiled and simple deployment language
-   employs an all-or-nothing deployment: do not keep state, etc.
-   `awless` does provide a rollback on any ran template.

**Does `awless` handles state when creating infrastructure (i.e. keep track of the changes)?**

Quoting from a logz.io/blog entry: _"Terraform is an amazing tool but a major challenge is managing the state file. Whenever you apply changes to your infrastructure, the entire managed body of code and created objects are tracked in the Terraform State file (.tfstate), which can reach hundreds of thousands of lines and must be managed carefully lest you incur large merge conflicts or unwanted resource changes"_, Ofer Velich.

As for now with `awless`, we have taken a different path: `awless` does not keep state of your cloud; it is more of an all-or-nothing deployment solution.

Note that `awless` logs (through rich and revertable logs) all your actions against the cloud and that you can revert any template ran.

About
=====

`awless` is an open source project created by Henri Binsztok, Quentin Bourgerie, Simon Caplette and François-Xavier Aguessy at WALLIX. `awless` is released under the Apache License and sponsored by Wallix.

```
Disclaimer: Awless allows for easy resource creation with your cloud provider;
we will not be responsible for any cloud costs incurred (even if you create a 
million instances using awless templates).
```

Contributors are welcome! Please head to Contributing (wiki) to learn more. Note that `awless` uses triplestore another project developped at WALLIX.
