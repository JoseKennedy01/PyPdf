# Arquitetura — PyPdf

## Objetivo e situação

Esta é uma arquitetura recomendada para o MVP; não há implementação ainda. A proposta deve ser revisada por Kennedy e Thiago.

## Recomendação

Usar um monólito Django renderizado no servidor: Django entrega templates HTML e recebe formulários de conversão; CSS e JavaScript complementam a interface. Não há necessidade inicial de uma API separada ou de um front-end SPA, o que reduz configuração e manutenção para uma equipe de duas pessoas.

A lógica de processamento deve ficar em serviços separados das views. Assim, uma view trata a requisição HTTP e autenticação, enquanto o serviço trata da conversão.

## Componentes

| Componente | Responsabilidade |
|---|---|
| Navegador | Exibir páginas e enviar arquivos por formulário |
| Templates e arquivos estáticos | Interface, estilos e scripts |
| Aplicação contas | Cadastro, login e logout |
| Aplicação conversoes | Upload, validação, autorização e resposta de download |
| Validadores | Tamanho, assinatura e leitura do documento |
| Serviços | Orquestração de cada conversão sem lógica HTTP |
| Adaptadores | Isolar bibliotecas ou executáveis externos |
| Área temporária privada | Arquivos de entrada e saída durante a tarefa |
| Django e banco | Contas, sessão e eventual metadado mínimo de tarefas |

## Fluxo recomendado

1. Usuário autenticado envia um arquivo.
2. O navegador pode verificar extensão e tamanho para orientar o usuário, mas isso não é uma proteção de segurança.
3. Django verifica sessão, CSRF e limite de upload.
4. Validador verifica assinatura real e se o documento pode ser aberto.
5. Serviço converte em diretório temporário com nome aleatório.
6. Aplicação confirma formato e existência do resultado.
7. Download é liberado apenas à conta proprietária da tarefa.
8. Arquivos temporários são apagados segundo a política em 11_dados_e_arquivos.md.

## Processamento

Para o MVP, recomenda-se processamento síncrono apenas com limites rigorosos de páginas, tempo e memória. O pedido HTTP permanece aberto durante a conversão. Se medições mostrarem que isso não atende, avaliar fila de tarefas e processo isolado antes de acrescentar OCR ou conversões pesadas.

## Login por e-mail

Recomendação para o primeiro dia de código: modelo de usuário Django próprio baseado em AbstractUser, com e-mail único, configurado antes da primeira migração. A documentação alerta que trocar AUTH_USER_MODEL depois de criar tabelas pode exigir migração manual complexa.

Referência: [personalização do usuário no Django](https://docs.djangoproject.com/en/6.1/topics/auth/customizing/).

## Limites

Hospedagem, banco de produção, fila e provedor de e-mail seguem em aberto. O limite de 15 MB é por arquivo; limites de páginas, resolução e tempo dependem de medições. As bibliotecas citadas ainda não estão instaladas.