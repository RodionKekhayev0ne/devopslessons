pipeline {
    agent any

    environment {
        // Путь к виртуальному окружению
        VENV_DIR = "venv"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Клонирование репозитория
                git branch: 'main', url: 'https://github.com/RodionKekhayev0ne/devopslessons.git'
                echo 'git cloned !!!'
            }
        }

        stage('Setup Python Environment') {
            steps {
                // Установка виртуального окружения и активация
                sh 'python3 -m venv $VENV_DIR'
                sh '. $VENV_DIR/bin/activate'
                echo 'env acvate !!!'
            }
        }

        // stage('Install Dependencies') {
        //     steps {
        //         // Установка зависимостей проекта
        //         sh '$VENV_DIR/bin/pip install -r requirements.txt'
        //     }
        // }

        stage('Run Migrations') {
            steps {
                // Применение миграций
                sh '$VENV_DIR/bin/python manage.py migrate'
            }
        }

        stage('Run Tests') {
            steps {
                // Запуск тестов
                sh '$VENV_DIR/bin/python manage.py test'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                
                sh '$VENV_DIR/bin/python manage.py runserver'
            }
        }
    }

    post {
        always {
            // Очистка виртуального окружения после завершения сборки
            cleanWs()
        }
    }
}
