FROM python:slim-bullseye
RUN apt-get update && apt-get install -y procps vim apache2-utils && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt requirements
RUN pip3 install -r requirements.txt

COPY . .
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]