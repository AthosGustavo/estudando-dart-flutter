# Estudando Dart/Flutter

*Documento em constante edição!*

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
 <summary>Lógica de programação</summary>

 ## Lógica de programação
 
- Imprimir no console: print();
- String se escreve com S maíusculo
- O tipo de variavel ´dynamic´ não possui tipagem.

**Concatenação de String**
```dart
  'Nome: ${nome}'
```

- Increment de variáveis
 ```dart
  int numero = 1
  numero = numero + 1;
  numero += 1
 ```
- A primeira incrementação é igual a segunda.

**Sintaxe dos operadores**
 ```dart
  and -> &&
  or  -> ||
 ```

## Operadores null

**Operador nullable ??**
 - Operador usado para fornecer valores padrão para uma variável vazia

*EXEMPLO*
 ```dart    
 String nome;
 String nomeCompleto = nome ?? 'Convidado';
 print('Olá, $nomeCompleto');
```
     
**Operador ?**
 - Usado para lidar com possíveis valores nulos
   
 - 1 caso: Usando o operador após um tipo
   - `String? nome;`
   - `String?` indica que `nome` pode ser nulo`
   
 - 2 caso: Acesso condicional
   - Usado para acessar funções e atributos de uma classe que a intância pode ser possivelmente nula.
   - Se nome não for nulo, retorna o comprimento, caso contrário, retorna null
 ```dart
 String? nome;
 int comprimentoDoNome = nome?.length
 ```
 - 3 operador non-null !
   - Operador usado para confirmar que tal variável não será nula
   - `sintaxe: variavel!`

 <details>
  <summary>Future</summary>

  ## Método Future
  - Classe que representa um valor ou erro que estará disponível em aalgum momento no futuro
 
 ```dart
  Future<tipoDoResultado> nomeMetodo() async {
   variavel = await metodo();
  }
 ```
 
  - Situações em que Future é usado
    - Chamadas na api
    - leitura/gravacao de arquivos
 </details>
</details>

<details>
 <summary>Context</summary>
 
 ## Context
 - Os widgets sao organizados de forma hierarquica em uma arvore de widgets ,mas por si so, os widgets nao conhecem o seu grau de parentescos com outros widgets.
 - O metodo BuildContext serve exatamente para localizar,levar informacoes e informar grau de parentesco.
 - As informacoes de context so podem ser obtidas no fluxo de baixo para cima,ou seja, filho para pai.
 

 
 ### Exemplos práticos para entender o context

 *Build context - contexto de construcao*
 ----------------------------------------

 #### Exemplo 1: Acionando o snackbar por meio de um botão

- ScaffoldMessenger.of(context): Aqui, estamos usando o ScaffoldMessenger para acessar o Scaffold mais próximo na árvore de widgets.
O Scaffold é responsável por exibir elementos de interface do usuário, como barras de aplicativos, gavetas e, neste caso, o SnackBar.

- showSnackBar(SnackBar(...)): Ao chamar showSnackBar, estamos indicando ao Scaffold que exiba um SnackBar na parte inferior da tela.

- content: Text('Texto alterado!'): O conteúdo do SnackBar é definido como um texto informando que o texto foi alterado.

- context: O context é passado como argumento para ScaffoldMessenger.of para informar ao Flutter sobre a posição do widget na árvore de widgets.
O BuildContext é necessário para que o Flutter saiba onde exibir o SnackBar na hierarquia de widgets.
 
 ```dart
 import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Context'),
        ),
        body: Botao(),
      ),
    );
  }
}

class Botao extends StatefulWidget {
  @override
  _Botao createState() => _Botao();
}

class _Botao extends State<Botao> {
  @override
  Widget build(BuildContext context) {
    return Container(
        child: Stack(children: [
      ElevatedButton(
          onPressed: () {
            ScaffoldMessenger.of(context)
                .showSnackBar(SnackBar(content: Text('Texto alterado')));
          },
          child: Text('Clique aqui'))
    ]));
  }
}

 ```

#### Exemplo 2: Navegação de telas

- Neste exemplo, quando o onPressed é acionado no ElevatedButton, o context passado para Navigator.of(context).push
refere-se ao contexto do widget TelaA, que é o contexto em torno do botão que está sendo pressionado.

- Ao fornecer esse contexto, o Flutter sabe onde na árvore de widgets a ação de navegação está ocorrendo.

- Dentro do builder, uma nova instância da TelaB é criada. O BuildContext é passado como um parâmetro para essa função,
fornecendo informações sobre o contexto do widget no qual a navegação está ocorrendo. Isso é essencial porque permite
ao Flutter construir a TelaB de acordo com a hierarquia de widgets existente.

- Observe que em `Navigator.of(context).push` é ultilado o context para recuperar o contexto da TelaA criada com o metodo Widget build
e que após isso o metodo build é usado novamente na linha 29 para fornecer informacoes do widget TelaB



```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TelaA(),
    );
  }
}

class TelaA extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tela A'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Use o BuildContext para navegar para TelaB
            Navigator.of(context).push(
              MaterialPageRoute(
                builder: (BuildContext context) {
                  return TelaB();
                },
              ),
            );
          },
          child: Text('Ir para Tela B'),
        ),
      ),
    );
  }
}

