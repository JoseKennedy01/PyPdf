# Execução local — PyPdf

## Estado atual

O repositório ainda não possui scaffold Django, dependências instaláveis ou comando de execução. Este documento descreve o plano futuro e não contém comandos executáveis no estado atual.

## Preparação quando o código começar

1. Escolher versão de Python compatível com Django.
2. Confirmar uv, já citado como candidato no README, antes de criar pyproject.toml e lockfile.
3. Criar estrutura Django em branch de implementação.
4. Manter segredos em .env local, ignorado pelo Git.
5. Criar .env.example somente com nomes e valores fictícios.
6. Fixar dependências e manter lockfile se o gerenciador escolhido recomendar para aplicação.

## Instruções que serão adicionadas

Após o scaffold, documentar comandos verificados em PowerShell para preparar ambiente, instalar dependências, aplicar migrações, criar usuário de desenvolvimento, executar testes, iniciar servidor local e rodar verificações de qualidade.

## Configuração segura

Não reutilizar segredo local em produção; não versionar .env, tokens ou senhas; DEBUG fica ativo somente localmente; revisar ALLOWED_HOSTS, HTTPS e cookies antes da implantação.

Referência: [checklist de implantação do Django](https://docs.djangoproject.com/en/6.1/howto/deployment/checklist/).