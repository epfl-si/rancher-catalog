#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import ch.epfl.idevelop.template_pipeline

def template_pipeline = new ch.epfl.idevelop.template_pipeline()

def test(afterfailover) {
}

def stack_env = null

template_pipeline.process(
    'mysql',
    false,
    false,
    this.&test,
    'epfl-idevelop',
    'amm-token',
    'rancher-catalog',
    'amm-ci@groupes.epfl.ch',
    'https://rancher.epfl.ch',
    'test-rancher-ci-cred-jenkins',
    'CI',
    stack_env
)
