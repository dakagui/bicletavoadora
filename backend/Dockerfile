## Reference https://fastapi.tiangolo.com/deployment/docker/
FROM python:3.10.1 as requirements-stage

WORKDIR /tmp
 
RUN pip install poetry
 
COPY ./pyproject.toml ./poetry.lock* /tmp/
 
RUN poetry export -f requirements.txt --output requirements.txt --without-hashes
 
FROM python:3.10.1
 
WORKDIR /code
 
COPY --from=requirements-stage /tmp/requirements.txt /code/requirements.txt
 
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
 
COPY ./app /code/app

EXPOSE 8080 

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
