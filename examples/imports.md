## Importações

As importações são bastante utilizadas pois trazem diversos benefícios, como, por exemplo, o reaproveitamento de código e estruturação/separação dos arquivos de uma bastante flexível.

Cada equipe define as suas preferências e metodologias a serem utilizadas em seus projetos, sendo assim, manter os arquivos separados contribui para uma boa manutenção do código.

Ao utilizarmos o plugin [postcss-import](#plugins-utilizados) o PostCSS irá utilizar as regras do plugin ao utilizarmos o `@import` e não mais as regras nativas do CSS.

#### Exemplos

Declaração de variáveis em um arquivo específico para de variáveis
```sass
/* variables.css */

$colorPrimary = black;
$colorSecundary = #056ef0;
```

Utilização do @import e respectivamente das variáveis
```sass
/* main.css */
@import 'variables'

body {
  background-color $colorSecundary;
}

h1 {
  color $colorPrimary;
}

.button {
  border-radius 5px;
}
```

É possível fazer a importação utilizando o conceito de módulos do NodeJS com o nosso plugin. Podemos navegars pelos diretórios do projeto, e até mesmo no node_modules para importarmos um arquivo de estilos.

Vejamos uma possível solução que faz a separação dos arquivos de uma forma interessante, utilizando o conhecimento sobre imports.

#### Ruim
```sass
/* main.css */
$colorPrimary = black;
$colorSecundary = #056ef0;
$colorTertiary = #fff;
$buttonWidth = 100px;
$buttonPadding = 15px;

body {
  background-color $colorSecundary;
}

h1 {
  color $colorPrimary;
}

.button {
  border-radius 5px;
  width: $buttonWidth;
  padding: $buttonPadding;
  color: $colorPrimary;
  border: 2px solid $colorPrimary;
}
.button:hover {
  border: 2px solid $colorTertiary;
}
```

#### Bom

```sass
/* variables.css */
$colorPrimary = black;
$colorSecundary = #056ef0;
$colorTertiary = #fff;
$buttonWidth = 100px;
$buttonPadding = 15px;

/* buttons.css */
@import 'variables'

.button {
  border-radius 5px;
  width: $buttonWidth;
  padding: $buttonPadding;
  color: $colorPrimary;
  border: 2px solid $colorPrimary;
}
.button:hover {
  border: 2px solid $colorTertiary;
}

/* main.css */
@import 'buttons'

body {
  background-color $colorSecundary;
}

h1 {
  color $colorPrimary;
}
```

#### Plugins utilizados
Para este conceito, fizemos a utilização de um plugin conhecido como [postcss-import](https://github.com/postcss/postcss-import).

#### Qual o próximo passo?

Acessar o próximo artigo onde vamos entender como funcionam os [seletores aninhados](nested-selectors.md) do PostCSS.