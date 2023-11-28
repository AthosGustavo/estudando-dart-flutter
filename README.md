# Estudando Dart/Flutter

<details>
 <summary>Lógica de programação</summary>

 <details>
  <summary>Future</summary>

  O método Future é utilizado para realizar operações assíncronas
  
  ```
  Future<TipoRetorno> nomeFuncao(Tipo parametro parametero) async {
   
   return someValue;  // ou throw SomeException;
  }

  ```
  
 </details>
</details>

Material Design
 - biblioteca com componentes estilizados criado pela google
Cupertino Design
 - biblioteca com componentes estilizados para apple

## Método build
 - No Flutter, a construção da interface do usuário é realizada através do método build de widgets.
 - Método usado em situações onde ocorre dinamicidade e alterações na tela,a exemplo de um atualizador e reconstrutor de estados e widget em situações onde alguma informação na tela é mudada por meio de uma interação.Por outro lado, o  método também é usado em situações estáticas.

## Flutter inspector
 - serve para visualizar a arvore de widgets e o tamanho dos widgets
 - widgets que nao possuem limite de altura ou largura,podem resultar em overflow

<details>
 <summary>Widget</summary>

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

##### AppBar
 - É a barra superior que geralmente contém o título do aplicativo e possivelmente ações, como botões de navegação ou de ação.
 
##### Body
 - É a área principal do conteúdo da tela. Pode conter qualquer widget, como listas, colunas, linhas, etc. É definida usando a propriedade body.
 
##### home
 - Define qual será a tela inicial do aplicativo
 - home serve para indicar que a tela inicial será definida por Scaffold

<details>
 <summary>Janela de diálogo</summary>

 Função anônima com parâmetros nomeados
  - Função com parãmetros e valores atribuídos no próprio parâmetro da função.

 *Exemplo: vamos supor que uma função aceite 3 valores em seu parâmetro*
 ```dart
 static carro({
   String nome = 'gol',
   String marca = 'Wolksvagem',
   String cor = 'prata'
 })
 ```
 
 ```dart
 static showDialogWithMessage({
    String? message,
    bool autoHide = true,
    int durationSeconds = 4,
    bool dismissible = true,
  }) async {
    final Widget widget = Center(
      child: Container(
        padding: EdgeInsets.all(16.0),
        width: 300,
        decoration: BoxDecoration(
          color: Colors.grey[800],
          borderRadius: BorderRadius.circular(8.0)
        ),
        child: Text(
          message ?? "Ocorreu um erro. Tente novamente.",
          style: TextStyle(
            color: Colors.white,
            fontSize: 12.0, // Alterado para fonte de tamanho 12
            decoration: TextDecoration.none, // Removido sublinhado
          ),
        ),
      ),
    );

    showDialogDefault(
      widget: widget,
      autoHide: autoHide,
      durationMilli: durationSeconds * 1000,
      dismissible: dismissible,
    );
  }
 ```

showDialog
  showDialogDefault
    showDialogWithMessage
 
</details>





</details>
