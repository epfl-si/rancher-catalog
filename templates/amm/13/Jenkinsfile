#!/usr/bin/groovy

// Load shared library
@Library('epflidevelop') import ch.epfl.idevelop.template_pipeline

pipeline = new ch.epfl.idevelop.template_pipeline()

def tests(stackname) {
}

def successhook() {
  if (env.BRANCH_NAME == 'latest') {
    def rancher_compose = readFile('./rancher-compose.yml')
    def docker_compose = readFile('./docker-compose.yml')
    def version = pipeline.get_template_version()
    def envvars = pipeline.get_stack_environment(rancher_server_url, rancher_server_credid, rancher_environment, 'amm')

    pipeline.upgrade_stack(rancher_server_url, rancher_server_credid, rancher_environment, 'amm', docker_compose, rancher_compose, envvars, "catalog://idevelop:amm:${version}")
  }
}

def rancher_server_url = 'https://test-rancher.epfl.ch'
def rancher_server_credid = 'test-rancher-ci-cred-jenkins'
def rancher_environment = 'DB'
def projectname = 'amm'
def isinfratemplate = false
def jenkins_email = 'amm-ci@groupes.epfl.ch'
def github_cred_id = 'amm-token'
def github_organization = 'epfl-idevelop'
def rancher_catalog_repo = 'rancher-catalog'

withCredentials(
    [[$class: 'UsernamePasswordMultiBinding',
    credentialsId: 'amm-test-rancher-creds',
    usernameVariable: 'ACCESS_KEY',
    passwordVariable: 'SECRET_KEY']]
  ) {

  def stack_env = [
    'SECRET_KEY' : 'ksjdlkdshlglsjdlksdlklkg',
    'LDAP_USER_BASE_DN': 'ou=users,o=epfl,c=ch',
    'LDAP_USER_SEARCH_ATTR': 'uid',
    'LDAP_SERVER': 'scoldap.epfl.ch',
    'CACHE_REDIS_LOCATION': 'redis_master/sentinel.redis-sentinel.rancher.internal:6379/1',
    'CACHE_REDIS_CLIENT_CLASS': 'django_redis_sentinel.SentinelClient',
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

  pipeline.process(
    projectname,
    isinfratemplate,
    this.&tests,
    github_organization,
    github_cred_id,
    rancher_catalog_repo,
    jenkins_email,
    rancher_server_url,
    rancher_server_credid,
    rancher_environment,
    stack_env,
    this.&successhook
  )

}

