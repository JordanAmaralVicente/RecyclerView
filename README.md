# RecyclerView
Tutorial de como usar uma RecyclerView no desenvolvimento Android

***

### Configuração prévia do projeto 

Para fazer o uso de uma RecyclerView é necessário, primeiramente, que você já tenha criado seu projeto de desenvolvimento android e que ele esteja devidamente configurado. 

Uma vez configurado o projeto, não é necessário nenhuma instalação de biblioteca externa, pois a RecyclerView é um recurso nativo do android.
***

## Primeiros passos

1. O primeiro passo para o uso de uma RecyclerView é a adição da tag ```<androidx.recyclerview.widget.RecyclerView />``` na Activity em que você deseja usar essa funcionalidade.

Abaixo, há uma imagem de como deve ficar a tag:

!["Imagem da Main_Activity](https://github.com/JordanAmaralVicente/RecyclerView/blob/main/Imagens_Recycler/activity_main.JPG "XML activity_main")

Além das tags normais, como: ``` android:id ``` ou ``` android:width & android:height ``` , devemos colocar uma tag muito importante, indicada por ``` tools:listitem = "@layout:item_view" ```. Pode ser que a IDE aponte algum erro, pois não implementamos esse código ainda, porém deixe ele aí que voltaremos. Lembrando que não precisa ser necessariamente esse nome, usamos esse pois fizemos um projeto só para isso, mas quando o projeto for maior, é aconselhável que você coloque o nome de acordo com o que será exibido. 

## Alguns outros passos

2. Após definido o layout da tela aonde você usará o RecyclerView, é necessário que desenvolva o código que está ligado àquele layout. Como segue a imagem abaixo:

!["Imagem da Classe Main"](https://github.com/JordanAmaralVicente/RecyclerView/blob/main/Imagens_Recycler/Main_Activity.JPG "Classe Main Activity")

Acima é a implementação da Classe que controla a activity em que estamos usando a RecyclerView. Vamos separar ela em algumas partes para ficar de mais fácil compreensão.

A primeira parte dessa implementação é a declaração dos atributos dessas classe, sendo eles:
```Java
  RecyclerView mRecyclerView;
  private FrutaAdapter mAdapter;
```
Usaremos o atributo ``` mRecyclerView ``` para controlar o layout que declaramos no código anterior 
Já o atributo ``` mAdapter ``` da Classe ``` FrutaAdapter``` é o objeto de uma classe que vamos implementar logo em seguida, mas já vamos deixá-la declarada aqui para não termos que voltar nessa parte.


Avançando um pouco no código, temos o método padrão das activities aonde todas as coisas são controladas e será lá que faremos algumas declarações. Sendo esse método o 
```Java
protected void onCreate(Bundle savedInstanceState)
``` 
nele, por padrão, tem algumas coisas que não alteramos, sendo eles: as duas primeiras chamadas de funções declaradas na imagem do código.

Logo após, temos a seguinte declaração de lista:
```Java
  String[] frutas = {"Maça", "Melão", "Banana", "Acerola", "Uva", "Melancia", "Abacate", "Abacaxi", "Açai"};
```
Aqui temos um Array de Strings, mas poderia ser qualquer outra coisa ou até mesmo um array de Objetos de Uma classe que você pegou do banco de dados. Por exemplo, uma classe chamada usuário que contém: Nome, email e senha. E puxando esses dados do banco de dados, você colocou todos eles em um Array. Mas para fins didáticos, colocamos um array de string para ficar mais fácil a compreensão.

Uma vez feito isso, podemos partir direto para a manipulação da RecyclerView e com isso, temos o seguinte trecho de código:  

```Java
mRecyclerView = findViewById(R.id.recycler_view_layour_recycler); //referência do arquivo xml
mRecyclerView.setLayoutManager(new LinearLayoutManager(this));    //gerenciador de layout
mAdapter = new FrutaAdapter(frutas);                              //criando o Adapter
mRecyclerView.setAdapter(mAdapter);                               //atribuindo o adapter para o recyclerView
```

a primeira linha desse trecho de código relaciona o objeto da classe RecyclerView com o layout que definimos no arquivo de layout XML. É importante atentar-se que você deve passar por parâmetro o mesmo ID que você definiu no arquivo XML. Aqui, passamos por parâmetro o id: ``` recycler_view_layour_recycler ``` .

Logo após, definimos o layout manager, que será responsável pelo gerenciamento da recycler view. Fazemos isso, através do método ``` setLayoutManager ``` que é acessado através do próprio objeto que criamos anteriormente. A RecyclerView tem um layout manager de default, mas é aconselhável explicitar no código qual você deseja usar para evitar problemas futuros quando quiser alterar suas View. Aqui usamos o ```LinearLayoutManager``` passando por parâmetro o objeto ```this``` que está ligado ao ```mRecyclerView```.

Abaixo, instânciamos o objeto ``` mAdapter ``` passando por parâmetro nosso array ```frutas``` que definimos anteriormente. Vale lembrar de todas observações referentes ao array de string ou objetos. E uma vez instanciando o Adapter , podemos já definir o adapter da recyclerview com o seguinte código ``` mRecyclerView.setAdapter(mAdapter) ``` passando por parâmetro o Adapter que acabamos de instanciar. 

## Back to the XML

lembra de quando colocamos a tag ```tools:listitem = "@layout:item_view"``` ? 

Agora iremos criar o arquivo XML desse código:

![Item View](https://github.com/JordanAmaralVicente/RecyclerView/blob/main/Imagens_Recycler/item_view.JPG "Item_View XML CODE")

Aqui é a parte aonde você definirá como será o design de cada item que ficará na tela. Você pode usar sua criatividade para fazer como quiser, mas é necessário lembrar que você deve ter um elemento, para cada atributo que você quiser mostrar. Por exemplo: Aqui, no tutorial, Só vamos mostrar uma sequência de textos. Então, vamos colocar apenas uma TextView, pois precisamos somente disso. Então, você adequa seu código de acordo com sua necessidade

* PS: Aqui é feito o design de uma única célula da RecyclerView, por exemplo: só o design da celula que vai aparecer a String: "Maça" !