class TelaB extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tela B'),
      ),
      body: Center(
        child: Text('Esta é a Tela B'),
      ),
    );
  }
}

```


 
</details>

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

 ##### Como usar o método onChanged

 *Utilizando onChanged para monitorar um input*

  - onChanged recebe em seu parâmetro o atributo text da classe TextEditingController e no seu escopo recebe o método setState para atualizar em especifico o valor de inputImgController.text.
 
 ```dart
 class CarregadorImg extends StatefulWidget{

  @override
  _CarregadorImg createState() => _CarregadorImg();
}

class _CarregadorImg extends State<CarregadorImg>{

  TextEditingController inputImgController = TextEditingController();
  //late String valueInputImg;
  
  @override
  Widget build(BuildContext context){
    return Container(
      child: Column(
        children: [
          TextFormField(
            controller: inputImgController,
            onChanged: (text){
              setState((){});
            },
            decoration: InputDecoration(
              labelText: 'Digite a URL da imagem.'),
              
          ),
          Container(
            height: 100,
            width: 100,
            child: inputImgController.text.isNotEmpty ? Image.network(
              inputImgController.text,
              fit: BoxFit.cover,
            ) : Container(),
          ),
          // TextButton(onPressed: (){}, child: Text('Clique aqui')),  
        ],
      )
    );
  }
}
```

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
##### validator
 - Fornece uma função de validação que verifica se o valor inserido no campo de texto é válido.
 - Deve retornar uma String com uma mensagem de erro se não foi válido e null se for válido.
 - O parâmetro value na função de validação contém o valor inserido no input.
 
#### Widget Form
 - Utilizado para agrupar e gerenciar widgets de entrada  de dados, de modo a facilitar a validação e o envio.

**GlobalKey**
 - A classe GlobalKey é uma chave global que pode ser usada para se comunicar com um objeto específico, independentemente de onde ele esteja na hierarquia de widgets.
 
**GlobalKey<State>**, subclasse de globalkey
 - Utilizada quando um widget possui um estado que você deseja acessar de fora do widget em que ele está.

**Validate**
 - O método validate percorre todos os validadores dos widgets de entrada dentro do Form e retorna true se todos os widgets são válidos.

**Validando um formulário com Autovalidate.onUserInteraction**
 - Determina se o formulário deve ser validado automaticamente à medida que os campos de entrada são alterados.
 - A validação ocorre automaticamente nos seguintes casos:
   - O usuário toca em um campo de texto.
   - O usuário digita algo no campo de texto.
   - O usuário sai do campo de texto.
  
```dart
class Formulario extends StatefulWidget {
  @override
  _Formulario createState() => _Formulario();
}

class _Formulario extends State<Formulario> {
  final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
  TextEditingController controllerInputNome1 = TextEditingController();
  TextEditingController controllerInputNome2 = TextEditingController();
  String msgInputEmpty = 'Por favor, insira o seu nome.';

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      autovalidateMode: AutovalidateMode.onUserInteraction,
      child: Column(
        children: [
          TextFormField(
            validator: (value) {
              if (value == null || value.isEmpty) {
                return msgInputEmpty;
              }
              return null;
            },
            decoration: InputDecoration(labelText: 'Digite o seu nome 1.'),
          ),
          TextFormField(
            validator: (value) {
              if (value == null || value.isEmpty) {
                return msgInputEmpty;
              }
              return null;
            },
            decoration: InputDecoration(labelText: 'Digite o seu nome 2.'),
          ),
          ElevatedButton(
            onPressed: () {
              if (_formKey.currentState!.validate()) {
                print('Dados salvos');
              }
            },
            child: Text('Salvar'),
          ),
        ],
      ),
    );
  }
}
```


```dart
Form(
  key: _formKey,
  child: Column(
    children: [
      // Adicione seus widgets de entrada aqui
      TextFormField(
       validator: (value) {
        if (value == null || value.isEmpty) {
         return 'Este campo não pode ficar em branco.';
        }
        return null;
      },
       // ... outras configurações do TextFormField
     ),

      // Outros widgets de entrada, botões, etc.
    ],
  ),
),

```
```dart
ElevatedButton(
  onPressed: () {
    if (_formKey.currentState!.validate()) {
      // Se a validação for bem-sucedida, faça algo, como enviar os dados.
      // Pode acessar os dados dos campos de texto por meio do controller ou
      // pelo método onSaved no TextFormField.
    }
  },
  child: Text('Enviar'),
),

