# monitoring-tools

This contains automation prometheus rule files configuration and alert manager configurations including gitlab-ci file.

# Alertmanager configuration

## Description
This project contains configuration files for Alertmanager. SP360 uses AWS Managed Prometheus   (AMP). Alertmanager requires two types of information:   
- rules for alerting (under the Rules Management tab in AWS AMP)
- configuration for alerting (under the Alert manager tab in AWS AMP)
This project contains these rules and configuration. These are uploaded via the AMP dashboard on AWS.   
**TBD** : Is there a way to automate the uploading of these files??  
**TBD** : How do we manage environment specific configuration   
**Note** : The organization of the configuration is constrained by AWS AMP. 

## Rules 
The rules are stored in the rules folder. The rules are orgainzed as individual yaml files depending on the type of rules. Following are the guidelines.  Note that these guidelines will 

- `infra`  
Contains Kubernetes infrastructure related alerts

- `api4xx`  
Contains alerts for 4XX alerts from all the microservices. This contains both warning and critical threshold alerts  

- `api5xx`  
Contains alerts for 4XX alerts from all the microservices. This contains both warning and critical threshold alerts  

- `***servicename***-alerts`  
Contains alerts specific to a microservice. These include latency (duration) alerts and any other alerts specific to the microservice.

- other types TBD  

## Configuration
The Alert manager configuration is a single yaml file (constrained by AWS AMP) that describes the following:

- alert message template  
The template describes how the alert message appears. This is defined using the Go templating language

- alert receivers  
The alert messages are sent to the receivers based on various rules defined. Typically receivers include tools such as PagerDuty, Slack, Email, etc. However, AWS AMP limits the receivers to SNS queues. The current SP360 implementation sends an email for the messages received into the SNS queue. Additional receiver flexibility can be implemented by using say lambda functions to integrate with PagerDuty and Teams.

## Environment specific configuration
The following configuration is unique to an environment:  
- alerting thresholds for the 4xx and 5xx warnings and critical erors
- alerting thresholds for microservice specific latencies
- any alerting thresholds for infrastructure, though these tend to be fairly constant
- the SNS queue(s) for alert receiver
- list of recepients for the various alerts

Presently, these are managed using a separate folder per environment. TBD Determine better ways to handle this requirement.

## Enhancements
### SNS Queues for receivers
Describe more granular queues for better control of alerts and recepients
### Connect SNS Queues to various alerting channels and recepients
Describe the various channels beyond emails - such as PagerDuty, Teams
Describe the approach for targeting recepients for targetted alerts.


Presently, the rules and config folders have se

