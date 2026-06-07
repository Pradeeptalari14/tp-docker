# Option: python:3.11-slim + Single-stage + Non-root
FROM python:3.11-slim
WORKDIR /app
ENV PORT=8080
RUN groupadd -r sre_group && useradd -r -g sre_group sre_user
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
RUN chown -R sre_user:sre_group /app
USER sre_user
EXPOSE 8080
CMD ["uvicorn","main:app","--host","0.0.0.0","--port","8080"]