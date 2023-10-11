pipeline {
  agent any
  environment {
   CLIENT = credentials('CLIENT')
    TENANT = credentials('TENANT')
    SECRET = credentials('SECRET')
  }

  stages {
    stage('Clonar repositorio') {
      steps {
          git url: 'https://github.com/iqtumg/iac_test.git' 
          echo "Descargando repositorio"
      }
    }

    stage('Autenticacion de azure'){
      steps {
          sh 'az login --service-principal -u $CLIENT -p $TENANT -t $SECRET '
            echo "Autenticado a azure con éxito"
        
      }
    }
    
      stage('Desplegar infraestructura'){
      steps{
         sh('terraform init')
            echo "Terraform init finalizado"
            sh('terraform plan')
            echo "Terraform plan finalizada"
        
          echo('Infraestructura desplegada')
          sh('terraform apply -auto-approve')
          echo('La infreastructura se desplegó con éxito!')
        
      }
    }
      stage('Destruir infraestrucutra'){
      steps {
        sh('terraform destroy -auto-approve')
        echo "Infraestructura destruida"
        
      }
    }
  }
}
