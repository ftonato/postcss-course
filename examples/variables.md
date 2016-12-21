## Variáveis

Variáveis servem para armazenar valores, que muitas vezes se repetem.  
Com a utilização de variáveis, podemos reaproveitar o código e prover uma fácil manutenção.

Você pode usar variáveis ​​dentro de valores, seletores e parâmetros da regra.

Vejamos uma possível solução que faz a otimização do seguinte trecho de código, utilizando o conhecimento sobre variáveis.

#### Ruim
```scss
.nav {
  width: calc(6 * 120px); /* 6 é o número de nav-item na tela. 120px é a largura de cada item. */
  border-bottom: 1px solid #056ef0; 
}

.nav-item {
  color: black;
  padding-top: 30px; /* o padding é a largura do item / 4; */
  transition: color .3s ease-in-out; 
}

.nav-item:hover {
 color: #056ef0;
}

```

#### Bom

```scss
$navItem: 120px;
$colorBlack: black;
$colorBlue: #056ef0;

nav {
  width: calc(6 * $navItem);
  border-bottom: 1px solid $colorBlue;
}

.nav-item {
  color: $colorBlack;
  padding-top: calc($navItem / 4);
  transition: color .3s ease-in-out; 
}

.nav-item:hover {
 color: $colorBlue;
}
```
