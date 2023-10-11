pipeline {
  agent any
  environment {
   CLIENT = 'edcd9ff6-fa78-48b6-ab0b-5f02c2145fc5'
    TENANT = 'bd177737-dc9f-49d5-89fa-af1c0232bfc9'
    SECRET = '_ZX8Q~YOFThPgRoHxaqUl3a-Hp-xm1~zznbSgcg4'
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
          sh 'az login --service-principal -u $CLIENT -p $SECRET -t $TENANT '
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
