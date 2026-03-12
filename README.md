# API Troubleshooting & Support Guide
Este repositório demonstra habilidades técnicas de Suporte L2/L3, focando na investigação de erros em plataformas SaaS, consumo de APIs e documentação técnica para resolução de incidentes.

# Tecnologias e Ferramentas

Postman: Testes de requisições e validação de endpoints.

Protocolo HTTP: Análise de métodos (GET, POST, PUT, DELETE) e Status Codes.

JSON: Manipulação e análise de estruturas de dados de retorno.

Markdown: Documentação técnica para KB (Knowledge Base).

# O que compõe este projeto?

Postman_Collections/: Arquivo JSON pronto para importação no Postman com chamadas configuradas para uma API pública.

Guides/Common_Errors.md: Um guia prático de "Causa Raiz" para os erros mais comuns encontrados por usuários.

Logs/Sample_Payloads.md: Exemplos de payloads JSON (Request/Response) de sucesso e erro.

# Cenários de Troubleshooting (Exemplos)

Neste projeto, simulo a investigação dos seguintes cenários:

# 1. Erro 401 Unauthorized

Cenário: O cliente tenta buscar dados, mas recebe erro de autorização.

Investigação: Verificação de Headers (Authorization: Bearer <token>) e validade da API Key.

Resolução: Passo a passo para o cliente regenerar o token no painel administrativo.

# 2. Erro 404 Not Found

Cenário: O dashboard não carrega as informações de um ID específico.

Investigação: Validação da URL dinâmica e conferência via SQL/BigQuery se o ID existe na base de dados.

#3. Erro 429 Too Many Requests

Cenário: Integração do cliente para de funcionar subitamente.

Investigação: Análise de Rate Limiting (limite de requisições por minuto).

# Como utilizar

Importe a coleção da pasta /Postman_Collections para o seu Postman.

Configure a base_url para https://jsonplaceholder.typicode.com/ 

Execute os testes e observe as respostas no console.

# Por que isso é relevante para Suporte Técnico?

Analistas de suporte em empresas SaaS precisam atuar como ponte entre o cliente e a engenharia. Este projeto demonstra que possuo a capacidade analítica para identificar se um problema está na requisição do cliente (Client-side) ou no servidor (Server-side), reduzindo o tempo de resolução (MTTR).
