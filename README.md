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

### StatefulWidget
  - Widget utilizado em situações em que parte da interface do usuário precisa ser atualizada dinâmicamente, exemplo: Ao clicar em um botão, +1 deve ser incrementado em uma variável e exibido na tela.

#### createState()
 - createState() é chamado uma vez durante a inicialização do widget.
 - Ele deve retornar uma nova instância de uma classe que estende State.
 - A instância da classe de estado fica associada a um único widget e é usada para armazenar e gerenciar o estado mutável desse widget.

#### Classe que implementa StatefulWidget
 - Responsável por definir a estrutura e configurações de armazenamento de estado.

#### Classe que implementa State
 - Responsável por manter o estado.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget{
  
  
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context){

    return MaterialApp(
      title:'AULA 2',
      home: Scaffold(
        appBar: AppBar(
          title: Text('StateFullWidget'),
        ),
        body: Teste(),
        
      )
    );
  }
}

class Teste extends StatefulWidget{
  const Teste({Key? key}) : super(key: key);

  @override
  _Teste createState() => _Teste();
}

class _Teste extends State<Teste>{
  int contador = 0;

  void _incrementador(){
    setState((){
      contador++;
    });
  }


  @override
  Widget build(BuildContext context){
    return Container(
      child: Column(
        children: [
          Text('contado: ${contador}'),
          ElevatedButton(
            onPressed: (){_incrementador();},
            child: Text('Clique em mim!'))
        ]
      )
    );
  }  
}
```
 

### Tipos de widgets

#### Container
 - Um Container é um agrupador de widgets, a exemplo de uma div.
 - O comportamento padrão de um container é ocupar todo espaço do seu componente pai, então em casos de Containers aninhados, pode ocorrer comportamentos não esperados, como sopreposição.

#### Column

#### Stack
 - O Widget Stack é uma alternativa ao Container. O Stack permite agrupamento de widgets e aninhamento de outras Stacks
 - O Stack sozinho não possui dimensāo e dessa forma não é possível definir uma cor de fundo.O Stack só possui dimensão se ele possuir um filho ou seja filho de outro widget, a exemplo de um Container.

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

#### Padding
 - Existe duas formas de usar o padding:Adicionando padding em um widget como um Stack e adicionando padding a um componente que possui vários widgets.

*Adicionando Padding a um Container*
```dart
Container(
  padding: EdgeInsets.all(8.0), // Adiciona padding de 8 pixels em todos os lados
  child: // Seu conteúdo aqui,
)

```
*Adicionando padding a um componente com vários widgets*
```dart
Padding(
  padding: EdgeInsets.all(8.0), // Adiciona padding de 8 pixels em todos os lados
  child: Row(
    children: [
      // Seus widgets da linha aqui
    ],
  ),
)

```

#### ListView
 - O ListView serve para criar uma coluna dinâmica de widgets e permite a rolagem da tela.

*Componente Tarefa*
```dart
class Tarefa extends StatelessWidget {
  
  final String nome;
  const Tarefa(this.nome, {Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(8.0),
      child: Container(
        child: Stack(
          children: [
          // O último container está sobreposto em cima do primeiro
            Container(
              color: Colors.blue,
              height: 140,
            ),
            Container(
              color: Colors.white30,
              height: 100,
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  Container(
                    color: Colors.black26,
                    width: 72,
                    height: 100,
                  ),
                  Text(nome),
                  ElevatedButton(
                    onPressed: () {},
                    child: const Icon(Icons.arrow_drop_up),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }   
}
```
```dart
lass MyApp extends StatelessWidget {
  const MyApp({Key? key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: Scaffold(
          appBar: AppBar(
            title: const Text('Minhas tarefas'),
          ),
          body: ListView(
            children: [
              Tarefa('Aprendendo Java'),
              Tarefa('Aprendendo Flutter'),
              Tarefa('Aprendendo Kotlin'),
              Tarefa('Aprendendo Kotlin'),
              Tarefa('Aprendendo Kotlin'),
              Tarefa('Aprendendo Kotlin'),
              Tarefa('Aprendendo Kotlin'),
              Tarefa('Aprendendo Kotlin'),
              Tarefa('Aprendendo Kotlin')
            ]
          ),
          floatingActionButton: FloatingActionButton(onPressed: () {})),
    );
  }
}
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
 <summary>Formulários</summary>

 ## Formulários

 ### Manipulando inputs

 #### TextFormField
 ##### Controller
  - A Classe TextEditingController permite controlar e manipular o texto no campo de entrada ```TextFormField``` e o Controller é a instância dessa classe.

###### Principais funcionalidades  do Controller
 - Recuperar o Texto Atual
```dart
TextEditingController nomeController = TextEditingController();
String valueInput = nomeController.text;

TextFormField(
  controller: nomeController
)
```
*Exemplo*
```dart
class Form extends StatefulWidget{

  @override
  _Form createState() => _Form(); 
}

class _Form extends State<Form>{
  TextEditingController nomeController = TextEditingController();

  @override
  Widget build(BuildContext context){

    return Container(
      child: Column(
        children: [
          TextFormField(
            controller: nomeController,
            decoration: InputDecoration(labelText: 'Digite algo'),
          ),
          TextButton(onPressed: (){print(nomeController.text);}, child: Text('Clique aqui'))
        ]
      )
    );

  }

}
```


 
 
</details>

### Iniciando um widget com valores dinâmicos
 - Vamos imaginar um componente que possui um widget stack filho e uma imagem como filha de stack.Vários componentes podem ser criados, mas as imagens deve ser diferente.Neste caso, sem usar a dinamicidade, todos os componentes possuíram a mesma imagem.

```dart
final String src_img
this.src_img
Image.network(src_img)
Componente(link)
```
 - Cada componente terá uma imagem diferente de forma dinâmica e não da forma hard code.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget{
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context){

    return MaterialApp(
      title: 'Flutter app',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Teste'),
        ),
        body:Column(
          children: [
            
            Componente('https://cdn.cloudflare.steamstatic.com/steam/apps/861650/header.jpg?t=1698396735'),
            Componente('https://www.promobit.com.br/blog/wp-content/uploads/2022/05/17183905/skate.jpg')
          ]
        )
        
          
      )

    );
  }
}

class Componente extends StatelessWidget{
  
  final String src_img;
  const Componente(this.src_img, {Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context){

    return Padding(
      padding:EdgeInsets.all(8.0),
      child: Container(
        color:Colors.grey,
        width: 400.0,
        height: 200.0,
          child: Stack(
            children:[
              Image.network(src_img),
            ]
          )
      )
    );
  }
    
}
```


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

### janela de diálogo 2

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Alerta Exemplo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Alerta Exemplo'),
        ),
        body: Center(
          child: Builder(
            builder: (BuildContext context) {
              return ElevatedButton(
                onPressed: () {
                  _exibirAlerta(context);
                },
                child: Text('Exiba o Alerta'),
              );
            },
          ),
        ),
      ),
    );
  }

  Future<void> _exibirAlerta(BuildContext context) async {
    return showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Alerta Acionado'),
          content: Text('Esta é a mensagem do alerta.'),
          actions: <Widget>[
            TextButton(
              onPressed: () {
                Navigator.of(context).pop();
              },
              child: Text('Fechar'),
            ),
          ],
        );
      },
    );
  }
}


```
 
</details>





</details>
