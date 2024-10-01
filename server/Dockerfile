# Use the official Python slim image as the base image
FROM python:3.12.0-slim-bookworm

# Set environment variables
ENV PYTHONUNBUFFERED 1
ENV PYTHONWRITEBYTECODE 1

# Define the application directory
ENV APP=/app

# Change the working directory
WORKDIR $APP

# Copy the requirements.txt file to the working directory
COPY requirements.txt $APP

# Install the required packages
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Copy the rest of the application files to the working directory
COPY . $APP

# Expose the port that the app runs on
EXPOSE 8000

RUN chmod +x /app/entrypoint.sh
ENTRYPOINT ["/bin/bash", "/app/entrypoint.sh"]

# Start the application using Gunicorn
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]
