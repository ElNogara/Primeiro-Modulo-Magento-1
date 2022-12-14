<h1>Primeiro Módulo Magento 1</h1>
Aprendendo a criar seu primeiro módulo magento 1 e a criar uma rota para um controller na plataforma. <br>


<h2>O que é preciso ter em mente na hora de criar o primeiro módulo Magento 1?</h2>
O seu módulo precisa seguir a estrutura padrão do Magento, ou seja, todo módulo desenvolvido deve estar dentro de app/code/<strong>CODEPOOL</strong>/<strong>NAMESPACE</strong>/<strong>MODULENAME</strong></br></br>

_CODEPOOL_ -> Pode variar entre 'local', 'community' e 'core'... Um resumão sobre isso, se usa o local quando seu módulo está sendo desenvolvido especificamente para uma funcionalidade de uma loja, o community é utilizado quando as funções do seu módulo são mais genéricas ou seja, pode auxiliar ou melhorar a utilização de várias lojas e o core é utilizado pela plataforma para armazenar todos os módulos padrões dela então não é recomendado realizar nenhuma alteração nessa codepool.</br>
_NAMESPACE_ -> É geralmente o nome da empresa/fabricante ou desenvolvedor que está criando o módulo.</br>
_MODULENAME_ -> É o nome do módulo, geralmente tentem utilizar um nome mais curto e que tenha referência com as funções que vai realizar. (Isso facilita sua vida no desenvolvimento dele)</br>

A pasta etc do módulo é responsável pelas configurações dele, como quais arquivos vão ser utilizados, rotas que serão criadas, dependências de outros módulos, campos que serão criados no admin da plataforma e por ai vai... Dentro do etc é obrigatório que seu módulo tenha o arquivo config.xml que é a onde você vai apontar esses campos utilizados. Abaixo um exemplo comentado:

```
<?xml version="1.0"?>
<config>
    <modules>
        <Elnogara_FirstModule> <!--Nessa linha é importante reparar que eu inseri o namepace e o moduleName da mesma forma que eu criei as pastas, é MUITO importante que isso seja feito dessa forma, caso contrário o Magento não vai conseguir localizar o seu módulo Obs: a primeira letra sempre precisa ser maiuscula-->
            <version>1.0.0</version> <!--Aqui é passado a versão do seu módulo, é muito utilizado quando vamos realizar alguma alteração no banco de dados da plataforma, pois o Magento identifica que a versão foi atualizada e recria ou executa as query's apontadas.-->
        </Elnogara_FirstModule>
    </modules>
</config>
```

Acima é uma estrutura padrão de um config.xml, mas como no nosso módulo vai utilizar um controller será necessário declarar uma rota no nosso config. Então abaixo tem um exemplo com a rota sendo declarada.

```
<?xml version="1.0"?>
<config>
    <modules>
        <Elnogara_FirstModule>
            <version>1.0.0</version>
        </Elnogara_FirstModule>
    </modules> <!--Note que dessa vez possui campos a mais, sendo eles responsáveis por declarar a rota do controller-->
    <frontend> <!--Aqui nós dissemos em que parte da plataforma estaremos criando algo, OU será no frontend que é responsável por desenvolver uma função para o frontend da sua loja OU será adminhtml que é responsável por desenvolver uma função para o admin da plataforma-->
        <routers> <!--Aqui estamos dizendo que será criado uma rota para nossa plataforma -->
            <nogara> <!--Aqui nós criamos um nó único, será um apelido para a sua nova rota-->
                <use>standard</use> <!--Esse campo basicamente diz qual é o tipo de rota que será criado, isso vou estar tratando em outro tutorial, pois não é foco nesse momento, apenas tenham em mente que em quase todas as rotas criadas o standard será usado, muito raramente vai estar utilizando outro parâmetro aqui-->
                <args> <!--Esse nó é responsável por passar argumentos para a sua rota, abaixo passei dois que são os mais importantes no meu ver, mas existem muitos outros que podem ser passados-->
                    <module>Elnogara_FirstModule</module> <!--Um dos argumentos passados é qual módulo que vai utilizar essa rota-->
                    <frontName>firstmodule</frontName> <!--E o outro argumento passado foi o frontName dessa rota, quando for ser acessada essa rota, qual frontName que vai ser chamado no caminho de url-->
                </args>
            </nogara>
        </routers>
    </frontend>
</config>
```

Além de declarar o controller dentro do nosso config também é importante criarmos o mesmo, então com isso em mente dentro da pasta principal do módulo(MODULENAME) vamos criar a pasta _controllers_ que é a pasta responsável por armazenar todos os controllers do módulo e será aonde vamos criar o nosso _TestController.php_ que é o nosso controller. Abaixo um exemplo do controller:

```
<?php

class Elnogara_FirstModule_TestController extends Mage_Core_Controller_Front_Action <!--A nomeclatura da classe deve seguir esse padrão sempre que é o nome das pastas que o controller está dentro, e depois o nome do controller. Além disso para que o controller frontend funcione corretamente é necessário que ele extenda a classe Mage_Core_Controller_Front_Action-->
{
    public function testAction() <!--Aqui estamos declarando uma action para o nosso controller, muita atenção nela pois também será passada na nossa URL-->
    {
?>
        <h1>Hello World</h1>
        <h5>Seu primeiro módulo em Magento 1</h5>
<?php

    }
}
?>
```

Se olhar com atenção no exemplo acima, você percebe que tanto o Controller quanto a Action possuem seu nome e também o que são no próprio nome, ou seja o nome do nosso Controller é TestController.php e a Action é testAction(), é extremamente importante que os dois tenham isso para que o magento entenda o que são.

Agora que tudo foi criado é preciso entender como vamos chamar essa rota corretamente que acabamos de desenvolver. Para acessar um controller é necessário passar seu <strong>FrontName</strong>/<strong>Nome do controller</strong>/<strong>Action que será chamada</strong>... Nós já declaramos tudo isso, o frontname foi declarado lá no nosso config.xml quando criamos a rota, o nosso Controller foi passado no momento que criamos o TestController.php com o nome de _Test_ sendo o nome do controller e a Action é a função que será chamada dentro do Controller que nós definimos como TestAction(), sendo assim a nossa rota para executarmos o código dentro da action test será:

`
https://DOMINIO-DA-SUA-LOJA/firstmodule/test/test
`
</br></br><strong>Espero muito ter ajudado. Mas qualquer dúvida estou a disposição - <a href="https://wellingtonnogara.com/" style="color: red;">Wellington Nogara</a>.</strong>
