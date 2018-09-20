node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Build Docker test'){
      sh 'docker build -t react-test2 -f Dockerfile.test --no-cache . '
    }
    stage('Docker test'){
      sh 'docker run --rm react-test2'
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test2'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app2 --no-cache .'
        sh 'docker tag react-app2 localhost:5000/react-app2'
        sh 'docker push localhost:5000/react-app2'
        sh 'docker rmi -f react-app2 localhost:5000/react-app2'
      }
    }
  }
  catch (err) {
    throw err
  }
}
