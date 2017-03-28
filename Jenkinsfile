#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import static ch.epfl.idevelop.utils.*

dockerBuild {
    checkout scm
    stage '\u2776 Example Stage 1'
    echo "\u2600 BUILD_URL=${env.BUILD_URL}"
    def workspace = pwd()
    echo "\u2600 workspace=${workspace}"

    stage '\u2777 Print all environment variables'
    sh 'env > env.txt'
    for (String i : readFile('env.txt').split("\r?\n")) {
        println i
    }
}

