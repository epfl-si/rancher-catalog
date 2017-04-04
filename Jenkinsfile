#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import ch.epfl.idevelop.template_pipeline

def template_pipeline = new ch.epfl.idevelop.template_pipeline()

def tests(stackname) {
  mysql = docker.image('mysql:5.7')
  mysql.inside("echo 'CREATE TABLE foo (foo integer);' | mysql -h ${stackname}.db.test-rsaas.epfl.ch -ptest -u test test")
  mysql.inside("echo 'INSERT INTO foo (foo) VALUES (1), (2), (3), (4); SELECT * FROM foo;' | mysql -h ${stackname}.db.test-rsaas.epfl.ch -ptest -u test test")
}

def stack_env_55 = [
  'MYSQL_VERSION' : '5.5',
  'MYSQL_ROOT_PASSWORD': 'test',
  'MYSQL_DATABASE': 'test',
  'AMM_USERNAME': 'test',
  'AMM_USER_PASSWORD_HASH': '*94bdcebe19083ce2a1f959fd02f964c7af4cfc29',
  'MAX_CONNECTIONS' : '3',
  'QUOTA_SIZE_MIB': '500',
  'MYSQL_EXPORT_PORT' : 3300
]

def stack_env_56 = [
  'MYSQL_VERSION' : '5.6',
  'MYSQL_ROOT_PASSWORD': 'test',
  'MYSQL_DATABASE': 'test',
  'AMM_USERNAME': 'test',
  'AMM_USER_PASSWORD_HASH': '*94bdcebe19083ce2a1f959fd02f964c7af4cfc29',
  'MAX_CONNECTIONS' : '3',
  'QUOTA_SIZE_MIB': '500',
  'MYSQL_EXPORT_PORT' : 3300
]

def stack_env_57 = [
  'MYSQL_VERSION' : '5.7',
  'MYSQL_ROOT_PASSWORD': 'test',
  'MYSQL_DATABASE': 'test',
  'AMM_USERNAME': 'test',
  'AMM_USER_PASSWORD_HASH': '*94bdcebe19083ce2a1f959fd02f964c7af4cfc29',
  'MAX_CONNECTIONS' : '3',
  'QUOTA_SIZE_MIB': '500',
  'MYSQL_EXPORT_PORT' : 3300
]

//template_pipeline.process(
//    'mysql',
//    false,
//    this.&test,
//    'epfl-idevelop',
//    'amm-token',
//    'rancher-catalog',
//    'amm-ci@groupes.epfl.ch',
//    'https://test-rancher.epfl.ch',
//    'test-rancher-ci-cred-jenkins',
//    'DB',
//    stack_env_57,
//    this.&successhook
//)

def rancher_server_url = 'https://test-rancher.epfl.ch'
def rancher_server_credid = 'test-rancher-ci-cred-jenkins'
def rancher_environment = 'DB'
def projectname = 'mysql'
def isinfratemplate = false
def jenkins_email = 'amm-ci@groupes.epfl.ch'
def github_cred_id = 'amm-token'
def github_organization = 'epfl-idevelop'
def rancher_catalog_repo = 'rancher-catalog'

node('docker') {
  try {
    template_pipeline.preinit()
    rancher_env_id = template_pipeline.get_environment_id(rancher_server_url, rancher_server_credid, rancher_environment);
    lock("template-${projectname}-${env.BRANCH_NAME}") {
      template_pipeline.deploy_test_and_cleanup(rancher_server_url, rancher_server_credid, rancher_env_id, projectname, isinfratemplate, stack_env_55, this.&tests)
      template_pipeline.deploy_test_and_cleanup(rancher_server_url, rancher_server_credid, rancher_env_id, projectname, isinfratemplate, stack_env_56, this.&tests)
      template_pipeline.deploy_test_and_cleanup(rancher_server_url, rancher_server_credid, rancher_env_id, projectname, isinfratemplate, stack_env_57, this.&tests)
      template_pipeline.success_post_tests(projectname, jenkins_email, github_cred_id, github_organization, rancher_catalog_repo, isinfratemplate)
    }
    currentBuild.result = "SUCCESS"
  } catch (err) {
    throw err
    currentBuild.result = "FAILURE"
  } finally {
    template_pipeline.inconditional_post_tests()
  }
}
