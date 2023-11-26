# Estudando Dart/Flutter

## Widget
 - Um widget pode ser interpretado como as tags html que exibem algum tipo de conteúdo ou agrupam conteúdos,exemplo: textos, botoẽs, divs, imagem e etc.

### Tipos de widgets

#### Container
 - Um Container é um agrupador de widgets, a exemplo de uma div.
 - O comportamento padrão de um container é ocupar todo espaço do seu componente pai, então em casos de Containers aninhados, pode ocorrer comportamentos não esperados, como sopreposição.

#### Stack
 - O Widget Stack é uma alternativa ao Container. O Stack permite agrupamento de widgets e aninhamento de outras Stacks

#### Exemplo de estilização de Container
```dart

 Container(
  width: 200.0,
  height: 100.0,
  color: Colors.blue,
  alignment: Alignment.center,
  margin: EdgeInsets.all(16.0),
  padding: EdgeInsets.symmetric(horizontal: 8.0, vertical: 12.0),
  child: Text(
    'Olá, Mundo!',
    style: TextStyle(color: Colors.white),
  ),
)

```
#### Exemplo de estilização de um widget Text
```dart
Text(
  'Olá, Mundo!',
  style: TextStyle(
    fontSize: 20.0,
    fontWeight: FontWeight.bold,
    color: Colors.blue,
  ),
  textAlign: TextAlign.center,
)
```

#### Scaffold, material design
 - Scaffold é um widget que fornece uma estrutura visual básica para um aplicativo móvel. Ele serve como um "esqueleto" para o layout da sua interface do usuário.
 
##### Elementos que Scaffold disponibiliza

###### AppBar
 - É a barra superior que geralmente contém o título do aplicativo e possivelmente ações, como botões de navegação ou de ação.
 
##### Body
 - É a área principal do conteúdo da tela. Pode conter qualquer widget, como listas, colunas, linhas, etc. É definida usando a propriedade body.
 
##### home
 - Define qual será a tela inicial do aplicativo
 - home serve para indicar que a tela inicial será definida por Scaffold
