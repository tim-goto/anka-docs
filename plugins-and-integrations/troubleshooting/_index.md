---
title: "Troubleshooting (Plugins and Integrations)"
linkTitle: "Troubleshooting"
weight: 99
hideSubPagesInLeftMenu: true
showBaseDirName: true
---
{{< hint error >}}
EOL and Deprecation list:
- Jenkins Plugin versions < 2.0 EOL
- Anka GitLab Runner versions < 1.0 EOL
{{< /hint >}}

**Please perform the checklist steps below before reaching out to customer support.**

---

### Troubleshooting Checklists

These checklists give you an idea where to look and what logs to check for indications of exactly what's wrong when you see failures.

#### Gitlab Runner

Our gitlab runner is based on the core and official gitlab runner release, so the [official troubleshooting guide](https://docs.gitlab.com/runner/faq/) is also good to review.

1. Find the job's console log inside of your Gitlab instance and gather the VM and node information from it.
1. If you have access to the gitlab-runner logs, collect those for the time period of the failure. Logs in the runner are labelled with `job=#`, matching the job ID.
1. Collect the logs in the Anka Build Cloud Controller from the time period of the failure (`Controller > Logs > Service: Controller`)
1. [Perform the Anka Virtualization checklist and check the logs at the time of the error on the Anka Node that ran the VM.]({{< relref "anka-virtualization-cli/troubleshooting/_index.md#anka-virtualization" >}})

#### Jenkins

1. When you first kick off a job in Jenkins, you can find the "node" or "computer" Jenkins ties the VM our plugin spins up to at the top of the Console Output. If you go to the node's page, you'll be able to access the "Logs" which show you Jenkins connecting to the Anka VM and any potential failures there. This is useful to check first, but the log is only available until the VM is terminated and Jenkins deletes the node.
1. Gain a understanding of what specifically is failing from the Console Output in the Jenkins job.
1. Collect the logs for the Anka Build Cloud Controller from the time period of the failure (`Controller > Logs > Service: Controller`).
1. Find the Jenkins System Log and look at the time of the failure for any errors related to the Anka plugin or Jenkins in general.
1. [Perform the Anka Virtualization checklist and check the logs at the time of the error on the Anka Node that ran the VM.]({{< relref "anka-virtualization-cli/troubleshooting/_index.md#anka-virtualization" >}})

#### Buildkite

1. Gain an understanding of what specifically is failing from the specific build log at buildkite.com.
1. Ensure the buildkite agent is configured correctly, registered and showing up properly on your buildkite organization agents page, and has an active status.
1. [Perform the Anka Virtualization checklist and check the logs at the time of the error on the Anka Node that ran the VM.]({{< relref "anka-virtualization-cli/troubleshooting/_index.md#anka-virtualization" >}})

#### Github Actions

1. Gain an understanding of what specifically is failing from the actions run log.
1. Follow [official troubleshooting guide from Github.](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/about-monitoring-and-troubleshooting#troubleshooting-your-workflows)
1. [Perform the Anka Virtualization checklist and check the logs at the time of the error on the Anka Node that ran the VM.]({{< relref "anka-virtualization-cli/troubleshooting/_index.md#anka-virtualization" >}})

#### Azure Devops Pipelines

1. Gain an understanding of what specifically is failing from the pipeline logs.
1. Follow [official troubleshooting guide from Microsoft.](https://docs.microsoft.com/en-us/azure/devops/pipelines/troubleshooting/troubleshooting?view=azure-devops)
1. [Perform the Anka Virtualization checklist and check the logs at the time of the error on the Anka Node that ran the VM.]({{< relref "anka-virtualization-cli/troubleshooting/_index.md#anka-virtualization" >}})

#### Anka Packer Plugin

1. Run your `packer build` with debug logging enabled: `export ANKA_LOG_LEVEL=debug; export ANKA_DELETE_LOGS=0; PACKER_LOG=1 packer build. . .`
2. Looks at the various anka commands in the logs to determine the exact one failing (if an anka command at all).

---

## Troubleshooting Guides
