## 1. Finalidade

Este documento registra o que o PyPdf deverá fazer no MVP e quais condições deverá respeitar. Os requisitos servirão como referência durante o desenvolvimento e permitirão criar testes que verifiquem o comportamento esperado.

Os requisitos descrevem funcionalidades planejadas. Eles não significam que elas já estejam implementadas.

## 2. Requisitos funcionais

### RF-01 — Cadastro

A aplicação deverá permitir que uma pessoa crie uma conta antes de utilizar as conversões.

No MVP, o cadastro solicitará apenas e-mail e senha. Regras detalhadas de validação, confirmação de e-mail e recuperação de senha poderão ser definidas em versões futuras.

### RF-02 — Login

A aplicação deverá permitir que uma pessoa cadastrada entre na própria conta usando e-mail e senha para acessar as funcionalidades do MVP.

### RF-03 — Restringir conversões a usuários autenticados

A aplicação deverá exigir login antes de aceitar arquivos para conversão. Uma pessoa sem sessão autenticada não deverá iniciar uma conversão.

### RF-04 — Converter PDF para PNG

A aplicação deverá aceitar um PDF válido dentro do limite de tamanho e produzir uma imagem PNG por página.

Quando o PDF tiver mais de uma página, as imagens deverão ser disponibilizadas em um arquivo ZIP. Para um PDF de uma página, o resultado deverá ser uma imagem PNG.

### RF-05 — Converter PNG para PDF

A aplicação deverá aceitar uma imagem PNG válida dentro do limite de tamanho e produzir um PDF de uma página contendo essa imagem.

O suporte a várias imagens em uma única conversão e a ordenação dessas imagens ainda não fazem parte do requisito aprovado.

### RF-06 — Aplicar limite de tamanho

Cada arquivo enviado deverá respeitar o limite inicial de 15 MB. Arquivos maiores deverão ser recusados com uma mensagem clara.

### RF-07 — Recusar PDF protegido por senha

No MVP, PDFs protegidos por senha deverão ser recusados. A aplicação deverá explicar que o arquivo não pode ser processado nessa etapa.

Bloquear um PDF com senha e remover a senha de um PDF são funcionalidades futuras, ainda não implementadas.

### RF-08 — Informar erros de entrada e processamento

A aplicação deverá informar quando não puder processar um arquivo por estar vazio, corrompido, em formato incompatível ou quando ocorrer uma falha durante a conversão.

A mensagem não deverá apresentar dados técnicos sensíveis nem expor detalhes internos do servidor.

### RF-09 — Disponibilizar o resultado

Após uma conversão concluída, a aplicação deverá permitir que o usuário baixe o resultado correspondente: PNG, ZIP de imagens ou PDF, conforme a operação.

A forma e o prazo de armazenamento dos arquivos ainda serão definidos na meta de segurança e gerenciamento de arquivos.

## 3. Requisitos não funcionais

### RNF-01 — Custo

O serviço deverá ser gratuito para os usuários. As ferramentas e dependências escolhidas deverão ser gratuitas para o projeto e, preferencialmente, de código aberto.

Custos de hospedagem e operação ainda precisam ser avaliados.

### RNF-02 — Segurança de arquivos

O back-end deverá validar arquivos enviados e aplicar medidas contra conteúdo inválido, nomes maliciosos e consumo excessivo de recursos. Os controles específicos serão detalhados na documentação de segurança.

### RNF-03 — Limite de recursos

O sistema deverá aplicar o limite de 15 MB e, após avaliação técnica, definir limites adicionais de processamento, como páginas e tempo máximo.

### RNF-04 — Clareza de uso

A interface deverá explicar os formatos aceitos, o limite de tamanho, o resultado esperado e os motivos comuns de recusa.

### RNF-05 — Compatibilidade das ferramentas

As bibliotecas escolhidas deverão funcionar com Python e Django no ambiente planejado e ter licenças compatíveis com o projeto.

## 4. Entradas e saídas do MVP

| Operação | Entrada | Saída |
|---|---|---|
| PDF para PNG | Um PDF válido, de até 15 MB e sem senha | Uma imagem PNG por página; ZIP quando houver várias páginas |
| PNG para PDF | Uma imagem PNG válida, de até 15 MB | Um PDF de uma página |

## 5. Situações que devem ser tratadas

| Situação | Comportamento esperado |
|---|---|
| Pessoa não autenticada | Solicitar login antes de aceitar o arquivo |
| Arquivo acima de 15 MB | Recusar e informar o limite |
| Arquivo vazio | Recusar e informar que não há conteúdo para converter |
| Arquivo com extensão que não corresponde ao conteúdo | Recusar após validação do formato real |
| Arquivo corrompido ou inválido | Informar que não foi possível processá-lo |
| PDF protegido por senha | Recusar no MVP e explicar a limitação |
| Falha durante a conversão | Informar que a operação falhou sem expor detalhes internos |
| PDF de várias páginas | Gerar uma imagem por página e disponibilizá-las em ZIP |
| PDF de uma página | Disponibilizar uma imagem PNG |
| PNG válido | Gerar e disponibilizar um PDF de uma página |

## 6. Critérios de aceitação

O MVP poderá ser considerado funcional quando os testes futuros confirmarem que:

1. Uma pessoa pode se cadastrar com e-mail e senha e entrar na própria conta.
2. Uma pessoa sem login não consegue iniciar uma conversão.
3. Um PDF válido dentro do limite produz uma imagem por página.
4. Um PDF de várias páginas resulta em ZIP contendo todas as imagens geradas.
5. Um PDF de uma página resulta em um PNG para download.
6. Um PNG válido produz um PDF de uma página.
7. Arquivos acima do limite são recusados com uma mensagem clara.
8. Arquivos vazios, inválidos ou corrompidos não geram um resultado apresentado como válido.
9. Um PDF protegido por senha é recusado no MVP.
10. Uma falha de conversão não expõe informações internas do servidor.

## 7. Relação com testes futuros

Cada requisito funcional deverá ter testes que verifiquem seu caminho válido e seus casos de erro. Por exemplo, a conversão PDF para PNG deverá ser verificada com arquivos de uma e várias páginas, enquanto a validação deverá ser verificada com arquivos grandes, vazios, inválidos e protegidos.

Os testes serão definidos e implementados quando houver código para testar. Este documento não afirma que os testes já existem ou foram executados.

## 8. Fora do MVP

Não fazem parte do MVP:

- PDF ↔ Word.
- PDF ↔ Excel.
- OCR.
- Bloquear ou desbloquear PDFs.
- Conversão de várias imagens PNG para um PDF.
- Armazenamento permanente de documentos.

Esses itens poderão ser avaliados em etapas futuras.