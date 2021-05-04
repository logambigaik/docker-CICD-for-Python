# Docker-CICD-for-Python

## Link for reference : https://docs.docker.com/language/python/develop/
# Build the Image

    # For SImple Application:

    >> requirements.txt
    
        $ cd /path/to/python-docker
        $ pip3 install Flask
        $ pip3 freeze > requirements.txt
        $ touch app.py

     >> app.py:

      from flask import Flask
      app = Flask(__name__)

      @app.route('/')
      def hello_world():
          return 'Hello, Docker!'


    >> Test the application:
    
        python3 -m flask run
    
   >> Dockerfile
   
      # syntax=docker/dockerfile:1

      FROM python:slim

      WORKDIR /app

      COPY requirements.txt requirements.txt
      RUN pip3 install -r requirements.txt

      COPY ..

      CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]


   >> With mysql:
   >>  Create Voluem and network
        
        docker volume create mysql
        docker volume create mysql_config
        docker network create mysqlnet
        
        docker run --rm -d -v mysql:/var/lib/mysql \
        -v mysql_config:/etc/mysql -p 3306:3306 \
        --network mysqlnet \
        --name mysqldb \
        -e MYSQL_ROOT_PASSWORD=password1 \
        mysql
  



   docker exec -it mysqldb  -u root -p 
   
 ![image](https://user-images.githubusercontent.com/54719289/116998160-b33c0a00-acd5-11eb-8453-bf0c145878e8.png)

    
# Run the image as container

        docker run --name python-docker -p 5000:5000 -d python-docker:latest
        

![image](https://user-images.githubusercontent.com/54719289/116995391-ec727b00-acd1-11eb-8e26-499b1759d832.png)


        docker run for database:
        
        $ docker run \
            --rm -d \
            --network mysqlnet \
            --name rest-server \
            -p 5000:5000 \
            python-docker
            

# Develop your app

        $ pip3 install mysql-connector-python
        $ pip3 freeze > requirements-mysql.txt


        docker-compose -f docker-compose..yml up --build
        
        
# Configure CI/CD

# Deploy your app
