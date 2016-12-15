FROM alpine:latest

RUN apk add --update py-pip

# add the files that make up the Flask Application
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# Copy application file and template file
COPY app.py /usr/src/app/
COPY templates/index.html /usr/src/app/templates/

# port number
EXPOSE 5000

# run the application
CMD ["python", "usr/src/app/app.py"]