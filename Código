# Vamos preparar os arquivos iniciais do projeto como prometido:
# Criaremos: data/items.csv, app/recommender.py, app/main.py, requirements.txt, README.md

import os

# Criar diretórios
os.makedirs("recommender_project/app/models", exist_ok=True)
os.makedirs("recommender_project/data", exist_ok=True)

# Criar arquivo CSV com dados de exemplo
csv_data = """item_id,title,genre
1,Matrix,Sci-Fi
2,Inception,Sci-Fi
3,The Godfather,Crime
4,Shrek,Animation
5,Toy Story,Animation
"""
with open("recommender_project/data/items.csv", "w") as f:
    f.write(csv_data)

# recommender.py
recommender_code = '''import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import linear_kernel

class ContentRecommender:
    def __init__(self, data_path):
        self.df = pd.read_csv(data_path)
        self.vectorizer = TfidfVectorizer()
        self.tfidf_matrix = self.vectorizer.fit_transform(self.df['genre'])

    def recommend(self, item_title, top_n=3):
        idx = self.df[self.df['title'] == item_title].index[0]
        cosine_similarities = linear_kernel(self.tfidf_matrix[idx], self.tfidf_matrix).flatten()
        similar_indices = cosine_similarities.argsort()[::-1][1:top_n+1]
        return self.df.iloc[similar_indices][['title', 'genre']].to_dict(orient='records')
'''

with open("recommender_project/app/recommender.py", "w") as f:
    f.write(recommender_code)

# main.py
main_code = '''from fastapi import FastAPI
from recommender import ContentRecommender

app = FastAPI()
recommender = ContentRecommender("data/items.csv")

@app.get("/recommend")
def get_recommendations(title: str, top_n: int = 3):
    return recommender.recommend(title, top_n)
'''

with open("recommender_project/app/main.py", "w") as f:
    f.write(main_code)

# requirements.txt
requirements = '''fastapi
uvicorn
pandas
scikit-learn
'''
with open("recommender_project/requirements.txt", "w") as f:
    f.write(requirements)

# README.md
readme = '''# Sistema de Recomendação com FastAPI

Este projeto é um sistema de recomendação simples baseado em conteúdo, usando Python, pandas, scikit-learn e FastAPI.

## Como executar

1. Instale as dependências:
