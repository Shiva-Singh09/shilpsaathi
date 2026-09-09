FROM python:3.11-slim

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libgl1 \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt ./
RUN pip install --no-cache-dir --upgrade pip setuptools wheel && \
    pip install --no-cache-dir -r requirements.txt

RUN python -c "from rembg import new_session; new_session('u2net')"

COPY . .

RUN ls -lh /root/.u2net/u2net.onnx && \
    python -c "import os; print('U2NET EXISTS:', os.path.exists('/root/.u2net/u2net.onnx')); print('HOME:', os.environ.get('HOME'))"

ENV PORT=8000
EXPOSE 8000

CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port ${PORT:-8000}"]