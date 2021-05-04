FROM python:slim
WORKDIR /app
COPY /python-dcoker/requirements.txt requirements.txt
COPY /python-dcoker/app.py app.py
RUN pip3 install -r requirements.txt
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]
