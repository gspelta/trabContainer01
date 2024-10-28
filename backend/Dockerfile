# Use uma imagem base oficial do Python
FROM python:3.9-slim

# Define o diretório de trabalho
WORKDIR /app

# Copia os arquivos da pasta guess_game para o diretório de trabalho
COPY . .

# Instala as dependências necessárias
RUN pip install --no-cache-dir -r requirements.txt

# Define a variável de ambiente para que o Flask não use o modo debug
ENV FLASK_ENV=production

# Expõe a porta em que o Flask estará rodando
EXPOSE 5000

# alterando chmod para executar arquivo
RUN chmod +x start-backend.sh

# Define o comando padrão para rodar a aplicação Flask
CMD ["./start-backend.sh"]
