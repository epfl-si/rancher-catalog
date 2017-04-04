#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import ch.epfl.idevelop.template_pipeline

def template_pipeline = new ch.epfl.idevelop.template_pipeline()

def test(afterfailover) {
}

def stack_env = [
  'MYSQL_VERSION' : '5.5',
  'MYSQL_ROOT_PASSWORD': 'test',
  'MYSQL_DATABASE': 'test',
  'AMM_USERNAME': 'test',
  'AMM_USER_PASSWORD_HASH': '*94bdcebe19083ce2a1f959fd02f964c7af4cfc29',
  'MAX_CONNECTIONS' : '3',
  'QUOTA_SIZE_MIB': '500',
  'MYSQL_EXPORT_PORT' : 3300
]

template_pipeline.process(
    'mysql',
    false,
    false,
    this.&test,
    'epfl-idevelop',
    'amm-token',
    'rancher-catalog',
    'amm-ci@groupes.epfl.ch',
    'https://test-rancher.epfl.ch',
    'test-rancher-ci-cred-jenkins',
    'DB',
    stack_env
)
