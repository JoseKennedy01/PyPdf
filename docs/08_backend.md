# Back-end — PyPdf

## Abordagem recomendada

Django cuida de autenticação, sessão, CSRF, rotas, formulários e respostas. Serviços separados executam o processamento de documentos.

## Aplicações previstas

### contas
Cadastro de e-mail/senha, login/logout e modelo de usuário. Recomenda-se e-mail único e configuração anterior à primeira migração. Django auth deve cuidar de hashing e sessão.

### conversoes
Formulários de upload, autorização, validadores, serviços PDF → PNG e PNG → PDF, download PNG/PDF/ZIP e mensagens seguras.

## Separação de responsabilidades

- visualizacoes.py: autenticar, validar requisição, chamar serviço e responder HTTP.
- formularios.py: validar os dados do formulário.
- validadores.py: verificar tipo, assinatura e limites.
- servicos/: orquestrar operações sem lógica HTTP.
- adaptadores/: encapsular biblioteca ou processo externo se a complexidade justificar.
- modelos.py/model.py: só criar modelo de tarefa se houver decisão de persistir metadados.

Arquivos do projeto podem usar português. Nomes estruturais padrão como manage.py, settings.py, urls.py e migrations/ permanecem conforme convenções e ferramentas Django.

## Usuário por e-mail

Recomendação para o primeiro dia de código: usuário customizado Django baseado em AbstractUser, com e-mail único, configurado em AUTH_USER_MODEL antes da primeira migração. Cadastro inicial terá apenas e-mail e senha; confirmação e recuperação ficam para decisão futura.

Referências: [autenticação Django](https://docs.djangoproject.com/en/6.1/topics/auth/) e [customização de usuários](https://docs.djangoproject.com/en/6.1/topics/auth/customizing/).

## Upload e conversão

- Usar request.FILES e chunks quando adequado.
- Limitar corpo no servidor/proxy e no Django.
- Não confiar em nome, extensão ou content_type do cliente.
- Usar diretório temporário fora da pasta pública.
- Não montar caminhos com nome enviado pelo usuário.
- Definir timeout para biblioteca ou executável.
- Limpar em falha e periodicamente remover sobras.
- Não armazenar arquivos permanentemente nem criar histórico sem decisão da equipe.

## Respostas e implantação

Formulários POST usam CSRF. Rota de download também valida conta proprietária. Exceções viram mensagens seguras, sem traceback ao usuário. runserver é somente para desenvolvimento; produção depende de servidor WSGI/ASGI, banco, proxy e hospedagem a escolher.