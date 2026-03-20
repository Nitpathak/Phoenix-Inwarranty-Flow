# Phoenix In-Warranty Flow — Postman Automation Framework with Github Actions #

## Overview ##

This repository is demonstration for POC for integration postman tests with github actions. The tests are written in Postman and they are on the VM with the help of newman and newman-reporter-htmlextra. Github Actions will trigger the Project execution on every push to main branch. You can also execute the project anually using workflow_dispatch. The projects on a scheduled time with the help of the crone job.

The HTML reports is archieved and kept in the artifacts section for the team to download it. Along with that they can view the report directly from the github page: https://github.com/Nitpathak/Phoenix-Inwarranty-Flow. The latest reports is mailed to the team members using GMAIL SMTP.


## Tech Stack ##

1. Postman: Where the API tests are written
2. Node.js v22: The engine that powers Newman under the hood
3. Newman: Runs those Postman tests from the command line (no UI needed)
4. Newman-reporter-htmlextra: Turns raw test results into a beautiful, readable HTML report
5. Github Actions: The automation engine — watches for code changes and kicks everything off
6. Gmail SMTP: Sends the report to the team by email after every run
7. Github Pages: Hosts the latest report online so anyone can view it via a link
8. CSV for the data driven testing: Lets the tests run with multiple sets of data automatically
9. AWS-EC2 instance for Self hosted github runner: A cloud server that runs the tests (self-hosted, always available)

## Architecture ##

```
Push to main / Cron / workflow_dispatch
            │
            ▼
    GitHub Actions Workflow
            │
            ▼
   Newman runs on AWS EC2 Runner
            │
     ┌──────┴──────┐
     ▼             ▼
HTML Report     CLI Output
     │
  ┌──┴───────────────────┐
  ▼                       ▼
GitHub Pages          GitHub Artifacts
  (live view)           (downloadable)
     │
     ▼
Gmail SMTP Notification → Team Members

```

## Github Pages ##
You can directly view the latest test reports of the Postman Test at the Github Page link: https://nitpathak.github.io/Phoenix-Inwarranty-Flow/

## How to run the projects ##
You can run the Projects on your local system for that: 
1. Clone the project on the local system: ``` git@github.com:Nitpathak/Phoenix-Inwarranty-Flow.git ```
2. Install Nodejs and NPM from https: ``` https://nodejs.org/en ```
3. Install Newman using ``` npm install -g newman ```
4. Install Newman-reporter-htmlextra: ``` npm install -g newman-reporter-htmlextra ```
5. Run the newman commands:
  ```
     Run the Postman Collection with newman
        run: |
          newman run Inwarranty-flow-Collection.postman_collection.json \
          -e QA.postman_environment.json \
          -r cli,htmlextra \
          --reporter-htmlextra-export ./newman/index.html
```

## HTML Reports ##
The Reports will be craeted in the newman folder

![Postman_Reports](https://github.com/Nitpathak/Phoenix-Inwarranty-Flow/blob/static-content/Newman-report.png)

## Testing Coverage ##
1. Happy Flow Testing
2. Negative Testing and Edge case Testing
3. Token Testing
4. Data Driven Testing with CSV
5. Schema Validation
6. Secrets Managments with Github Actions

## Project Structure ##

```
Phoenix-Inwarranty-Flow/
├── .github/
│   └── workflows/
│       └── newman-tests.yml        # GitHub Actions workflow definition
├── newman/
│   └── index.html                  # Generated HTML report (post-run)
├── Inwarranty-flow-Collection.postman_collection.json   # Postman collection
├── QA.postman_environment.json     # QA environment variables
├── data.csv                        # CSV file for data-driven testing
└── README.md

```

Maintained by: @Nitpathak
