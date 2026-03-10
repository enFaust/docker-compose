# Multi-stage Dockerfile for Python Flask application

FROM python:3.9-slim as build
WORKDIR /app
COPY requirements.txt .
RUN pip install --user -r requirements.txt
FROM python:3.9-slim as runtime
COPY --from=build /root/.local /root/.local
COPY app.py .
ENV PATH=/root/.local/bin:$PATH
EXPOSE 5000
CMD ["python", "app.py"]