---
project: faas
stars: 26045
description: OpenFaaS - Serverless Functions Made Simple
url: https://github.com/openfaas/faas
---

OpenFaaS ® - Serverless Functions Made Simple
---------------------------------------------

OpenFaaS® makes it easy for developers to deploy event-driven functions and microservices to Kubernetes without repetitive, boiler-plate coding. Package your code or an existing binary in an OCI-compatible image to get a highly scalable endpoint with auto-scaling and metrics.

**Highlights**

-   Ease of use through UI portal and _one-click_ install
-   Write services and functions in any language with Template Store or a Dockerfile
-   Build and ship your code in an OCI-compatible/Docker image
-   Portable: runs on existing hardware or public/private cloud by leveraging Kubernetes
-   CLI available with YAML format for templating and defining functions
-   Auto-scales as demand increases including to zero
-   Commercially supported Pro distribution by the team behind OpenFaaS

**Want to dig deeper into OpenFaaS?**

-   Trigger endpoints with either HTTP or events sources such as Apache Kafka and AWS SQS
-   Offload tasks to the built-in queuing and background processing
-   Quick-start your Kubernetes journey with GitOps from OpenFaaS Cloud
-   Go secure or go home with 5 must-know security tips
-   Learn everything you need to know to go to production
-   Integrate with Istio or Linkerd with Featured Tutorials
-   Deploy to Kubernetes or OpenShift

Overview of OpenFaaS (Serverless Functions Made Simple)
-------------------------------------------------------

> Conceptual architecture and stack, more detail available in the docs

### Code samples

You can generate new functions using the `faas-cli` and built-in templates or use any binary for Windows or Linux in a container.

Official templates exist for many popular languages and are easily extensible with Dockerfiles.

-   Node.js (`node12`) example:
    
    "use strict"
    
    module.exports \= async (event, context) \=> {
        return context
            .status(200)
            .headers({"Content-Type": "text/html"})
            .succeed(\`
            <h1>
                👋 Hello World 🌍
            </h1>\`);
    }
    
    _handler.js_
    
-   Python 3 example:
    
    import requests
    
    def handle(req):
        r \=  requests.get(req, timeout \= 1)
        return "{} => {:d}".format(req, r.status\_code)
    
    _handler.py_
    
-   Golang example (`golang-http`)
    
    package function
    
    import (
        "fmt"
        "net/http"
    
        handler "github.com/openfaas/templates-sdk/go-http"
    )
    
    // Handle a function invocation
    func Handle(req handler.Request) (handler.Response, error) {
        var err error
    
        message := fmt.Sprintf("Body: %s", string(req.Body))
    
        return handler.Response{
            Body:       \[\]byte(message),
            StatusCode: http.StatusOK,
        }, err
    }
    

Get started with OpenFaaS
-------------------------

### Official training resources

View our official training materials

### Official eBook and video workshop

The founder of OpenFaaS wrote _Serverless For Everyone Else_ to help developers understand the use-case for functions through practical hands-on exercises using JavaScript and Node.js. No programming experience is required to try the exercises.

The examples use the faasd project, which is an easy to use and lightweight way to start learning about OpenFaaS and functions.

Check out Serverless For Everyone Else on Gumroad

### OpenFaaS and Golang

Everyday Go is a practical, hands-on guide to writing CLIs, web pages, and microservices in Go. It also features a chapter dedicated to development and testing of functions using OpenFaaS and Go.

-   Everyday Golang

### Community blog and documentation

-   Read the documentation: docs.openfaas.com
-   Read latest news and tutorials on the Official Blog

Community Sponsorship
---------------------

OpenFaaS users can subscribe to a weekly Community Newsletter called Insiders Updates, to keep up to date with new features, bug fixes, events, tutorials and security patches. Insiders Updates are written by the project founder and distributed via GitHub Sponsors.

-   Get a Community Subscription

### Quickstart

> Here is a screenshot of the OpenFaaS Community Edition UI which was designed for ease of use. The inception function is being run which is available on the in the store.

Deploy OpenFaaS to Kubernetes, OpenShift, or faasd now with a deployment guide

### Video presentations

-   Meet faasd. Look Ma’ No Kubernetes! 2020
-   Getting Beyond FaaS: The PLONK Stack for Kubernetes Developers 2019
-   Serverless Beyond the Hype - Alex Ellis - GOTO 2018
-   How LivePerson is Tailoring its Conversational Platform Using OpenFaaS - Simon Pelczer 2019
-   Digital Transformation of Vision Banco Paraguay with Serverless Functions @ KubeCon 2018
-   Introducing "faas" - Cool Hacks Keynote at Dockercon 2017

### Community events and blog posts

Have you written a blog about OpenFaaS? Do you have a speaking event? Send a Pull Request to the community page below.

-   Read blogs/articles and find events about OpenFaaS

### Contributing

OpenFaaS Community Edition is written in Golang. All third-party contributions to the source code are made under the MIT license, additional restrictions apply to OpenFaaS CE as a whole, where contributions from OpenFaaS Ltd are licensed under the OpenFaaS CE EULA. Various types of contributions are welcomed whether that means providing feedback, testing existing and new feature or hacking on the source code.

#### How do I become a contributor?

Please see the guide on community & contributing

#### Dashboards

Example of a Grafana dashboard linked to OpenFaaS showing auto-scaling live in action: here

> OpenFaaS Pro auto-scaling dashboard with Grafana

An alternative community dashboard is available here

### Press / Branding / Website Sponsorship

-   Individual Sponsorships 🍻
    
    Users and contributors are encouraged to join their peers in supporting the OpenFaaS project through GitHub Sponsors.
    
-   OpenFaaS Pro for Production
    
    OpenFaaS Pro (Standard and For Enterprises) is built for production, the Community Edition (CE) is suitable for a Proof of Concept (PoC), for experimentation, and some limited internal use.
    
    Learn more about OpenFaaS editions
    
-   Website Sponsorship 🌎
    
    Companies and brands are welcome to sponsor openfaas.com, the Gold and Platinum tiers come with a homepage logo, see costs and tiers. Website sponsorships are payable by invoice.
    
-   Press / Branding 📸
    
    For information on branding, the press-kit, registered entities and sponsorship head over to the openfaas/media repo. You can also order custom SWAG or take part in the weekly Twitter contest #FaaSFriday
    
    Looking for statistics? This project does not use a mono-repo, but is split across several components. Use Ken Fukuyama's dashboard to gather accurate counts on contributors, stars and forks across the GitHub organisation.
    
    > Note: any statistics you gather about the openfaas/faas repository will be invalid, the faas repo is not representative of the project's activity.
    

### Governance

OpenFaaS ® is an independent open-source project created by Alex Ellis, which is being built and shaped by a growing community of contributors.

OpenFaaS is hosted by OpenFaaS Ltd (registration: 11076587), a company which also offers commercial services, homepage sponsorships, and support. OpenFaaS ® is a registered trademark in England and Wales.

### Users

View a selection of end-user companies who have given permission to have their logo listed at openfaas.com.

If you're using OpenFaaS please let us know on this thread. In addition, you are welcome to request to have your logo listed on the homepage. Thank you for your support.
