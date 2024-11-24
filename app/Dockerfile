# Use the official Python image from the Docker Hub, specifically Python 3.10 on Alpine
FROM python:3.10-alpine

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set the working directory in the container
WORKDIR /app

# Install dependencies required for building Python packages
# RUN apk update && apk add --no-cache gcc musl-dev libffi-dev

# Copy the requirements.txt file to the working directory
COPY requirements.txt /temp/requirements.txt


# Copy the rest of the application code to the working directory
COPY . /app

# Expose the port that the Django app will run on
EXPOSE 8000

# RUN python -m venv /py &&\
#     /py/bin/pip install --upgrade pip &&\
#     /py/bin/pip install --no-cache-dir -r /temp/requirements.txt &&\
#     rm -rf /temp

RUN ["pip","install","--upgrade","pip"]
RUN ["pip","install","--no-cache-dir","-r","/temp/requirements.txt"]
RUN ["rm","-rf","/temp"]

        
ENV PATH="/bin:$PATH"

# CMD ["python3","manage.py","runserver","0.0.0.0:8000"]
CMD ["gunicorn", "my_project.wsgi:application", "--bind", "0.0.0.0:8000"]