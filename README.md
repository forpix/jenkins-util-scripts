# jenkins-util-scripts

A collection of scripts, custom steps that can be used in a Jenkins pipeline

Some of the API's provided:

* Add/Remove environment variabels to a node
* Delete jobs based on a condition
* Fetch plotting data form the current job
* Run a script on multiple slaves
* Extract details about test results (junit)
* Get a list of the failed stages
* ...

## Installation

Add this repository as a [shared library](https://jenkins.io/doc/book/pipeline/shared-libraries/) in your jenkins instance

## Usage

See the [example](https://github.com/roel0/jenkins-util-scripts/blob/master/example/Jenkinsfile) for more information.

### Get_failed_stages

It is possible to get a list of the failed stages. However this is only possible when the stages use the super_stage wrapper instead of directly using the stage API by jenkins.

```groovy
try {
    super_stage("stage1") {
    }
    super_stage("stage2") {
        error "oei"
    }
} catch(e) {
}

println "Failed stages: ${get_failed_stages().join(',')}"
```
This will print out => Failed stages: stage2
