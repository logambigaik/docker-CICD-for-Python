# Docker-CICD-for-Python

# Build the Image

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
    
    
# Run the image as container

        docker run --name python-docker -p 5000:5000 -d python-docker:latest

![image](https://user-images.githubusercontent.com/54719289/116995391-ec727b00-acd1-11eb-8e26-499b1759d832.png)


# Develop your app

# Configure CI/CD

# Deploy your app
