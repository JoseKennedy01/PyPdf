## 1. Propósito

O PyPdf será uma aplicação web para conversão de documentos. O produto deverá oferecer uma experiência simples para enviar um arquivo, convertê-lo e baixar o resultado.

O desenvolvimento será feito com Python e Django no back-end e HTML, CSS e JavaScript no front-end.

## 2. Usuários esperados

A aplicação é destinada a pessoas que precisam converter documentos, como estudantes e usuários domésticos ou profissionais.

O uso exigirá cadastro e login. Não haverá conversão anônima no MVP.

No MVP, o cadastro exigirá apenas e-mail e senha. A confirmação de e-mail e a recuperação de senha ainda serão avaliadas para versões futuras.

## 3. Objetivos

- Oferecer conversões úteis em uma aplicação web.
- Começar com um conjunto pequeno de funcionalidades e ampliá-lo em etapas.
- Utilizar ferramentas gratuitas para o projeto e, preferencialmente, de código aberto.
- Tratar arquivos enviados com cuidado e limitar o consumo de recursos.
- Documentar as limitações das conversões para não prometer fidelidade que as ferramentas não garantem.

## 4. Escopo do MVP

O MVP deverá incluir:

- Cadastro e login obrigatórios.
- Conversão de PDF para PNG.
- Conversão de PNG para PDF.
- Limite de 15 MB por arquivo enviado.
- Uma imagem PNG independente para cada página do PDF.
- Download em ZIP quando um PDF com várias páginas gerar várias imagens.
- Recusa inicial de PDFs protegidos por senha.
- Mensagens compreensíveis quando o arquivo for inválido ou a conversão falhar.

## 5. Escopo futuro

Estão no escopo futuro, mas não fazem parte do MVP:

- Conversões entre PDF e Word (`.docx`).
- Conversões entre PDF e Excel (`.xlsx`).
- OCR para PDFs digitalizados.
- Bloqueio e desbloqueio de PDFs com senha.
- Outras funções de gerenciamento e conversão de documentos que venham a ser aprovadas.

PDF para Word será tratado como uma conversão de melhor esforço. Não será prometida reprodução perfeita do layout.

## 6. Limitações conhecidas

- PDFs danificados, vazios, protegidos por senha ou incompatíveis poderão ser recusados.
- A qualidade de conversão dependerá do arquivo de origem e das ferramentas selecionadas.
- O limite de 15 MB não garante que todos os documentos dentro desse tamanho possam ser processados: limites adicionais de páginas, tempo e recursos serão definidos após a avaliação técnica e de segurança.
- A política de retenção e exclusão dos arquivos ainda será definida.

## 7. Decisões ainda pendentes

- Quais dados serão solicitados no cadastro.
- Se haverá confirmação de e-mail e recuperação de senha no MVP.
- Se a conversão de várias imagens PNG em um único PDF fará parte do MVP.
- Por quanto tempo os arquivos convertidos ficarão disponíveis.
- Quais limites de páginas e tempo serão aplicados.
- Quais tecnologias de conversão serão escolhidas.

## 8. Estado do produto

Este documento descreve o produto planejado. Cadastro, login, conversões e OCR ainda não foram implementados.