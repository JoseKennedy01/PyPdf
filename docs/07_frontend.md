# Interface web — PyPdf

## Abordagem recomendada

Começar com templates HTML renderizados pelo Django, CSS e JavaScript pequeno. Não há necessidade inicial de SPA ou aplicação front-end separada.

Nomes próprios do projeto serão em português quando possível, como estilos/principal.css e scripts/conversor.js. Convenções necessárias do Django permanecem compatíveis.

## Páginas previstas

- Início com operações do MVP.
- Cadastro com e-mail e senha.
- Login e logout.
- Formulário PDF → PNG.
- Formulário PNG → PDF.
- Estado de processamento e link de download.
- Mensagens para formato, limite, senha e falha.

## Experiência de envio

- Mostrar formatos aceitos e limite 15 MB perto do campo.
- Uma operação por envio no MVP.
- Permitir trocar o arquivo antes de enviar.
- Validações no navegador servem para conveniência; o servidor sempre valida.
- Informar que PDF multipágina retorna ZIP.
- Não exibir documento de upload por URL pública.
- Indicador de progresso pode ser adicionado após o fluxo básico.

## Acessibilidade

Associar rótulos aos campos, suportar teclado, ligar erros aos campos e não usar só cor para indicar resultado. Planejar layout responsivo. Não declarar conformidade com padrão sem auditoria.

## Diretórios

- templates/: templates comuns.
- aplicacoes/contas/templates/contas/: páginas da conta.
- aplicacoes/conversoes/templates/conversoes/: páginas de conversão.
- static/estilos/: CSS.
- static/scripts/: JavaScript.

A estrutura será confirmada durante o scaffold respeitando o carregamento de templates e arquivos estáticos pelo Django.