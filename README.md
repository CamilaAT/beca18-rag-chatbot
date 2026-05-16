# Beca 18 RAG Chatbot — PRONABEC

## Descripción
Sistema de preguntas y respuestas basado en Recuperación Aumentada con Generación (RAG) 
sobre el Reglamento Oficial de Beca 18 (Resolución Directoral Ejecutiva N.° 033-2026-MINEDU/VMGI-PRONABEC). 
El chatbot responde exclusivamente con información del documento oficial, citando el número 
de página fuente, y rechaza preguntas fuera del alcance del reglamento.

## Pipeline
El sistema extrae texto del PDF página por página, lo divide en chunks de 400 tokens con 
overlap de 60, genera embeddings con gemini-embedding-001 (3072 dimensiones), los indexa 
en ChromaDB con distancia coseno, y ante cada pregunta recupera los k fragmentos más 
relevantes para fundamentar la respuesta de gemini-2.0-flash.

## Instalación
```bash
pip install -r requirements.txt
```

## Configuración API Key
1. Obtén tu key en https://aistudio.google.com/app/apikey
2. Crea un archivo `.env` en la raíz con: GEMINI_API_KEY=tu_key_aqui

## Cómo ejecutar
1. Coloca el PDF en `data/beca18_reglamento.pdf`
2. Abre `notebooks/beca18_rag_chatbot.ipynb` en Google Colab
3. Ejecuta todas las celdas en orden
4. El índice ChromaDB se construye automáticamente en el primer run

## Uso del chatbot
- Escribe tu pregunta en el campo de texto
- Ajusta el slider **k** para controlar cuántos fragmentos recuperar (default: 5)
- Click **"Preguntar"** para obtener la respuesta
- Expande **"Fuentes recuperadas"** para ver los fragmentos del documento usados
- Click **"Limpiar"** para resetear la interfaz