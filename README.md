# docu-connector
## Introduction

This repository contains a module that extends Mule 4 to simplify JWT-based authentication with the [DocuSign eSignature service](https://www.docusign.com/products/electronic-signature).  
Once incorporated into your Anypoint Studio project, it provides a single Mule component which simplifies the process of obtaining an OAuth token, for a specified DocuSign user, which can then be used in the Authorization header of any subsequent HTTPS-based requests to the [DocuSign REST API](https://developers.docusign.com/esign-rest-api).

## Prerequisites

It is assumed that you already have access to a demo/sandbox DocuSign account, and are able to perform the one-time authentication as the user you wish to impersonate within your Mule flow - see the "Provide Consent" section below.

## Installation

Download the release JAR file and load it into your Anypoint Studio Maven repository.
Once present, you can add a dependency to your pom.xml to incorporate the module:

```xml
<dependency>  
  <groupId>uk.org.mule.docu</groupId>  
  <artifactId>docu-connector</artifactId>  
  <version>0.2.0</version>  
  <classifier>mule-plugin</classifier>  
</dependency>  
```

## Provide Consent

Before you can use the connector, you will need to provide consent for it to impersonate your DocuSign user, click on the link below to do so:

> [Provide Consent](https://account-d.docusign.com/oauth/auth?response_type=code&scope=signature%20impersonation&client_id=480bf239-9265-4f94-a333-5b1eebde0300&redirect_uri=https://www.mule.org.uk/docu-connector/)

## Usage
The "Get user access token" component can be placed into your flow like any other component, with the access token being assigned to a target variable of your choosing:

![Get user access token target](/images/get-user-access-token-target.png)

The component requires that an associated configuration is defined that specifies:

+ The Base Path for the OAuth token request
    + "account-d.docusign.com" (for a demo/sandbox account), or
    + "account.docusign.com" (for a production account)
+ The guid identifier for the DocuSign user that you wish to have the docu-connector impersonate

![DocuSign Config](/images/docusign-config.png)

The access token returned can be incorporated into the "Authorization" header of any subsequent HTTPS requests to the DocuSign service for the following hour:

![HTTP Authorization Header](/images/http-authorized-request.png)
