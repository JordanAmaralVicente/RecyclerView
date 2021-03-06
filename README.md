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

Na TextView que usaremos, colocamos o ID : ```android:id="@+id/fruta_item"``` para poder identificar um item. É importantíssimo declarar um ID, pois iremos precisar na última parte do código. 
***

## Últimos Passos ( A Parte Difícil :c ) 

Agora, estamos nos estágio final de fazer nossa recyclerView funcionar. Já definimos Todos os layouts e a classe principal da nossa aplicação. Agora Vamos definir a Classe ```FrutaAdapter.java``` :

![Adapter 1](https://github.com/JordanAmaralVicente/RecyclerView/blob/main/Imagens_Recycler/Adapter_1.JPG "Imagem Adapter 1")
![Adapter 2](https://github.com/JordanAmaralVicente/RecyclerView/blob/main/Imagens_Recycler/Adapter_2.JPG "Imagem Adapter 2")

o primeiro passo dessa parte é a declaração da classe FrutaAdapter
```Java
public class FrutaAdapter extends RecyclerView.Adapter<FrutaAdapter.ViewHolder>
```
Além do nome, temos que herdar ou extender a classe ```RecyclerView.Adapter<FrutaAdapter.ViewHolder> ``` . Extendemos essa classe como se ela fosse uma Array de FrutaAdapter.ViewHolder.

Sendo que ViewHolder é uma subclasse da classe que estamos criando no momento, então é possível que a IDE, novamente, aponte um erro, mas ao final do código estará tudo funcionando. 

abaixo da declaração temos os seguintes elementos:
```Java
private String[] frutasSet; //array que irá preencher a lista
public FrutaAdapter(String[] frutasSet) {
    this.frutasSet = frutasSet;
}
```
Aqui, criamos um atributo do objeto que será criado com o mesmo tipo que estamos recebendo por parâmetro. Se você estiver usando um array de objetos, no construtor da Classe você precisar modificar a classe String para o objeto que você deseja. E dentro do construtor, atribuímos ao atributo frutasSet o array de frutas que recebemos por parâmetro no construtor.

Logo Após a isso, declaramos uma subclasse
```Java
    public static class ViewHolder extends RecyclerView.ViewHolder {
        private final TextView textView; //o exemplo é composto apenas por um texto
        public ViewHolder(@NonNull View itemView) {
            super(itemView);

            textView = (TextView) itemView.findViewById(R.id.fruta_item);
        }
        public TextView getTextView() {
            return textView;
        }
    }
```
Essa subclasse vai aplicar o item_view em cada um dos elementos que temos no array. Nela, declaramos o campos que cada elemento terá, aqui temos somente texto então declaramos o atributo ` private final TextView textView` e criamos um getter para ele, chamado `getTextView` que retorna um TextView.
Se tivéssemos mais elementos, criamos um atributo e um getter para cada um deles tanto quanto for necessário. 

Dentro do construtor dessa subclasse, recebemos uma View como parâmetro, sendo o item_view que criamos e enviamos ela para a classe pai que irá gerenciar isso. Logo após, linkamos o objeto textView com a TextView do Layout através de seu ID `fruta item`.

Uma vez definida a subclasse, voltamos à classe pai e declaramos as seguintes funções herdadas da classe RecyclerView:

```Java
@NonNull
    @Override
    public FrutaAdapter.ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.item_view, parent, false);
        return new ViewHolder(view);
    }
```
Nesse método retornamos para a Classe RecyclerView o valor gerado pela FrutaAdapter.ViewHolder.
Para isso, declaramos primeiro uma nova View. Nessa parte, não há muito o que se mudar, exceto o layout do item_view que será usado, indicado por: `R.layout.item_view`.
Após isso, retornamos um objeto do tipo ViewHolder passando por parâmetro a View que criamos na linha de cima. 

Após isso, temos 
```Java
@Override
    public void onBindViewHolder(@NonNull FrutaAdapter.ViewHolder holder, int position) {
        holder.getTextView().setText(frutasSet[position]);
    }
```
Nesse método herdado, Recebemos um objeto do tipo ``FrutaAdapter.ViewHolder`` que é a classe que criamos e um Index para saber a posição atual do array. indicado por `int position`. E, assim, através do objeto `holder` , pegamos a textView declarada, mudamos o texto presente nela através do função `setText()` passando por parâmetro o Array de frutas e o conteúdo da posição que desejamos atribuir à textView. Ficando do seguinte modo ` holder.getTextView().setText(frutasSet[position]);`


Por fim, temos: 
```Java
@Override
    public int getItemCount() {
        return frutasSet.length;
    }
```
Que servirá de contador para a classe Pai da classe atual, de forma que será o tamanho total do array que estamos trabalhando. Nesse método apenas pegamos o tamanho do array através do atributo `length` presente no array. 

***

# Resultado Final

Com isso, temos o seguinte resultado do nosso tutorial:

![Resultado Final](https://github.com/JordanAmaralVicente/RecyclerView/blob/main/Imagens_Recycler/Resultado_Final.png "Imagem")



***

Participantes: [Guilherme Augusto](https://github.com/Guilhermeaug) & [Jordan Ítalo](https://github.com/JordanAmaralVicente)
