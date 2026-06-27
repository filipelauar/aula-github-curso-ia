# 📱 Calculadora Interativa

## Visão Geral

Esta é uma **calculadora web moderna** construída com **HTML, CSS e JavaScript puro** (sem frameworks). A interface é responsiva, intuitiva e possui um design elegante com gradiente roxo, oferecendo operações matemáticas básicas e funções avançadas em um único arquivo HTML.

### Tecnologias
- **HTML5** — Estrutura semântica
- **CSS3** — Layout em Grid, animações, gradiente de fundo
- **JavaScript vanilla** — Lógica de cálculo sem dependências

---

## 🎨 Interface (Estrutura Visual)

### Layout
A calculadora usa **CSS Grid** com 5 colunas e várias linhas de botões, centralizada na tela com um fundo de gradiente roxo.

### Cores e Tipos de Botão

| Tipo | Cor | Uso |
|------|-----|-----|
| **Número** | Cinza claro (#ecf0f1) | Dígitos 0-9 e ponto decimal |
| **Operador** | Azul roxo (#667eea) | +, −, ×, ÷, % |
| **Função** | Laranja (#f39c12) | x², √, 1/x, +/−, ⌫ |
| **Igual** | Verde (#27ae60) | Executa o cálculo |
| **Limpar** | Vermelho (#e74c3c) | Reseta tudo |

### Display
- Fundo preto (#2d3436) com texto verde (#00ff00)
- Fonte monoespaçada para melhor legibilidade
- Quebra automaticamente números muito longos

---

## 🧠 Estado Interno (Variáveis JavaScript)

A calculadora funciona com **3 variáveis principais** que controlam todo o seu estado:

```javascript
let operacaoAtual = '';      // Número sendo digitado agora
let numeroAnterior = '';     // Primeiro número de uma operação
let operadorAtual = '';      // Operador escolhido (+, -, *, /, %)
```

### Como funcionam:

1. **`operacaoAtual`** — Acumula os dígitos digitados pelo usuário antes de escolher um operador
2. **`numeroAnterior`** — Armazena o primeiro operando quando um operador é clicado
3. **`operadorAtual`** — Guarda qual operador (+, -, *, /, %) foi selecionado

**Exemplo**: Digite "8", clique "+", digite "3", clique "=":
- Após digitar "8": `operacaoAtual = "8"`
- Após clicar "+": `numeroAnterior = "8"`, `operadorAtual = "+"`, `operacaoAtual = ""`
- Após digitar "3": `operacaoAtual = "3"`
- Após clicar "=": calcula e reseta

---

## 🔢 Operações Disponíveis

### Operações Básicas

| Botão | Símbolo | Função | Descrição |
|-------|---------|--------|-----------|
| + | + | Soma | Adiciona dois números |
| − | − | Subtração | Subtrai o segundo do primeiro |
| × | × | Multiplicação | Multiplica dois números |
| ÷ | ÷ | Divisão | Divide o primeiro pelo segundo* |
| % | % | Módulo | Resto da divisão |

*Se divisor for 0, exibe "Erro"

### Operações de Função

| Botão | Símbolo | Função JavaScript | Descrição |
|-------|---------|-----------------|-----------|
| x² | x² | `potencia()` | Eleva número ao quadrado |
| √ | √ | `raizQuadrada()` | Calcula raiz quadrada* |
| 1/x | 1/x | `inverso()` | Calcula o inverso (1/número)** |
| +/− | +/− | `mudarSinal()` | Inverte sinal (positivo ↔ negativo) |

*Rejeita números negativos com alerta
**Rejeita zero com alerta (evita divisão por zero)

### Controle

| Botão | Função | Descrição |
|-------|--------|-----------|
| C | `limpar()` | Reseta tudo para 0 |
| ⌫ | `apagarUltimo()` | Remove o último dígito |
| . | `numero('.')` | Adiciona vírgula decimal* |
| = | `calcular()` | Executa a operação |

*Não permite duas vírgulas no mesmo número

---

## 📊 Fluxo de Uso — Exemplo Prático

Vamos calcular **8 + 3 = 11**:

1. **Clica "8"**
   - Função `numero('8')` é chamada
   - `operacaoAtual = "8"`
   - Display mostra: **8**

2. **Clica "+"**
   - Função `operador('+')` é chamada
   - `numeroAnterior = "8"` (copia `operacaoAtual`)
   - `operadorAtual = "+"`
   - `operacaoAtual = ""` (limpa para digitar próximo número)
   - Display mostra: **8** (mantém)

3. **Clica "3"**
   - Função `numero('3')` é chamada
   - `operacaoAtual = "3"`
   - Display mostra: **3**

4. **Clica "="**
   - Função `calcular()` é chamada
   - Converte: `num1 = 8`, `num2 = 3`
   - Executa: `8 + 3 = 11`
   - `operacaoAtual = "11"` (resultado)
   - `numeroAnterior = ""`, `operadorAtual = ""` (reseta)
   - Display mostra: **11**

---

## ⚠️ Tratamento de Erros

A calculadora protege contra operações inválidas:

| Situação | Comportamento |
|----------|--------------|
| **Raiz de número negativo** | Alerta: "Não é possível calcular raiz quadrada de número negativo" |
| **Divisão por zero** | Exibe "Erro" no display |
| **Inverso de zero (1/0)** | Alerta: "Não é possível dividir por zero" |
| **Duas vírgulas** | Ignora a segunda vírgula (função `numero()` valida) |

---

## 🔧 Estrutura do Código — Funções Principais

### Entrada de Dados
```javascript
function numero(n)              // Adiciona dígito ou vírgula
function operador(op)           // Seleciona operador básico
```

### Cálculo
```javascript
function calcular()             // Executa operação e mostra resultado
```

### Operações Especiais (1 número)
```javascript
function potencia()             // x²
function raizQuadrada()         // √
function inverso()              // 1/x
function mudarSinal()           // +/−
```

### Controle
```javascript
function apagarUltimo()         // Remove último dígito (⌫)
function limpar()               // Reseta tudo para 0 (C)
function atualizarDisplay()     // Renderiza valor na tela
```

---

## 💡 Detalhes Técnicos

### Operador Switch
A função `calcular()` usa um `switch` para determinar qual operação executar:

```javascript
switch (operadorAtual) {
  case '+': resultado = num1 + num2; break;
  case '-': resultado = num1 - num2; break;
  case '*': resultado = num1 * num2; break;
  case '/': resultado = num2 !== 0 ? num1 / num2 : 'Erro'; break;
  case '%': resultado = num1 % num2; break;
}
```

### Validações
- **`numero()`**: Impede segunda vírgula verificando `operacaoAtual.includes('.')`
- **`operador()`**: Só funciona se há algo digitado (`operacaoAtual !== ''`)
- **`calcular()`**: Só executa se há operador e segundo número (`operadorAtual !== '' && operacaoAtual !== ''`)

### Cadeias de Operação
Se você digita **8 + 3 +** (sem pressionar "="), a calculadora:
1. Detecta que há `numeroAnterior` e `operadorAtual` já definidos
2. Executa o cálculo anterior (8 + 3 = 11)
3. Armazena 11 como novo `numeroAnterior`
4. Aguarda o próximo número

---

## 🚀 Como Usar

1. **Abra o arquivo** `calculadora.html` em qualquer navegador
2. **Clique nos números** para digitar
3. **Escolha uma operação** (+, −, ×, ÷, %)
4. **Clique "="** para ver o resultado
5. **Use funções especiais** como x², √, +/− conforme necessário

### Atalhos Úteis
- **C**: Limpa tudo e volta ao estado inicial
- **⌫**: Remove o último dígito
- **+/−**: Muda o sinal do número (positivo ↔ negativo)

---

## 📝 Resumo

| Aspecto | Descrição |
|--------|-----------|
| **Arquivo** | `calculadora.html` |
| **Tecnologia** | HTML5 + CSS3 + JavaScript puro |
| **Operações** | 5 básicas + 4 avançadas + 3 controles |
| **Estado** | 3 variáveis (operacaoAtual, numeroAnterior, operadorAtual) |
| **Segurança** | Valida divisão por zero, raiz negativa e dupla vírgula |
| **Interface** | Grid 5x4, gradiente roxo, cores por tipo de botão |

