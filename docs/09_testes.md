# Estratégia de testes — PyPdf

## Ferramentas

Recomenda-se começar com o executor de testes incluído no Django e Django TestCase, evitando dependência extra. Avaliar pytest/pytest-django se a equipe encontrar benefício. Ruff pode ser usado como ferramenta de desenvolvimento para lint e formatação; tem licença MIT.

Django documenta seu framework e integração com outros executores: [testes Django](https://docs.djangoproject.com/en/6.1/topics/testing/). [Licença Ruff](https://github.com/astral-sh/ruff/blob/main/LICENSE).

## Camadas de teste

### Unidade
Regras de tamanho/formato, nomes de saída, ZIP, mapeamento de erros e autorização de tarefas.

### Integração
Upload autenticado, bloqueio sem login, CSRF, chamada ao serviço, download e limpeza.

### Conversão
PDF sintético de uma e várias páginas, PNG válido, formato inválido, arquivo protegido e conferência da quantidade/formato da saída.

### Segurança
Extensão falsa, arquivos vazios/corrompidos, nome com caminho/Unicode, limite 15 MB, timeout, acesso de outra conta, logs e limites de recursos.

### Desempenho
Medir tempo e memória para combinações representativas de páginas e resolução. Separar upload, conversão e download, registrar ambiente e não generalizar benchmark local para hospedagem.

## Organização futura

Usar pastas de testes por aplicação ou uma pasta central, a decidir no scaffold. Arquivos com prefixo test_ para descoberta automática. Gerar fixtures por código; não armazenar documentos privados ou reais no Git.

## Estado

Ainda não há código, testes de funcionalidade ou resultados medidos. Esta é a estratégia futura; nenhum teste foi criado ou executado.