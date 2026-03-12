# Knowledge Base: API & System Troubleshooting
Este guia contém os procedimentos operacionais padrão (SOP) para a investigação de erros técnicos reportados via tickets de suporte L2/L3.

# 1. Erro de Autenticação (401 Unauthorized)
Cenário: O usuário reporta que "a integração parou de funcionar" ou "não consigo logar via API".

Checklist de Investigação:

Validação de Header: Verificar se o campo Authorization: Bearer <TOKEN> está presente no header da requisição.

Excluir Espaços: Confirmar se o cliente não incluiu espaços em branco acidentais ao copiar a API Key.

Expiração: Validar se o token JWT não expirou (utilizando ferramentas como jwt.io para conferir o campo exp).

# Exemplo de Resposta JSON de Erro:
```
{
  "error": "unauthorized",
  "message": "Invalid or expired token. Please generate a new API Key in your dashboard.",
  "status": 401
}
```

# 2. Recurso não Localizado (404 Not Found)
Cenário: O cliente fornece um ID de pedido/usuário, mas o sistema diz que ele não existe.

Checklist de Investigação:

Syntax Check: Validar se o endpoint está seguindo a estrutura correta (ex: /api/v1/orders/123 em vez de /api/v1/order/123).

Database Query (SQL): Executar uma query no banco de dados para verificar o status do registro:
SELECT id, status, deleted_at 
FROM orders 
WHERE id = '123';

Soft Delete: Verificar se o campo deleted_at está preenchido (o dado existe no banco, mas foi "excluído" logicamente).

# 3. Limite de Requisições Excedido (429 Too Many Requests)
Cenário: O cliente está tentando sincronizar muitos dados de uma vez e a API bloqueia o acesso.

Checklist de Investigação:

Rate Limiting: Verificar nos logs se o cliente ultrapassou o limite de requisições por minuto (RPM) do plano atual.

Log Analysis: Identificar o IP ou a API Key que está gerando o alto volume.

Solução: Orientar o cliente a implementar uma lógica de Exponential Backoff (esperar um tempo crescente antes de tentar novamente) ou sugerir o upgrade de plano.

# 4. Erro Interno / Timeout (500 / 504 Error)
Cenário: A tela fica branca ou o sistema retorna "Internal Server Error".

Checklist de Investigação:

Chrome DevTools: Abrir a aba Network, encontrar a requisição vermelha e olhar a aba Response.

Server Logs: Procurar por Stack Traces nos logs do servidor (ex: Grafana/Loki) para identificar se o erro é no banco de dados ou no código.

Payload Size: Verificar se o arquivo/JSON enviado pelo usuário não é grande demais para o processamento do servidor.

# Dicas para o Analista de Suporte:

Sempre peça o Request ID para rastrear nos logs.

Sempre verifique se o problema ocorre apenas em um navegador (cache/cookies) ou em todos.

Documente a solução no ticket para alimentar a base de dados de problemas conhecidos (ITIL - Problem Management).
