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
   >>  Create Volume and network
        
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

ecafa108-6865-4eac-88ec-1ff6ae58d8ee

 ![image](https://user-images.githubusercontent.com/54719289/117037361-4be68000-acfe-11eb-829a-a08d34160d2a.png)
![image](https://user-images.githubusercontent.com/54719289/117037419-5b65c900-acfe-11eb-9f0c-ed48bb42ea2f.png)
![image](https://user-images.githubusercontent.com/54719289/117037489-70daf300-acfe-11eb-810e-ac15060149a1.png)
![image](https://user-images.githubusercontent.com/54719289/117037862-e34bd300-acfe-11eb-9c0f-94fd77f11b14.png)

![image](https://user-images.githubusercontent.com/54719289/117037902-ee9efe80-acfe-11eb-9005-ab440aeecad6.png)

>> Under ACtion create workflow and select Docker-CI
![image](https://user-images.githubusercontent.com/54719289/117042378-ce257300-ad03-11eb-8c7a-1d6e9d50e3a3.png)
![image](https://user-images.githubusercontent.com/54719289/117042429-e09fac80-ad03-11eb-9a7c-8e1d022e3394.png)

![image](https://user-images.githubusercontent.com/54719289/117042212-93bbd600-ad03-11eb-8ca9-9d5fdfe45ae4.png)

# Deploy your app

![image](https://user-images.githubusercontent.com/54719289/117046388-8bb26500-ad08-11eb-88f7-0f9eb61cfb63.png)

