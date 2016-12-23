## Seletores Aninhados

Este conceito apresenta como aninhar uma regra de estilo dentro de outra, com o seletor da regra filho relativo ao seletor da regra pai.  
Além de aumentar a modularidade e a capacidade de manutenção dos nossos arquivos de estilo, esse recurso permite que estilos relacionados sejam agregados em uma única estrutura dentro de um arquivo CSS, melhorando a legibilidade e a facilidade de manutenção.

A W3C tem uma especificação própria de como utilizar o nested [CSS Nesting Module Level 3](https://tabatkins.github.io/specs/css-nesting/), e há um plugin conhecido [CSS Nesting](https://github.com/jonathantneal/postcss-nesting) para PostCSS que segue essa especificação. Todavia utilizaremos o plugin conhecido como [PostCSS Nested](#plugins-utilizados) que segue as regras do Sass.

#### Exemplos

Declaração de um bloco com seletores aninhados
```sass
.nav {
  background: black;
  
  &__list {
    background: red;
  
    &__item {
      background: white;
    }
  }
  
  &__link {
    background: blue;

    &--active {
      background: green;
    }
  }
}
```

Após processado, teremos o seguinte resultado
```sass
.nav {
  background: black;
}

.nav__list {
  background: red;
}

.nav__list__item {
  background: white;
}

.nav__link {
  background: blue;
}

.nav__link--active {
  background: green;
}
```

É possível fazer diversas combinações capazes de trazerem diversos benefício, mas é claro que há alguns problemas.  
Para conhecer um pouco mais sobre o que pode ser feito utilizando o [PostCSS Nested](#plugins-utilizados), leia a documentação oficial.

Vejamos uma possível solução para otimizar o código aninhado abaixo, utilizando o conhecimento sobre Nested.

#### Ruim
```sass
.form {
  background-color: #ddd;
}

.form .button, .form .input {
  width: 50%;
  display: block;
}

.button {
  background-color: #06f;
  color: #fff;
  font-size: 1.000em;
  font-weight: 500;
}

.input {
  border: 1px solid #fff;
  color: #000;
  font-weight: 500;
}

.button:hover, .input:hover {
  opacity: .75;
}
```

#### Bom

```sass
.form {
  background-color: #ddd;

  & .button,
  & .input {
    width: 50%;
    display: block;
  }
}

.button {
  background-color: #06f;
  color: #fff;
  font-size: 1.000em;
  font-weight: 500;

  &:hover {
    opacity: .75;
  }
}

.input {
  border: 1px solid #fff;
  color: #000;
  font-weight: 500;

  &:hover {
    opacity: .75;
  }
}
```

#### Plugins utilizados
Para este conceito, fizemos a utilização de um plugin conhecido como [PostCSS Nested](https://github.com/postcss/postcss-nested).