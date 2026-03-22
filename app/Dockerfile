# Python 3.11 の軽量イメージをベースに使用
FROM python:3.11-slim

# 作業ディレクトリを設定
WORKDIR /app

# 1. curl をインストール（Debian/Ubuntu 系の apt を使用）
# rm -rf でキャッシュを消去してイメージサイズを軽量に保ちます
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*

# 2. 依存パッケージファイルをコピー
COPY requirements.txt .

# 3. Python パッケージをインストール
RUN pip install --no-cache-dir -r requirements.txt

# 4. アプリケーションファイルをコピー
COPY . .

# Flask が使用するポートを公開
EXPOSE 5000

# Gunicorn で起動
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "2", "--timeout", "60", "app:app"]
