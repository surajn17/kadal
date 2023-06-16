pipeline {
  agent any

  stages {
    stage('Deploy Web Server') {
      steps {
        sh 'ssh ubuntu@54.250.115.66 sudo apt update'
        sh 'ssh ubuntu@54.250.115.66 sudo apt install -y apache2'
        sh 'ssh ubuntu@54.250.115.66 sudo systemctl start apache2'
        sh 'ssh ubuntu@54.250.115.66 sudo systemctl enable apache2'
      }
    }

    stage('Deploy WordPress') {
      steps {
        sh 'ssh ubuntu@54.250.115.66 sudo apt install -y php libapache2-mod-php php-mysql'
        sh 'ssh ubuntu@54.250.115.66 sudo apt install -y mysql-server'
        sh 'ssh ubuntu@54.250.115.66 sudo mysql_secure_installation'
        sh 'ssh ubuntu@54.250.115.66 sudo mysql -e "CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;"'
        sh 'ssh ubuntu@54.250.115.66 sudo mysql -e "CREATE USER \'wordpressuser\'@\'localhost\' IDENTIFIED BY \'password\';"'
        sh 'ssh ubuntu@54.250.115.66 sudo mysql -e "GRANT ALL ON wordpress.* TO \'wordpressuser\'@\'localhost\';"'
        sh 'ssh ubuntu@54.250.115.66 sudo mysql -e "FLUSH PRIVILEGES;"'
        sh 'ssh ubuntu@54.250.115.66 sudo docker run -d --name wordpress -p 80:80 -e WORDPRESS_DB_HOST=localhost -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wordpressuser -e WORDPRESS_DB_PASSWORD=password wordpress'
      }
    }
  }
}
