# PyPdf

Aplicação web planejada para conversão de documentos com Python e Django.

> **Status:** planejamento e documentação. Cadastro, login e conversões ainda não foram implementados.

## MVP aprovado

- Cadastro e login com e-mail e senha.
- PDF para PNG: uma imagem por página; ZIP quando houver várias.
- PNG para PDF.
- Limite de 15 MB por arquivo.
- PDFs protegidos por senha serão recusados inicialmente.

## Escopo futuro

- PDF ↔ Word (DOCX).
- PDF ↔ Excel (XLSX).
- OCR para PDFs digitalizados.
- Bloqueio e desbloqueio de PDF com senha.

PDF para Word será de melhor esforço, sem promessa de fidelidade exata. As tecnologias seguem como recomendações sujeitas à revisão da equipe.

## Tecnologias planejadas

- Python e Django no servidor.
- HTML, CSS e JavaScript na interface.
- Git e GitHub Desktop.
- pypdfium2 como candidata para PDF → PNG.
- Pillow como candidata para PNG → PDF.
- Outras conversões e OCR serão avaliados conforme [decisões técnicas](docs/04_decisoes_tecnicas.md).

As ferramentas ainda não foram instaladas ou testadas. O repositório usa MIT; licenças de dependências e binários serão verificadas antes da adoção.

## Documentação

- [Visão do produto](docs/01_visao_produto.md)
- [Requisitos](docs/02_requisitos.md)
- [Arquitetura](docs/03_arquitetura.md)
- [Decisões técnicas](docs/04_decisoes_tecnicas.md)
- [Segurança e privacidade](docs/05_seguranca.md)
- [Conversões](docs/06_conversoes.md)
- [Interface web](docs/07_frontend.md)
- [Back-end](docs/08_backend.md)
- [Estratégia de testes](docs/09_testes.md)
- [Execução local](docs/10_execucao.md)
- [Dados e arquivos](docs/11_dados_e_arquivos.md)

## Colaboração

Kennedy conduz o projeto com participação no front-end e back-end. Thiago participa mais do front-end e também auxilia no back-end. O fluxo combinado usa branches por tarefa e pull requests revisados em conjunto; main é a linha principal.

## Segurança

Uploads são entrada não confiável. Validação, limites de processamento, isolamento, download autenticado e exclusão temporária serão definidos antes do lançamento. Não envie credenciais, .env, documentos privados ou resultados ao repositório público.

## Execução

A aplicação ainda não é executável. As instruções serão adicionadas após a criação do scaffold e a definição das dependências.