#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import ch.epfl.idevelop.template_pipeline

def template_pipeline = new ch.epfl.idevelop.template_pipeline()

def tests(stackname) {
}

def successhook() {
}

def rancher_server_url = 'https://test-rancher.epfl.ch'
def rancher_server_credid = 'amm-test-rancher-creds'
def rancher_environment = 'DB'
def projectname = 'amm'
def isinfratemplate = false
def jenkins_email = 'amm-ci@groupes.epfl.ch'
def github_cred_id = 'amm-token'
def github_organization = 'epfl-idevelop'
def rancher_catalog_repo = 'rancher-catalog'

withCredentials(
    [[$class: 'UsernamePasswordMultiBinding',
    credentialsId: rancher_server_credid,
    usernameVariable: 'ACCESS_KEY',
    passwordVariable: 'SECRET_KEY']]
  ) {

  def stack_env = [
    'SECRET_KEY' : 'ksjdlkdshlglsjdlksdlklkg',
    'LDAP_USER_BASE_DN': 'ou=users,o=epfl,c=ch',
    'LDAP_USER_SEARCH_ATTR': 'uid',
    'LDAP_SERVER': 'scoldap.epfl.ch',
    'REDIS_SERVICE': 'redis-sentinel/redis',
    'CACHE_REDIS_LOCATION': 'redis://redis:6379/1',
    'CACHE_REDIS_CLIENT_CLASS': 'django_redis.client.DefaultClient',
    'AMM_CERTIFICATE': 'test',
    'SERVICE_FQDN': 'amm.db.test-rsaas.epfl.ch',
    'DJANGO_WORKER_COUNT': '2',
    'LDAP_SERVER_FOR_SEARCH': 'ldap.epfl.ch',
    'LDAP_USE_SSL': 'true',
    'AMM_ENVIRONMENT': '1a7',
    'RANCHER_API_URL': 'https://rancher.epfl.ch/',
    'RANCHER_VERIFY_CERTIFICATE': 'true',
    'RANCHER_ACCESS_KEY': ACCESS_KEY,
    'RANCHER_SECRET_KEY': SECRET_KEY,
    'DJANGO_SETTINGS_MODULE': 'config.settings.prod',
  ]

  template_pipeline.process(
    projectname,
    isinfratemplate,
    tests,
    github_organization,
    github_cred_id,
    rancher_catalog_repo,
    jenkins_email,
    rancher_server_url,
    rancher_server_credid,
    rancher_environment,
    stack_env,
    successhook
  )

}

