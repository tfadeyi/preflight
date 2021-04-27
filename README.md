# Jetstack Secure Agent

[![release-master](https://github.com/jetstack/preflight/actions/workflows/release-master.yml/badge.svg)](https://github.com/jetstack/preflight/actions/workflows/release-master.yml)
[![Go Reference](https://pkg.go.dev/badge/github.com/jetstack/preflight.svg)](https://pkg.go.dev/github.com/jetstack/preflight)
[![Go Report Card](https://goreportcard.com/badge/github.com/jetstack/preflight)](https://goreportcard.com/report/github.com/jetstack/preflight)


The Jetstack Secure Agent is a tool to automatically perform Kubernetes cluster configuration
checks using [Open Policy Agent (OPA)](https://www.openpolicyagent.org/).

This repository hosts the agent part of Jetstack Secure. It sends data to the [Jetstack Secure SaaS](https://platform.jetstack.io) platform.

<!-- markdown-toc start - Don't edit this section. Run M-x
markdown-toc-refresh-toc -->

**Table of Contents**

* [Jetstack Secure Agent](#jetstack-secure-agent)
   * [Project Background](#project-background)
   * [Agent](#agent)
   * [Packages](#packages)
   * [Installation](#installation)

<!-- markdown-toc end -->

## Project Background

Jetstack Secure was originally designed to automate Jetstack's production readiness
assessments.
These are consulting sessions in which a Jetstack engineer inspects a customer's
cluster to suggest improvements and identify configuration issues.
The product of this assessment is a report
which describes any problems and offers remediation advice.

While these assessments have provided a lot of value to many customers, with a
complex system like Kubernetes it's hard to thoroughly check everything.
Automating the checks allows them to be more comprehensive and much faster.

The automation also allows the checks to be run repeatedly, meaning they can be
deployed in-cluster to provide continuous configuration checking. This enables
new interesting use cases as policy compliance audits.

## Agent

The Jetstack Secure _agent_ uses _data gatherers_ to collect required data from
Kubernetes and cloud provider APIs before formatting it as JSON for analysis.
Once data has been collected, it is sent to the configured backend.

To run the Agent locally you can run:

```bash
preflight agent --agent-config-file ./path/to/agent/config/file.yaml
```

Or, to build and run a version from master:

```bash
go run main.go agent --agent-config-file ./path/to/agent/config/file.yaml
```

You can find the example agent file
[here](https://github.com/jetstack/preflight/blob/master/agent.yaml).

You might also want to run a local echo server to monitor requests the agent
sends:

```bash
go run main.go echo
```

## Packages

Policies for cluster configuration are encoded into *Jetsack Secure packages*.  Each
package focuses on a different infrastructure component, for example the `gke`
package provides rules for the configuration of a GKE cluster.

Jetstack Secure packages are implemented using
[Open Policy Agent](https://www.openpolicyagent.org) with evaluation
taking place in the SaaS backend.

## Installation

Please follow the instructions at
[platform.jetstack.io](https://platform.jetstack.io) for the latest
installation instructions.
