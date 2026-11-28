# Dados e arquivos — PyPdf

## Dados persistidos

No MVP, guardar apenas dados necessários às contas e operação. Não armazenar o conteúdo do PDF/PNG nem histórico de documentos, a menos que a equipe aprove isso depois. Metadados de tarefas devem ser mínimos e requerem decisão específica.

## Arquivos temporários — proposta

- Usar diretório por conversão fora do repositório, static e raiz pública.
- Gerar identificador aleatório e permissões mínimas.
- Manter apenas entrada, processamento e resultado.
- Vincular tarefa e download à conta.
- Excluir depois da transferência e manter rotina para apagar resíduos órfãos.
- Não salvar conteúdo em banco de dados.
- Não registrar conteúdo, senha de PDF, nome original ou caminho completo.

O prazo exato em que o resultado pode ser baixado deve ser aprovado por Kennedy e Thiago e depende da hospedagem. Não há armazenamento persistente definido.

## Nome e saída

- Criar nomes internos neutros, como pagina_001.png.
- Nunca usar nome original diretamente como caminho.
- Gerar ZIP com nomes controlados e sem estrutura fornecida pelo usuário.
- Servir tipo de conteúdo e nome de download coerentes.

## Privacidade e Git

O repositório é público. Não versionar uploads, resultados, dados de conta, .env ou documentos reais. Usar amostras sintéticas. O .gitignore ajuda, mas não substitui revisão antes de commit.

## Pendências

Prazo de disponibilidade, hospedagem, armazenamento temporário e política de logs serão revistos antes do desenvolvimento de upload e antes da implantação.