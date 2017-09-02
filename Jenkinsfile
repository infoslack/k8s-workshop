node {
  def project = 'infoslack-1322'
  def appName = 'k8s-workshop'
  def imageTag = 'gcr.io/${project}/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}'

  checkout scm

  stage 'Build docker image'
  sh("docker build -t ${imageTag} .")

  stage 'Push to registry'
  sh("gcloud docker -- push ${imageTag}")

  stage 'Deploy'
  switch (env.BRANCH_NAME) {

    case "staging":
        sh("sed -i.bak 's#CHANGE-HERE#${imageTag}' ./kubernetes/k8s-app.yaml")
        sh("kubectl --namespace=staging apply -f kubernetes/k8s-app.yaml")
        break

    case "master":
        sh("sed -i.bak 's#CHANGE-HERE#${imageTag}' ./kubernetes/k8s-app.yaml")
        sh("kubectl --namespace=production apply -f kubernetes/k8s-app.yaml")
        break
  }
}
