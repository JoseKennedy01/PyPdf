# Segurança e privacidade — PyPdf

## Princípio

Todo arquivo recebido é entrada não confiável. Extensão, nome, MIME informado pelo navegador ou tamanho, sozinhos, não provam que o arquivo é seguro.

## Controles recomendados

1. Exigir sessão autenticada e proteção CSRF no upload.
2. Limitar o corpo da requisição no servidor/proxy e validar até 15 MB por arquivo no Django. Os limites de memória internos não substituem o limite do servidor web.
3. Verificar extensão permitida, assinatura real e capacidade de abrir o documento. Não confiar em content_type enviado pelo cliente.
4. Processar uploads em blocos quando adequado, evitando carregá-los integralmente na memória.
5. Gerar nomes internos aleatórios; nunca usar nome enviado pelo usuário como caminho.
6. Processar fora de diretórios públicos/estáticos e sem permissão de execução.
7. Limitar páginas, pixels/DPI, CPU, memória, tempo e concorrência. Determinar valores por medição antes do lançamento.
8. Executar conversores com timeout, permissões mínimas e, em serviço público, isolamento sem rede e volume limitado.
9. Proteger downloads com autenticação e autorização da sessão proprietária.
10. Excluir entradas/saídas temporárias e manter rotina para arquivos órfãos após falhas.
11. Não registrar conteúdo, senha de PDF, token, nome original ou caminhos privados.
12. Em produção, manter DEBUG desativado, segredos em variáveis de ambiente e revisar HTTPS e cookies seguros.

Django recomenda limitar o corpo do upload no servidor web e alerta que não há validação universal que torne qualquer arquivo seguro. [Segurança de uploads no Django](https://docs.djangoproject.com/en/6.1/topics/security/#user-uploaded-content). Ler uploads em blocos evita picos de memória. [Uploads no Django](https://docs.djangoproject.com/en/6.1/ref/files/uploads/).

## Riscos e respostas

| Risco | Resposta proposta |
|---|---|
| Extensão ou MIME falsificados | Validar conteúdo real e tentar abrir com ferramenta apropriada |
| PDF malformado/ativo | Atualizar conversor e isolar processamento; conversão não é antivírus |
| PDF protegido por senha | Recusar no MVP; nunca tentar descobrir senha |
| Muitas páginas/resolução extrema | Limitar páginas e DPI, tempo, memória e concorrência |
| Path Traversal | Nome interno aleatório e diretório de tarefa; não concatenar nome enviado |
| ZIP Slip/ZIP Bomb | MVP não recebe ZIP; ao gerar ZIP usar nomes controlados e limites de quantidade/tamanho |
| Abuso de recursos | Limites no servidor, rate limit por conta/IP e concorrência limitada |
| Acesso ao resultado de outro usuário | Associar tarefa à conta e autorizar cada download |
| Vazamento por mensagem/log | Mensagens seguras; logs privados mínimos e sem conteúdo |

OCRmyPDF declara que não foi projetado para proteger contra malware em PDFs e recomenda isolamento para arquivos não confiáveis. [Segurança de PDFs no OCRmyPDF](https://ocrmypdf.readthedocs.io/en/latest/pdfsecurity.html).

## Credenciais e configuração

- Usar autenticação e hashing de senha do Django.
- Nunca armazenar senha em texto puro.
- Não versionar SECRET_KEY, credenciais, tokens, .env, uploads nem resultados.
- .env.example deve conter apenas valores fictícios.
- Revisar DEBUG, ALLOWED_HOSTS, HTTPS e cookies antes de publicar.
- [Checklist de implantação segura do Django](https://docs.djangoproject.com/en/6.1/howto/deployment/checklist/).

## Armazenamento: recomendação pendente

Recomenda-se não guardar documentos permanentemente. Manter cada conversão em pasta temporária fora do repositório e da raiz pública, identificada por token aleatório, e liberar o resultado somente à conta dona da tarefa. Apagar após download e usar rotina de limpeza para resíduos. O prazo exato para baixar deve ser aprovado por Kennedy e Thiago conforme limites da hospedagem.

## Pontos abertos

- Número máximo de páginas, DPI, tempo e concorrência.
- Prazo de download e hospedagem.
- Forma de rate limit do serviço.
- Verificação antivírus adicional, a reavaliar antes de abrir ao público.
- O isolamento tem de ser validado no servidor real; desenvolvimento local não representa essa proteção.