pipeline {
    agent any

    parameters {
        booleanParam(name: 'IaC', defaultValue: false, description: 'Is the Infrastracture already deployed, if not check this.')
        choice(
            name: 'scanMode',
            choices: ['dev', 'prod_no_security', 'prod'],
            description: 'Select the Scan mode: <dev> : Will run checks without interrupting the pipeline, useful in development. <prod_no_security> : Will skip security checks in production.     <prod> : Will run full checks and stop in case of severe vulnerabilities (HIGH, CRITICAL) '
        )
    }

    stages {
        stage('Deploy IaC') {
            when {
                equals expected: true, actual: params.IaC
            }
            steps {

                build job: 'rome_aks', wait: false, parameters: [
                    string(name: 'scanMode', value: params.scanMode)
                ]
            }
        }


        stage('Deploy Gateway') {
            steps {

                build job: 'rome_gateway', wait: false, parameters: [
                    string(name: 'scanMode', value: params.scanMode)
                ]
            }
        }

        stage('Deploy User') {
            steps {

                build job: 'rome_user', wait: false, parameters: [
                    string(name: 'scanMode', value: params.scanMode)
                ]
            }
        }

        stage('Deploy Certificate') {
            steps {

                build job: 'rome_certificate', wait: false, parameters: [
                    string(name: 'scanMode', value: params.scanMode)
                ]
            }
        }

        stage('Deploy Frontend') {
            steps {

                build job: 'rome_frontend', wait: false, parameters: [
                    string(name: 'scanMode', value: params.scanMode)
                ]
            }
        }
    }
}