pipeline {
  agent any

  stages {
    stage('Deploy Web Server') {
      steps {
        sh 'sudo apt  install -y apache2'
        sh 'sudo systemctl start apache2'
        sh 'sudo systemctl enable apache2'
      }
    }

    stage('Deploy WordPress') {
      steps {
        sh 'sudo apt install -y php libapache2-mod-php php-mysql'
        sh 'sudo apt install -y mysql-server'
        sh 'sudo mysql_secure_installation'
        sh 'sudo mysql -e "CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;"'
        sh 'sudo mysql -e "CREATE USER \'wordpressuser\'@\'localhost\' IDENTIFIED BY \'password\';"'
        sh 'sudo mysql -e "GRANT ALL ON wordpress.* TO \'wordpressuser\'@\'localhost\';"'
        sh 'sudo mysql -e "FLUSH PRIVILEGES;"'
        sh 'sudo docker run -d --name wordpress -p 80:80 -e WORDPRESS_DB_HOST=localhost -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wordpressuser -e WORDPRESS_DB_PASSWORD=password wordpress'
      }
    }
  }
}
