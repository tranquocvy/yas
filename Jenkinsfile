pipeline {
    agent any

    stages {
        stage('CI for YAS Microservices') {
            parallel {
                // Ví dụ cho service 'media' nằm ngay ở root
                stage('Media Service CI') {
                    when {
                        // Chỉ chạy nếu có thay đổi trong thư mục 'media'
                        changeset "media/**"
                    }
                    stages {
                        // Phase 1: TEST
                        stage('Test') {
                            steps {
                                dir('media') {
                                    // Chạy test và sinh báo cáo JaCoCo
                                    sh 'mvn clean test'
                                }
                            }
                            post {
                                always {
                                    dir('media') {
                                        // Upload kết quả Test (Pass/Fail)
                                        junit 'target/surefire-reports/*.xml'
                                        // Upload Độ phủ (Coverage) - JaCoCo plugin sẽ đọc file này
                                        jacoco execPattern: 'target/jacoco.exec'
                                    }
                                }
                            }
                        }
                        // Phase 2: BUILD
                        stage('Build') {
                            steps {
                                dir('media') {
                                    // Đóng gói thành file .jar
                                    sh 'mvn package -DskipTests'
                                }
                            }
                        }
                    }
                }

                // Copy stage cho các service khác như 'product', 'cart' tương tự...
                stage('Product Service CI') {
                    when { changeset "product/**" }
                    stages {
                        stage('Test') {
                            steps {
                                dir('product') { sh 'mvn clean test' }
                            }
                            post {
                                always {
                                    dir('product') {
                                        junit 'target/surefire-reports/*.xml'
                                        jacoco execPattern: 'target/jacoco.exec'
                                    }
                                }
                            }
                        }
                        stage('Build') {
                            steps {
                                dir('product') { sh 'mvn package -DskipTests' }
                            }
                        }
                    }
                }
            }
        }
    }
}