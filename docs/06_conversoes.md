# Conversões — PyPdf

## Escopo do MVP

Aprovado:
- PDF → PNG.
- PNG → PDF.
- Cadastro/login com e-mail e senha.
- Limite de 15 MB por arquivo.
- Uma imagem PNG por página de PDF.
- ZIP quando a saída tiver várias imagens.
- Recusa de PDFs protegidos por senha.

Nada disso foi implementado ainda.

## Operações e tecnologias candidatas

| Operação | Entrada e resultado | Tratamento | Recomendação de protótipo |
|---|---|---|---|
| PDF → PNG | PDF sem senha até 15 MB; uma imagem por página | PNG direto para uma página; ZIP para várias | pypdfium2 |
| PNG → PDF | Um PNG até 15 MB; PDF de uma página | Preservar proporção e orientação | Pillow |
| PDF → DOCX (futuro) | PDF digitalizado ou com texto; DOCX editável | Layout e tabelas podem divergir; OCR à parte para scans | Comparar pdfplumber + python-docx com pdf2docx, revendo licença transitiva |
| DOCX → PDF (futuro) | DOCX para PDF | Fontes e paginação podem divergir | LibreOffice isolado |
| PDF → XLSX (futuro) | PDF com tabelas para planilha | Scans exigem OCR; conferir células | Camelot + openpyxl; pdfplumber alternativa |
| XLSX → PDF (futuro) | Planilha para PDF | Conferir impressão, fórmulas, gráficos e fontes | LibreOffice isolado |
| OCR (futuro) | PDF digitalizado para PDF pesquisável/texto | Acurácia varia por idioma e scan | OCRmyPDF + Tesseract; não converte sozinho para DOCX/XLSX |

## Regras para as saídas do MVP

- Cada página PDF gera exatamente um PNG.
- PDF de uma página retorna PNG direto; PDF com várias páginas retorna ZIP.
- PNG gera PDF de uma página no MVP.
- ZIP tem nomes neutros controlados pela aplicação, sem pastas enviadas pelo usuário.
- Arquivo inválido ou resultado parcial nunca é apresentado como sucesso.
- PDF com senha é recusado.

## Qualidade

PDF → PNG é renderização, não extração de texto. DPI alto melhora definição, mas aumenta CPU, memória e saída. O padrão DPI e limite de páginas devem ser medidos antes de aprovação pública.

PDF → Word/Excel varia com o documento. PDFs digitais costumam ser mais fáceis de extrair que scans. Não prometer layout idêntico; validar com amostras e permitir revisão manual.

## Casos para testes futuros

- PDF de 1 página e várias páginas.
- PNG válido com diferentes dimensões e modos de cor.
- Arquivos vazios, truncados, corrompidos, protegidos e extensão falsa.
- Abaixo, no limite e acima de 15 MB.
- Timeout, falha parcial e conversor ausente.
- Página gigante ou excesso de páginas.
- Tentativa de usuário obter resultado de outra conta.
- Nome original com caracteres especiais e tentativas de Path Traversal.

## Fontes

- [pypdfium2](https://github.com/pypdfium2-team/pypdfium2)
- [Pillow: escrita de PDF](https://pillow.readthedocs.io/en/stable/handbook/image-file-formats.html)
- [pdfplumber: extração e limites](https://github.com/jsvine/pdfplumber)
- [Camelot](https://github.com/camelot-dev/camelot)
- [OCRmyPDF: componentes](https://ocrmypdf.readthedocs.io/en/latest/installation.html)