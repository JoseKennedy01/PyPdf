# Decisões técnicas — PyPdf

## Situação

Este documento registra recomendações e pesquisa; não significa que as bibliotecas foram aprovadas, instaladas ou integradas. A avaliação foi realizada em 27/11/2026. Rechecar licenças, versões e dependências quando fixarmos a instalação.

## Critérios

- Sem custo de licença ou uso de API paga.
- Preferência por ferramentas gratuitas e abertas.
- Compatibilidade com Python/Django.
- Licenças e dependências compatíveis com o MIT atual do repositório.
- Desempenho, manutenção, dependências externas e segurança avaliados com amostras.

## Opções e recomendação inicial

| Operação | Candidatas | Recomendação para protótipo | Limitações |
|---|---|---|---|
| PDF → PNG | pypdfium2, PyMuPDF, pdf2image/Poppler | pypdfium2 | Depende de binários PDFium; revisar plataforma e avisos das dependências incluídas. DPI e páginas aumentam CPU/memória. |
| PNG → PDF | Pillow, ReportLab | Pillow | A documentação descreve saída PDF; validar transparência, orientação e tamanho. |
| PDF → Word | pdfplumber + python-docx; pdf2docx + PyMuPDF | Prototipar pdfplumber + python-docx para evitar AGPL no caminho principal | Pode perder layout, fontes, colunas, imagens e tabelas. |
| Word → PDF | LibreOffice em modo de linha de comando; PyMuPDF Office | LibreOffice | Executável externo, instalação, isolamento, fontes e tempo limite. Paginação pode divergir do Microsoft Word. |
| PDF → Excel | Camelot + openpyxl; pdfplumber + openpyxl | Camelot para tabelas de PDFs digitais; pdfplumber como alternativa | PDF escaneado exige OCR; tabela visualmente complexa pode ser extraída incorretamente. Backends opcionais e extras pesados do Camelot precisam de revisão separada. |
| Excel → PDF | LibreOffice ou renderizador próprio | LibreOffice | Avaliar impressão, fórmulas, gráficos, folhas e fontes. |
| OCR | Tesseract; OCRmyPDF com Tesseract e pypdfium2 | OCRmyPDF como candidato para PDF pesquisável | Não é conversor direto para DOCX/XLSX; requer dados de idioma e componentes externos. |
| Inspeção de PDF | pypdf, pypdfium2 | pypdf pode apoiar metadados e estrutura, não renderizar páginas | Não substitui o motor de renderização. |

## Licenças

| Ferramenta | Licença/fato consultado | Consequência |
|---|---|---|
| pypdfium2 | Apache-2.0 ou BSD-3-Clause; PDFium usa licença BSD e binários têm avisos próprios | Candidata; preservar avisos dos componentes distribuídos. |
| Pillow | HPND; documenta gravação de PDF | Candidata para PNG → PDF; preservar aviso. |
| pdfplumber e pdfminer.six | MIT; pdfplumber funciona melhor com PDFs digitais e não faz OCR | Candidatas para texto e tabelas. |
| python-docx | MIT; cria/atualiza DOCX, mas não converte PDF sozinho | Precisa de extrator de PDF. |
| Camelot | MIT; extração tabular e exportação para planilha | Candidato; revisar dependências do modo escolhido. |
| openpyxl | MIT/Expat; grava e lê XLSX | Candidato para planilhas. |
| pdf2docx | Pacote declara MIT, mas importa PyMuPDF | Não adotar sem revisar dependência transitiva. |
| PyMuPDF | AGPL-3.0 ou licença comercial da Artifex | A AGPL tem obrigações de copyleft; não é compatível automaticamente com o MIT escolhido. Evitar sem revisão específica. |
| LibreOffice | MPL-2.0 e componentes com outras licenças | Candidato como executável externo; manter avisos e revisar forma de distribuição. |
| Tesseract | Apache-2.0; requer dados treinados por idioma | Candidato OCR; incluir avisos do motor e dados usados. |
| OCRmyPDF | MPL-2.0 no programa principal e dependências Python/externas | Candidato a orquestrador, não uma conversão Word/Excel pronta. |

Esta é uma triagem técnica, não uma análise jurídica. Verificar a licença exata de cada versão e dependência antes de adoção e distribuição.

## Recomendação para o MVP

- PDF → PNG: avaliar pypdfium2.
- PNG → PDF: avaliar Pillow.
- Contas: autenticação Django; usuário com e-mail único definido antes da primeira migração.
- Manter Word, Excel e OCR fora do MVP.
- Não instalar bibliotecas até aprovação do plano e criação do ambiente.

## Fontes oficiais

- [pypdfium2: licença e dependências](https://github.com/pypdfium2-team/pypdfium2#licensing)
- [Pillow: formatos e escrita de PDF](https://pillow.readthedocs.io/en/stable/handbook/image-file-formats.html)
- [pdfplumber: licença, escopo e limites](https://github.com/jsvine/pdfplumber)
- [python-docx: licença MIT](https://github.com/python-openxml/python-docx/blob/master/LICENSE)
- [Camelot: extração e licença](https://github.com/camelot-dev/camelot)
- [openpyxl](https://openpyxl.readthedocs.io/en/stable/)
- [pdf2docx importa PyMuPDF](https://github.com/ArtifexSoftware/pdf2docx/blob/master/pdf2docx/converter.py)
- [PyMuPDF: licença AGPL/comercial](https://pymupdf.readthedocs.io/en/latest/about.html#license-and-copyright)
- [LibreOffice: licenças](https://www.libreoffice.org/licenses/)
- [Tesseract: licença Apache-2.0](https://github.com/tesseract-ocr/tesseract/blob/main/LICENSE)
- [OCRmyPDF: instalação e componentes](https://ocrmypdf.readthedocs.io/en/latest/installation.html)