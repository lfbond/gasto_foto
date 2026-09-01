# Gasto na Foto

Aplicação web simples para registrar despesas a partir de uma foto de comprovante. O usuário seleciona ou fotografa um recibo, a imagem é enviada para uma inteligência artificial e os itens identificados aparecem na tela junto com o total acumulado.

> Projeto educacional construído com HTML, CSS e JavaScript puro.

## Funcionalidades

- Seleção de uma imagem pelo navegador ou captura de foto em dispositivos compatíveis.
- Leitura do comprovante usando o Puter AI.
- Identificação do estabelecimento, dos itens comprados e dos respectivos valores.
- Classificação visual da despesa por categoria:
  - 🛒 Mercado
  - 🚗 Transporte
  - 🍔 Comida
  - 💊 Saúde
  - 🎉 Lazer
  - 🏠 Casa
  - 💸 Outros
- Exibição de cada comprovante processado em uma lista.
- Soma dos totais das notas carregadas durante a sessão.
- Layout responsivo, adequado para uso em telas pequenas.

## Como funciona

O processamento acontece neste fluxo:

1. O usuário toca no campo **Toque para fotografar o comprovante**.
2. O navegador abre o seletor de arquivos ou a câmera do dispositivo.
3. O evento `change` chama a função `lerFoto()` em `scripts.js`.
4. A imagem e uma instrução de formatação são enviadas para `puter.ai.chat()`.
5. A resposta da IA é dividida em duas partes pelo caractere `|`:
   - descrição da compra;
   - total numérico da nota.
6. A descrição é adicionada à lista e o total é acumulado no resumo da página.

## Pré-requisitos

- Um navegador moderno com suporte a JavaScript, como Chrome, Edge, Firefox ou Safari.
- Conexão com a internet.
- Acesso ao serviço Puter, utilizado pela aplicação para a análise da imagem.
- Um comprovante legível, preferencialmente bem iluminado e sem cortes.

Não há dependências locais, processo de build ou servidor backend neste projeto.

## Executando localmente

### Opção 1: abrir diretamente

1. Baixe ou clone este repositório.
2. Abra o arquivo `index.html` no navegador.
3. Selecione uma foto de comprovante.

### Opção 2: usar um servidor local

Servir os arquivos localmente costuma oferecer um comportamento mais consistente para recursos do navegador:

```bash
python -m http.server 8000
```

Em seguida, acesse:

```text
http://localhost:8000
```

Também é possível usar a extensão Live Server do VS Code ou qualquer servidor HTTP estático.

## Estrutura do projeto

```text
.
├── index.html    # Estrutura da página e campo para selecionar a imagem
├── scripts.js    # Integração com a IA e cálculo do total
├── style.css     # Estilos, cores e layout responsivo
└── README.md     # Documentação do projeto
```

## Formato esperado da resposta da IA

A instrução enviada à IA pede uma resposta em uma única linha, com duas partes separadas por `|`:

```text
categoria e itens|total
```

Exemplo:

```text
🍔 <strong>Padaria Pão Quente</strong><br>Pão — R$ 5,00<br>Leite — R$ 4,50|9.50
```

O código usa a primeira parte para preencher o comprovante e converte a segunda com `Number()` para atualizar o total acumulado.

## Arquivos principais

### `index.html`

Define a interface inicial da aplicação:

- título e descrição;
- caixa de total gasto;
- campo de imagem com `accept="image/*"`;
- container `.lista`, onde os comprovantes são inseridos;
- carregamento do Puter.js e de `scripts.js`.

### `scripts.js`

Contém a lógica principal:

- `pedido`: instrução de formatação enviada à IA;
- `lerFoto()`: lê o arquivo selecionado e processa a resposta;
- `total`: variável mantida em memória para somar as notas da sessão.

### `style.css`

Controla a aparência da aplicação, incluindo o resumo em verde, o seletor de foto com borda tracejada, os cartões dos comprovantes e a largura máxima da página.

## Limitações atuais

- Os dados ficam apenas na memória da página e são perdidos ao recarregar ou fechar a aba.
- Não existe edição ou exclusão de um comprovante já adicionado.
- Não há tratamento visual para erros de rede, imagem ilegível ou resposta inválida da IA.
- A precisão depende da qualidade da foto e da interpretação do modelo.
- O código espera que a IA respeite exatamente o separador `|` e o formato solicitado.
- O conteúdo retornado pela IA é inserido com `innerHTML`; em uma versão de produção, a resposta deveria ser validada e sanitizada antes de ser exibida.
- O Puter.js é carregado por CDN, portanto a aplicação depende de um serviço externo.

## Possíveis melhorias

- Persistir despesas usando `localStorage`, IndexedDB ou uma API.
- Permitir editar, excluir e recategorizar lançamentos.
- Adicionar estados de carregamento e mensagens de erro.
- Validar a resposta da IA antes de adicionar o comprovante.
- Sanitizar o HTML recebido ou renderizar os dados como texto e elementos DOM seguros.
- Exibir data, hora e foto original de cada despesa.
- Adicionar filtros por categoria e período.
- Exportar os lançamentos para CSV ou PDF.
- Criar testes para o parser da resposta e para o cálculo do total.

## Tecnologias utilizadas

- HTML5
- CSS3
- JavaScript (ES6+)
- [Puter.js](https://js.puter.com/) para acesso ao Puter AI

## Licença

Licença Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.
