node {
  stage('Build and deploy on develop') {
    openshiftBuild bldCfg: 'python-app',
      namespace: 'ingresos-develop',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'python-app',
      namespace: 'ingresos-develop'
  }
  stage('Validate for testing') {
    input message: 'Should be released to test envirenment?',
      id: 'approval'
  }
  stage('Deploy on test') {
    openshiftTag srcStream: 'python-app',
      namespace: 'ingresos-develop',
      srcTag: 'latest',
      destinationNamespace: 'ingresos-test',
      destStream: 'python-app',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'python-app',
      namespace: 'ingresos-test'
  }
  stage('Validate for production') {
    input message: 'Should be released to production envirenment?',
      id: 'approval'
  }
  stage('Desplegar en Produccion') {
    openshiftTag srcStream: 'python-app',
      namespace: 'ingresos-develop',
      srcTag: 'latest',
      destinationNamespace: 'ingresos-production',
      destStream: 'python-app',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'python-app',
      namespace: 'ingresos-production'
  }
}
