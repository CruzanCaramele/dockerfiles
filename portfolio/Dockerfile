FROM alpine:latest

# update container
RUN apk add --update py-pip

# add files
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# Copy applications
COPY app.py /usr/src/app/
COPY templates/ /usr/src/app/templates/
COPY static/ /usr/src/app/static/

# port number 
EXPOSE 8000

# run the application
CMD ["python", "/usr/src/app/app.py"]

