
pipeline {
  agent any
  environment {
    ID     = credentials('id')
    CLIENT = credentials('client')
    TID     = credentials('tid')
  }

  stages {
    stage('Clonar repositorio') {
      steps {
          git url: 'https://github.com/Nca46/iac_test.git' 
          echo "Descargando repositorio"
      }
    }

    stage('Autenticacion de azure'){
      steps {
          sh 'az login --service-principal -u $ID -p $CLIENT -t TID '
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