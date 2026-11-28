# PyPdf

Aplicação web planejada para converter documentos entre PDF, Word, Excel e PNG.

> **Status:** planejamento inicial. As conversões descritas abaixo ainda não foram implementadas.

## Objetivo

O PyPdf tem como objetivo oferecer uma interface web para converter documentos entre PDF, DOCX, XLSX e PNG, usando ferramentas sem custo de licença ou serviços pagos.

## Funcionalidades planejadas

- PDF para Word (DOCX) e Word (DOCX) para PDF.
- PDF para Excel (XLSX) e Excel (XLSX) para PDF.
- PDF para PNG, gerando uma imagem por página.
- PNG para PDF.
- OCR para auxiliar no processamento de PDFs escaneados.

A conversão de PDF para Word será de melhor esforço. O arquivo resultante será editável, mas pode não preservar exatamente o layout, as tabelas, as imagens ou a formatação do original. Resultados de OCR também podem conter erros e precisar de revisão.

A ferramenta específica para PDF → Word ainda será avaliada com arquivos de exemplo e com atenção às licenças de suas dependências. Não será usado serviço comercial ou API paga.

## Limites planejados

- Tamanho máximo: 15 MB por arquivo enviado.
- PDF para PNG: cada página gera uma imagem PNG.
- PDFs com várias páginas: proposta de disponibilizar as imagens em um arquivo ZIP.

O limite de páginas e o tempo máximo de processamento ainda serão definidos. O limite de tamanho, sozinho, não determina o esforço de processar um documento.

## Tecnologias planejadas

- Python e Django no servidor.
- HTML, CSS e JavaScript na interface.
- `uv` para gerenciar dependências e o ambiente Python.
- SQLite para desenvolvimento inicial, com reavaliação do banco quando os requisitos de implantação forem definidos.
- `pypdfium2` como candidata para PDF para PNG.
- Pillow como candidata para PNG para PDF.
- LibreOffice como opção gratuita para Word/Excel para PDF.
- Tesseract e OCRmyPDF como candidatos para OCR.
- Camelot como candidata para extrair tabelas de PDF para Excel.
- Uma solução gratuita própria ou compatível com a licença do projeto para PDF → Word; seleção e qualidade ainda em avaliação.

Essas tecnologias são planejadas ou candidatas. Nenhuma conversão foi implementada.

## Estrutura planejada

```text
config/       Configurações principais do Django
conversions/  Formulários, validações e serviços de conversão
docs/         Arquitetura, segurança e decisões do projeto
```

A estrutura completa será atualizada quando os arquivos forem criados.

## Desenvolvimento

O projeto está sendo planejado por dois integrantes. O fluxo de colaboração proposto usa a branch `main`, branches curtas por tarefa e pull requests revisados pelo outro integrante.

O repositório usa a licença MIT. Consulte o arquivo `LICENSE` para conhecer os termos completos. As licenças das dependências também serão verificadas antes de serem adotadas.

## Segurança e privacidade

Os arquivos enviados devem ser tratados como entrada não confiável. Antes de disponibilizar o aplicativo, serão definidos validação de conteúdo, limites de páginas e tempo, processamento isolado, armazenamento temporário e política de exclusão.

OCRmyPDF recomenda isolamento ao processar PDFs não confiáveis; o processamento público precisará de uma arquitetura segura para esse trabalho. [Aviso de segurança do OCRmyPDF](https://ocrmypdf.readthedocs.io/en/latest/pdfsecurity.html)

Não envie ao repositório senhas, tokens, chaves, arquivos `.env` ou documentos privados.

## Execução

A execução local ainda não está disponível. As instruções serão adicionadas quando a estrutura Django e as dependências forem criadas.