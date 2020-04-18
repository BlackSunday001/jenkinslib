#!/groovy

@Library('jenkinslib')

def tools = new org.devops.tools()

String workspace = "/opt/jenkins/workspace"

//Pipeline
pipeline {
    agent {
        node {
            label "build01"
            customWorkspace "${workspace}"
        }
    }

    parameters {
        string(
            name: "DEPLOY_ENV",
            defaultValue: 'staging',
            description: ''
        )
    }

    options {
        timestamps()    //在输出日志中会增加时间
        skipDefaultCheckout()   //跳过默认检查代码库的checkout，
        disableConcurrentBuilds()   //禁止并行
        timeout(time: 1, unit: 'HOURS') //流水线超时设置 1 小时
    }

    stages {
        //下载代码
        stage('GetCode'){
            when {
                environment name: 'test',
                value: 'abcd'
            }
            steps{
                timeout(time: 5, unit: "MINUTES"){
                    script{
                        println('获取代码')
                        tools.PringMes('获取代码','gree')
                        input {
                            message "Should we continue?"
                            ok "Yes, we should."
                            submitter "tracy"
                            parameters {
                                string(
                                    name: "PERSON", 
                                    defaultValue: "Mr Jenkins", 
                                    descript: 'Who should I say hello to?'
                                )
                            }
                        }
                    }
                }
            }
        }

        //代码构建
        stage('Build'){
            steps{
                timeout(time: 20, unit: "MINUTES"){
                    script{
                        println('应用构建')
                        tools.PringMes('应用构建','gree')
                        mvnHome = tool "m2"
                        println(mvnHome)
                    }
                }
            }
        }

        //代码扫描
        stage('CodeScan'){
            steps{
                timeout(time: 30, unit: "MINUTES"){
                    script{
                        println('代码扫描')
                        tools.PringMes('代码扫描','gree')
                    }
                }
            }
        }
    }
    //构建后的操作
    post {
        always {
            script{
                println("always")
            }
        }

        success {
            script{
                currentBuild.description += "\n 构建成功"
            }
        }
        failure {
            script{
                currentBuild.description += "\n 构建失败"
            }
        }
        aborted {
            script{
                currentBuild.description += "\n 构建取消"
            }
        }
    }
}
