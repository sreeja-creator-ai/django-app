pipeline {
  agent any

  stages {
    stage('Clone Repository') {
      steps {
        git 'https://github.com/sreeja-creator-ai/django-app.git'
      }
    }

    stage('Build & Deploy Containers') {
      steps {
        bat 'docker-compose down || true'
        bat 'docker-compose build'
        bat 'docker-compose up -d'
      }
    }

    stage('Run Migrations & Collect Static') {
      steps {
        bat 'docker-compose run web python manage.py migrate'
        bat 'docker-compose run web sh -c "python manage.py migrate && python manage.py collectstatic --noinput"'
      }
    }
  }

  post {
    always {
      echo 'Pipeline execution completed.'
    }
  }
}
