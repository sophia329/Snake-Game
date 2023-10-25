node('appserver-cweb')
{
  def app

  stage('Cloning Git')
  {
    /*Let's make sure we have the repository cloned to out workspace*/
    checkout scm
  }

  stage('Build-and-Tag')
  {
    /*This builds the actual image; same as docker build on cmd*/
    app =docker.build("sophia329/snake-game")
  }

  stage('Post-to-dockerhub')
  {
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    {
      app.push("latest")
    }
  }

  stage('Pull-image-server')
  {
    sh "docker-compose down"
    sh "docker-compose up -d"
  }
  
}