```
```dart
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
 <summary>InkWell</summary>

 ## InkWell
  - Este widget tem o poder de transformar qualquer widget clicável e executar uma função.
 ```dart
  return Stack(
      
      alignment: Alignment.bottomCenter, children: [
      InkWell(
        onTap:(){
          Navigator.push(
            context,
            MaterialPageRoute(builder: (context) => DetailsScreen(nome: widget.nome, numero: widget.numero, endereco: widget.endereco, nomePet: widget.nomePet))
          );
        },
        child: Ink(
          height: 220,
          width: 280,
          padding:EdgeInsets.only(top: 8.0, right: 16.0, bottom: 8.0, left: 16.0),
          // /margin: EdgeInsets.all(8.0), // Adiciona uma margem externa
          decoration: BoxDecoration(
            color: Colors.blue, // Cor de fundo azul
            borderRadius: BorderRadius.circular(10.0), // Borda arredondada
          ),
          child: Column(
            crossAxisAlignment:
                CrossAxisAlignment.start, // Alinha o texto à esquerda
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(widget.nome),
              Text(widget.numero),
              Text(widget.endereco),
              Text(widget.nomePet),
            ],
          ),
        ),
      ),
    ]);
 ```
</details>


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

<details>
 <summary>Alinhamento e estilização de Widgets</summary>

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

```
padding: EdgeInserts
```
Métodos de EdgeInserts

 - ```all```: Espaçamento aplicado em todas as direções.
 - ```only```: Permite especificar diferentes valores para cada direção individualmente.
 - ```symmetric```: Permite especificar valores diferentes para os lados vertical e horizontal.
 - ```fromLTRB```: Permite especificar valores para as quatro direções diretamente.

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
Utilizando Border Radius
 - Adiciona o arredondamento em todas as bordas
  - ```borderRadius: BorderRadius.circular(10.0),```

## Alinhamento de widgets

#### crossAxisAlignment
 - Usado em widgets como Column e Row

*Usado em uma Column*
 - Controla a posição horizontal dos elementos filhos

*Usado em uma Row*
 - Controla a posiçao vertical dos elementos filhos

#### mainAxisAlignment
*Usado em uma Colunm*
 - controla a posição horizontal dos elementos filhos

*Usado em uma Row*
 - Controla a posição vertical dos elementos filhos

#### Alignment
 - Pode ser usado em qualquer widget que aceite um filho e geralmente é aplicado a widgets como Container, Stack 
 - Utilizado nos elementos filhos de Stack.
 - Permite posicionamento de ambos os eixos.
 - ´alignment: Alignment.´


</details>

<details>
 <summary>Método Navigate</summary>

 ## MaterialPageRoute
  - O MaterialPageRoute é uma classe em Flutter que representa uma rota que utiliza as transições do Material Design ao navegar entre telas.
 
 ## Explicando o context 
 
 - O context utilizado no trecho Navigator.push(context, ...) é o mesmo context passado para a função build(BuildContext context).
 - O primeiro parâmetro do Navigator.push é o context atual, indicando de onde a navegação está sendo iniciada.
 - O segundo parâmetro é uma instância de MaterialPageRoute. O construtor dessa classe aceita um argumento chamado builder, que é uma função que recebe o (context) e retorna o widget que deve ser construído para representar a nova rota.
 - o context passado para o MaterialPageRoute é um novo contexto criado com base no contexto e nas informações da próxima tela.Esse contexto é usado para garantir que o novo widget (FormScreen neste caso) seja construído com o contexto apropriado, herdados do contexto do widget pai (onde a navegação foi iniciada). Isso é essencial para manter a consistência e acesso correto aos recursos e configurações do ambiente.

```dart
class _InitialScreen extends State<InitialScreen>{

  @override
  Widget build(BuildContext context){
    
    return Scaffold(
      appBar: AppBar(
        title: Text('Registrar pet')
      ),
      body: ListView(),
      floatingActionButton: FloatingActionButton(
        onPressed: (){
          Navigator.push(
            context,
            MaterialPageRoute(builder: (context){
              return FormScreen();
            }
            
            )
          );
        },
        child: Icon(Icons.add),
      ),
      
    );
  }
}
```

## Sintaxe dos métodos

```dart
Navigator.push(contextoAtual, MaterialPageRoute)

MaterialPageRoute(builder: (novoContexto){return Widget})
```

# Navigate.pop
 - Volta para uma página anterior.

```
Navigator.pop(context, result)
```

## Parâmetros

**Context**
 - Contexto da tela atual

**result, parâmetro opcional**
 - Parâmetro usado para passar dados de volta para a rota anterior


## Recebimento de resultados
 - Após efetuar o método Navigate.pop() é necessário enviar valores para a tela anterior, a exemplo de uma atualização de lista após realizar um cadastro em um formulário.
 - Sendo assim, é possível encadear um método then ao Navigator.push que levou a tela atual e dentro do then, chamar o setState para atualizar estados.

```dart
Navigator.push(
            context,
            MaterialPageRoute(builder: (context){
                return FormScreen(formDataController); //estudar sobre a necessidade de passar a instancia de formDataController no parametro de FormScreen
              }
            
            )
          ).then((result){ //ESTUDAR SOBRE THEN
            //if (result != null && result is int){
              setState(() { //O método setState nao aceita parametros
                result.listaRegistros.length;
                
                // Mesmo que o escopo do setState esteja vazio, o Flutter
                // percebe a mudança de estado e reconstrói automaticamente
                // o widget. Isso resulta na reconstrução do ListView.builder,
                // que por sua vez atualiza a lista de registros na interface
                // do usuário.

              });
            //}
          });
```

 
 
</details>






