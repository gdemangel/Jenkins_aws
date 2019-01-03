// comment 

pipeline  {

	agent any

	stages {

		   stage('Checkout repositorio git') {

		   	steps {

		   	  git poll: true, url:'https://github.com/gdemangel/Jenkins_aws.git'
		   	
		   	}

		   }

		   stage('Crear ambiente virtual ') {

		   	   steps { 

		   		   sh '''

		   			   bash -c "virtualenv entorno_virtual && source entorno_virtual/bin/activate"

		   		   '''

		   	   }

		   }

		   stage('Instalar requerimientos') {
               
               steps {

               	   sh '''

               	   			bash -c "entorno_virtual/bin/pip install -r requirements.txt"               	   			

               	   '''

               }

		   } 

		   stage('Testear app') {


		   	   steps {

		   	   		sh '''

		   	   				bash -c "entorno_virtual/bin/pytest"		   	   		

		   	   		'''

		   	   }

		   } 

		   stage('Correr aplicacion') {

		   	   steps {

		   	   		sh '''

		   	   				 bash -c "entorno_virtual/bin/python src/main.py &"

		   	   		'''
		   
		   	   }
		   
		   }

		   stage('Build Docker Img') {

		   	   steps {

		   	   	   sh ''' 

		   	   	   			docker build -t apptest:latest .

		   	   	   '''

		   	   }

		   }

		   stage('Push Docker Img') {

		   	   steps {

		   	   	   sh ''' 
		   	   	   			
							docker tag apptest:latest gdemangel/apptest:latest
											docker push gdemangel/apptest:latest
											docker rmi apptest:latest
	
		   	   	   '''

		   	   }

		   } 

	}

}



