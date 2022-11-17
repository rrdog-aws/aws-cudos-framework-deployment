# Cloud Intelligence Dashboards (CUDOS Framework)

[![PyPI version](https://badge.fury.io/py/cid-cmd.svg)](https://badge.fury.io/py/cid-cmd)

## Welcome to Cloud Intelligence Dashboards (CUDOS Framework) automation repository
This repository contains CloudFormation templates and Command Line tool (cid-cmd) for managing various dashboards provided in AWS Well Architected LAB [Cloud Intelligence Dashboards](https://www.wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/).

There are several ways we can manage dashboards:
1. CloudFormation Template (using cid-cmd tool in lambda) 
2. Using cid-cmd tool from command line

We recommend cid-cmd tool via [AWS CloudShell](https://console.aws.amazon.com/cloudshell/home).

## Supported dashboards
---
| Dashboard documentation | Demo URL | Prerequisites URL |
| --- | --- | --- |
| [CUDOS Dashboard](https://www.wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/2b_cudos_dashboard/) | [demo](https://d1s0yx3p3y3rah.cloudfront.net/anonymous-embed?dashboard=cudos) | [link](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/alternative_deployments/) |
| [Cost Intelligence Dashboard](https://www.wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/2a_cost_intelligence_dashboard/) | [demo](https://d1s0yx3p3y3rah.cloudfront.net/anonymous-embed?dashboard=cost_intelligence_dashboard) | [link](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/alternative_deployments/) |
| [Trusted Advisor Organisation (TAO) Dashboard](https://www.wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/trusted-advisor-dashboards/) | [demo](https://d1s0yx3p3y3rah.cloudfront.net/anonymous-embed?dashboard=e1799d0d-166c-4e61-8fa6-5c927f70c799) | [link](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/trusted-advisor-dashboards) |
| [Trends Dashboard](https://www.wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/3_additional_dashboards/#trends-dashboard) | [demo](https://d1s0yx3p3y3rah.cloudfront.net/anonymous-embed?dashboard=trends-dashboard) | [link](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards) |
| [KPI Dashboard](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/deploy_dashboards/) | [demo](https://d1s0yx3p3y3rah.cloudfront.net/anonymous-embed?dashboard=kpi) | [link](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/cost-usage-report-dashboards/dashboards/alternative_deployments/) |
| [Compute Optimizer Dashboard](https://www.wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/compute-optimizer-dashboards/) | [demo](https://d1s0yx3p3y3rah.cloudfront.net/anonymous-embed?dashboard=compute-optimizer-dashboard) | [link](https://wellarchitectedlabs.com/cost/200_labs/200_cloud_intelligence/compute-optimizer-dashboards) |


## Before you start
1. :heavy_exclamation_mark: Complete the prerequisites for respective dashboard (see above).
2. :heavy_exclamation_mark: [Specifying a Query Result Location Using a Workgroup](https://docs.aws.amazon.com/athena/latest/ug/querying.html#query-results-specify-location-workgroup)
3. :heavy_exclamation_mark: Make sure QuickSight [Enterprise edition](https://aws.amazon.com/premiumsupport/knowledge-center/quicksight-enterprise-account/) is activated.

## How to use for Dasbhoard Deployment

1. Launch [AWS CloudShell](https://console.aws.amazon.com/cloudshell/home) or your local shell

    Automation requires Python 3

2. Make sure you have latest pip package installed
    ```bash
    python3 -m ensurepip --upgrade
    ```

4. Install CID Python automation PyPI package
    ```bash
    pip3 install --upgrade cid-cmd
    ```

5. Deploy the Dashboards
    ```bash
    cid-cmd deploy
    ```
### Demo

   [![asciicast](https://asciinema.org/a/467770.svg)](https://asciinema.org/a/467770)

## Other Commands

#### Update existing Dashboards
Update only Dashboard
```bash
cid-cmd update
```
Update dashboard and all dependenies (Datasets and Athena View). WARNING: this will override any customization of SQL files and Datasets.
```bash
cid-cmd update --force --recursive 
```
#### Show Sashboard status 
```bash
cid-cmd status
```

####  Share QuickSight resources
```bash
cid-cmd share
```

#### Delete Dashboard and all dependencies unused by other
```bash
cid-cmd delete
```  

#### Export 
A command `export` takes as an input a QuickSight Analysis and generates all assets for a deployment of this Analysis as a Dashboard in another AWS Account. Commands generates a yaml file with a description of Dashboard and all required Datasets. Also this command generates a QuickSight Template in the current AWS Account that can be used for Dashboard deployment in other accoutns. The resource file can be used with all other `cid` commands in other accounts. Both accounts must have relevant Athena Views and Tables.  

Export in account A:  
```
cid-cmd export
```

Deployment in account B:  
```
cid-cmd deploy --resources ./mydashboard.yaml
```

#### See available commands and command line options
```
cid-cmd --help
```


## Troubleshooting 

If you experience unexpected behaviour of the cid-cmd script please run cid-cmd in debug mode 

```bash
cid-cmd -vv [command]
```
    
This will produce a log file in the same directory that were at the tile of launch of cid-cmd. 

:heavy_exclamation_mark:Inspect the produced debug log for any sensitive information and anonymise it.

We encourage you to open [new issue](https://github.com/aws-samples/aws-cudos-framework-deployment/issues/new) with description of the problem and attached debug log file.
