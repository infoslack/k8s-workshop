node {
  def project = 'infoslack-1322'
  def appName = 'k8s-workshop'
  def imageTag = 'gcr.io/${project}/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}'

  checkout scm

  stage 'Build docker image'
  sh("docker build -t ${imageTag} .")

  stage 'Push to registry'
  sh("gcloud docker -- push ${imageTag}")
}
