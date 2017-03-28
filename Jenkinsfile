#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import static ch.epfl.idevelop.utils.*


//package ch.epfl.idevelop
def utils = new ch.epfl.idevelop.utils()


def projectname = 'mysql'
def templatename = 'mysql'
def image_prefix = 'dabelenda'
def dependencies(foo) {
  return []
}
def unittest() {
}
def buildcoveragexml() {
  return null
}
def acceptancetests(container) {
}
def versionmaj = '1'
def versionmin = '2'
def custombuild = null
def container_run_args = []
def github_cred_id = 'foo'
def github_organization = 'bar'

//def call(projectname, templatename, image_prefix, dependencies, unittest, buildcoveragexml, acceptancetests, versionmaj, versionmin, custombuild, container_run_args, github_cred_id, github_organization) {
node('docker') {
  try {
    stage("Checkout project git repo") {
      checkout scm
    }
    stage("Run unit tests") {
      unittest()
    }
    coveragefile = buildcoveragexml()
    if (coveragefile) {
      // TODO publish coverage
    }

    tag = env.BRANCH_NAME
    if (tag == 'master') {
      tag = 'latest'
    }
    def image = null
    def container = null
    
    lock("container-${projectname}-${tag}") {
      stage("build image ${image_prefix}/${projectname}:${tag}") {
        if (custombuild) {
          image = custombuild("${image_prefix}/${projectname}:${tag}")
        } else {
          image = docker.build("${image_prefix}/${projectname}:${tag}")
        }
      }

      stage("deploy image to local docker-engine") {
        def extra_args = dependencies(true)
        container = image.run() // extra_args + container_run_args)
      }

      stage("run acceptance tests") {
        acceptancetests(container)
        container.stop
      }

      stage("push image with tag ${tag}") {
        image.push(tag)
      }

      if (tag == 'latest') {
        buildnumber = manager.build.getEnvironment(manager.listener)['BUILD_NUMBER']
        stage "tag git repo with ${versionmaj}.${versionmin}.${buildnumber}" {
          sh "git tag ${versionmaj}.${versionmin}.${buildnumber}"
          sh "git push --tags"
        }

        lock("template-${templatename}") {
          stage("push docker image with tags") {
            image.push("${versionmaj}")
            image.push("${versionmaj}.${versionmin}")
            image.push("${versionmaj}.${versionmin}.${buildnumber}")
          }

          stage("checkout rancher-template-${templatename}") {
            multiscm {
              git {
                remote {
                  github("${github_organization}/rancher-template-${templatename}")
                  credentials(github_cred_id)
                  branch('test')
                }
                extensions {
                  relativeTargetDirectory('template')
                }
              }
            }
            sh "cd template; git pull --rebase origin master"
          }

          stage("modify template for image update") {
            // TODO modify template
          }

          stage("push template modifications") {
            // TODO commit changes to template
            // TODO push git repo
          }
        }
      }
    }

    currentBuild.result = "SUCCESS" 
  } catch (err) {
    println err
    currentBuild.result = "FAILURE" 
  } finally {
    try {
      // cleanup
      dependencies(false)
    } catch (err) {
      // do nothing
    }
    stage("Notifications") {
      utils.notifyBuild(currentBuild)
    }
  }
//}
}
