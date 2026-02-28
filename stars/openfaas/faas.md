---
project: faas
stars: 26100
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

OpenFaaS Tiers and Pricing
--------------------------

This repository is part of OpenFaaS Community Edition (CE), which is licensed for non-commercial use by individuals, and a time-limited trial for commercial Proof Of Concepts (PoC). Internal use within a company or business requires a license.

OpenFaaS CE:

-   has usage restrictions, which you can learn about in the OpenFaaS CE EULA
-   has basic or primitive features and capabilities compared to the commercial versions
-   is not licensed for commercial use of any kind beyond an initial trial period

OpenFaaS Standard and OpenFaaS for Enterprises are full and distinct commercial products.

They are maintained and developed independently, by a full-time team, with commercial support, and active maintenance for CVEs, and updates in the Kubernetes and Cloud Native ecosystem.

Learn more about the tiers at https://www.openfaas.com/pricing/

Overview of OpenFaaS (Serverless Functions Made Simple)
-------------------------------------------------------

> Conceptual architecture and stack, more detail available in the docs

### Code samples

You can scaffold a new function using the `faas-cli new` command passing in the name of the function and the language template you want to use i.e. `faas-cli new --lang node20 stripe-webhooks`.

Official templates exist for many popular languages and are easily extensible with Dockerfiles.

Learn about OpenFaaS templates in the docs

-   Node.js (`node20`) example:
    
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
    
-   Python 3 example (`python3-http`):
    
    def handle(event, context):
        return {
            "statusCode": 200,
            "body": "Hello from OpenFaaS!"
        }
    
    _handler.py_
    
-   Golang example (`golang-middleware`)
    
    package function
    
    import (
     	"fmt"
     	"io"
     	"net/http"
    )
    
    func Handle(w http.ResponseWriter, r \*http.Request) {
        var input \[\]byte
        
       	if r.Body != nil {
        		defer r.Body.Close()
        		body, \_ := io.ReadAll(r.Body)
        		input \= body
       	}
        
       	w.WriteHeader(http.StatusOK)
       	w.Write(\[\]byte(fmt.Sprintf("Body: %s", string(input))))
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

### Quickstart

> Here is a screenshot of the OpenFaaS Community Edition UI which was designed for ease of use. The inception function is being run which is available on the in the store.

Deploy OpenFaaS to Kubernetes, OpenShift, or faasd now with a deployment guide

OpenFaaS Standard and OpenFaaS for Enterprises have their own, brand new dashboard with multi-tenancy support, learn more about the OpenFaaS Dashboard.

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

-   Website Sponsorship 🌎
    
    If you'd like to gain visibility by displaying your logon on the openfaas.com homepage, feel free to reach out via email or browse the tiers via GitHub Sponsors.
    
-   Press / Analysts
    
    Looking at these repositories for commit counts and activity? All public repositories are part of OpenFaaS CE, a limited version of OpenFaaS aimed at giving people a low-barrier trial experience without having to sign up with a credit card. OpenFaaS CE is maintained on a best effort basis, but is not "OpenFaaS" itself. All OpenFaaS product development is done in private repositories, and cannot be tracked by third parties or by simply browsing GitHub.
    
    How are GitHub Stars and Forks counted? OpenFaaS CE is not a mono-repo, you cannot simply look at one repository and say "ah that's the count" - statistics are gathered from the whole GitHub organisation.
    

### Governance

OpenFaaS ® is an independent open-source project created by Alex Ellis, which is being built and shaped by a growing community of contributors.

OpenFaaS is hosted by OpenFaaS Ltd (registration: 11076587), a company which also offers commercial services, homepage sponsorships, and support. OpenFaaS ® is a registered trademark in England and Wales.

### Users

View a selection of end-user companies who have given permission to have their logo listed at openfaas.com.
