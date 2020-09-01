#!/usr/bin/env groovy

pipeline {

    agent{
        label 'TAM001'
    }

    //オプション
    options {
        //同時ビルド無効
        disableConcurrentBuilds()
    }

    stages{
        //チェックアウト
        stage('Checkout'){
            steps{
                script{
                    //クリーン
                    cleanWs()
                    //チェックアウト
                    checkout scm
                }
            }
        }

        //ビルド
        stage('Build'){
            steps{
                script{
                    sh "ant"
                }
            }
        }

        //テスト結果
        stage('Report'){
            steps{
                script{
                    junit 'build/test-report/*.xml'
                }
            }
        }
    }

    post{
        always{
            //成果物保存
            archiveArtifacts artifacts: "**/build/*.jar" , fingerprint: true
        }
        failure{
            echo "エラー"
        }
        success{
            echo "正常"
        }
        unstable{
            echo "不安定"
        }
    }
}
