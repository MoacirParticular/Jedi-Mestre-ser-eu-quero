# Swift
[Melhor dos melhores](https://docs.swift.org/swift-book/)

Swift é uma maneira fantástica de escrever software, seja para telefones, desktops, servidores ou qualquer outra coisa que execute código. É uma linguagem de programação segura, rápida e interativa que combina o melhor do pensamento linguístico moderno com a sabedoria da cultura de engenharia mais ampla da Apple e as diversas contribuições de sua comunidade de código aberto. O compilador é otimizado para desempenho e a linguagem é otimizada para desenvolvimento, sem comprometer nenhum dos dois.


## Extensões

As extensões adicionam novas funcionalidades a uma classe, estrutura, enumeração ou tipo de protocolo existente. Isso inclui a capacidade de estender tipos para os quais você não tem acesso ao código-fonte original (conhecido como modelagem retroativa). As extensões são semelhantes às categorias no Objetivo C. (Ao contrário das categorias Objective-C, as extensões Swift não têm nomes.)

Extensões em Swift podem:

* Adicione propriedades de instância computada e propriedades de tipo computado
* Defina métodos de instância e métodos de tipo
* Forneça novos inicializadores
* Defina subscritos
* Defina e use novos tipos aninhados
* Faça com que um tipo existente esteja em conformidade com um protocolo

Em Swift, você pode até estender um protocolo para fornecer implementações de seus requisitos ou adicionar funcionalidades adicionais que os tipos em conformidade podem aproveitar. Para mais detalhes, consulte [Extensões de Protocolo](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html#ID521).

``` 
    NOTA

    As extensões podem adicionar novas funcionalidades a um tipo, mas não podem substituir a funcionalidade existente.
```

[Saiba mais](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html)




## O que são protocolos e como funcionam no Swift?

### Geralmente, um protocolo:

* É um projeto que uma classe ou estrutura segue
* É um contrato de comunicação para objetos não relacionados nos quais confiar
* Define métodos e valores

Para entender como os protocolos funcionam no Swift, vamos supor que estejamos construindo um software aplicativo e devemos modelar os requisitos para satisfazer o aplicativo. Podemos começar com uma superclasse e moldar o relacionamento por meio de herança ou começar com um protocolo e moldar o relacionamento por meio da implementação.

Se quisermos construir um sistema de remessa de salários para nosso aplicativo e tivermos uma classe Funcionário , usar um protocolo parecido com o seguinte:

```
protocol EmployerProtocol {
    var emplname: String { get }
    var description: String { get }
    var salary: Int {get set}
    
    func paySalary (salary: Int)-> String
}
```

Normalmente, se usarmos get , podemos torná-lo um const , var , let ou propriedade computada. No entanto, usando a declaração de propriedade get set para os limites de propriedade salary var salary: Int {get set} para var .

Se quisermos escrever uma classe que siga este protocolo, como a classe Employee , temos o seguinte:

```
class Employee: EmployerProtocol {
    var emplname: String="Victor Jonah"
    var description: String="Software Engineer"
    var salary: Int=5000
    
    func paySalary (salary: Int)-> String { return"Salário desembolsado para {emplname}" }
}
```

Em resumo, os protocolos nos permitem agrupar nossos métodos, propriedades e funções. No entanto, esses protocolos só podem estar em conformidade com classes, enums e structs.

Mais de um protocolo pode estar em conformidade com um objeto, mas devem ser separados por vírgulas:

```
struct Player: MainPlayer, EnemyPlayer { 
    //definição de código
}
```

Além disso, se uma classe tem uma superclasse, podemos definir quaisquer protocolos após o nome da superclasse:

```
class TheClass: ItsSuperclass, FirstProtocol, SecondProtocol { 
    //a definição da classe vai aqui
}
```

Podemos usar enum com nossos protocolos para propriedades computadas, mas eles não funcionam para propriedades armazenadas:

```
 enum Employer: EmployerProtocol {
    var salary: Int = 5000
    
    var emplname: String { return "Alex" }
    var description: String { return "CEO" }
    
    
    func paySalary(salary: Int) -> String {
            return "Paga ai."
    }    
}
```

O Swift também gera um erro no tempo de compilação se o protocolo não estiver em conformidade com a classe, estrutura ou enum.

#### Um exemplo de protocolo móvel Swift
Vejamos um caso de uso mais comum para o protocolo com um exemplo móvel:

```
 protocol Mobile {
    var name: String {get}
    var iEMICode: Int {get}
    var sIMCard: String {get}
    var processador: String {get}
    var internalMemory: Int {get}
    var isSingleSIM: Bool {get}
    
    func GetIEMICode ()-> String
    func SendMessage ()-> String
    func Dial ()-> String
    func Receive ()-> String
    
    init (nome: String)
}

struct Apple: Mobile {
    var name: String="Apple"
    
    init (nome: String) {
        self.name  = nome
    }
    
    var iEMICode: Int=3244332
    var sIMCard: String="Vodaphone"
    
    var processador: String="Snapdragon"
    var internalMemory: Int=213424
    var isSingleSIM: Bool=true
    
    func GetIEMICode ()-> String {
        return "IEMEICode"
    }
    
    func SendMessage ()-> String {
        return "Mensagem enviada"
    }
    
    func Dial ()-> String {
        return "discado"
    }
    
    func Receive ()-> String {
        return "Recebendo chamada"
    }
}

struct Samsung: Mobile {
    var name: String="Samsung"
    init (nome: String) {
        self.name = nome
    }
    
    var iEMICode: Int=3243433
    var sIMCard: String="TMobile"
    var processador: String="Snapdragon"
    var internalMemory: Int=324432
    var isSingleSIM: Bool=false
    
    func GetIEMICode ()-> String {
        return "IEMEICode"
    }
    
    func SendMessage ()-> String {
        return "Mensagem enviada"
    }
    
    func Dial ()-> String {
        return "discado"
    }
    
    func Receive ()-> String {
        return "Recebendo chamada"
    }
}
```

Observe que a palavra-chave mutating na linha 9 funciona quando temos um objeto que deve alterar uma de suas propriedades. Devemos especificar que GetIEMICode () é um método mutante em nosso protocolo. Em nossa estrutura, também devemos especificar a palavra-chave mutating , mas não na classe.

Vantagens dos protocolos em Swift
A partir dos exemplos acima, podemos ver porque os protocolos são úteis e porque o Swift usa o paradigma orientado a protocolo. As vantagens de usar protocolos se manifestam das seguintes maneiras:

#### Clareza do código
Os protocolos de nomenclatura fornecem um melhor entendimento de suas instâncias. Em nosso primeiro exemplo, criamos um EmployeeProtocol que está em conformidade com a classe Employee , mostrando como os protocolos oferecem significado para classes, enums ou structs.

Como Dave Abrahams disse na WWDC 2015 , “Não comece com uma aula, comece com um protocolo. ”

#### Reutilização
Com extensões de protocolo, podemos ter uma implementação padrão para nosso método na classe, enum ou estrutura com a qual estão em conformidade. Podemos ver isso no código abaixo:

````
 protocol Person {
    var name: String {get}
    var age: Int {get}
    var gender: String {get}
    func speak ()
}

extension Person {
    func speak () {
        print ("Olá, isso funciona!")
    }
}

class Masculino: Person {
    var name: String=""
    var age: Int=23
    var gender: String="Masculino"
}

struct Feminino: Person {
    var name: String
    var age: Int
    var gender: String
}
````

Ao criar uma funcionalidade padrão usando a palavra-chave extension na linha 9, não precisamos repeti-la em nossa classe ou estrutura.

Separação de classes
Os protocolos também eliminam a necessidade de classes, enums e structs dependerem uns dos outros porque não usam herança.

Conclusão
Em resumo, os protocolos em Swift oferecem comunicação entre objetos não relacionados, onde definimos os métodos e variáveis ​​observados em classes, enums e structs. Como o Swift adota o paradigma orientado a protocolo, podemos modelar nosso sistema antes de definir classes, estruturas ou enums, tornando o processo mais eficiente.

A postagem [Compreendendo os protocolos em Swift](https://blog.logrocket.com/understanding-protocols-in-swift/) apareceu primeiro em [LogRocket Blog](https://blog.logrocket.com).



## Delegate

Delegação é um padrão de projeto simples mas extremamente poderoso usado quando um objeto age no lugar de um outro ou junto com ele. Delegar uma ação é perguntar para outro objeto como uma certa ação deve ser realizada. Um exemplo clássico de método de um delegate é o didSelectRowAtIndexPath: do UITableViewDelegate que informa que uma célula foi selecionada. Delegação é usado quando se quer delegar uma tarefa ou 'perguntar' algo para outro objeto.

[Saiba Mais](https://pt.stackoverflow.com/questions/50526/quando-e-como-usar-protocolos-e-delegates/50602)

## Codable 
Codable é um alias de tipo para os protocolos Codable e Decodable. Quando você usa Codable como um tipo ou uma restrição genérica, ele corresponde a qualquer tipo que esteja em conformidade com ambos os protocolos.

[Saiba Mais](https://developer.apple.com/documentation/swift/codable)


## Como faz uma request no Swift


## Storyboard

.storyboardé essencialmente um único arquivo para todas as suas telas no aplicativo e mostra o fluxo das telas. Você pode adicionar segues/ transições entre telas, dessa maneira. Portanto, isso minimiza o código padrão necessário para gerenciar várias telas.

## XIB

Antes do storyboard, cada UIViewController tinha um .xib associado a ele. .Xib é onde você pode criar sua tela individual.

## ViewCode

A escolha entre usar Storyboards e escrever views programaticamente em um projeto iOS é muito subjetiva. Tendo lidado com ambas no passado, eu pessoalmente, apoio projetos que são completamente escritos com views programáticas – pela sua capacidade de permitir que várias pessoas façam alterações na mesma tela, sem conflitos impossíveis de se resolver, e pelo code review facilitado.

## Notification Center

Um mecanismo de envio de notificações que permite a transmissão de informações a observadores registrados.

## Notificação de pouca memória em uma ViewController

Visão Geral
Se o sistema ficar com pouca memória livre e não conseguir recuperar a memória encerrando aplicativos suspensos, o UIKit enviará um aviso de baixa memória para aplicativos em execução. O UIKit fornece avisos de baixa memória das seguintes maneiras:
It calls the applicationDidReceiveMemoryWarning(_:) method of your app delegate.
It calls the didReceiveMemoryWarning() method of any active UIViewController classes.
It posts a didReceiveMemoryWarningNotification object to any registered observers.
Ele fornece um aviso para despachar filas do tipo DISPATCH_SOURCE_TYPE_MEMORYPRESSURE.

Quando seu aplicativo receber um aviso de baixa memória, libere o máximo de memória possível o mais rápido possível. Remova referências a imagens, arquivos de mídia ou quaisquer arquivos de dados grandes que já tenham uma representação no disco e possam ser recarregados posteriormente. Remova referências a quaisquer objetos temporários que você não precise mais. Se as tarefas ativas puderem consumir quantidades significativas de memória, pause as filas de despacho ou restrinja o número de operações simultâneas que seu aplicativo executa.

```
Importante
A falha em reduzir o uso da memória do seu aplicativo pode resultar no encerramento do seu aplicativo. Portanto, considere gravar quaisquer dados não salvos no disco como parte de seus esforços de limpeza.
```

Para testar a resposta do seu aplicativo a um aviso de baixa memória, use o comando Simular Aviso de Memória no iOS Simulator.


## Clean Code 

Código limpo nada mais é do que código de ótima qualidade.
A procura por escrever códigos de qualidade é comportamento intrínseco à nossa profissão. Desde a primeira linha de código já procuramos e estabelecemos padrões que o tornam melhor. Porém, devemos nos aprofundar nesse assunto, pois, hoje, há padrões difundidos e regras fundamentais provenientes de décadas de refinamento.
Minha primeira experiência no estudo aprofundado de código limpo foi a partir do livro Clean Code de Robert C. Martin. A obra é um ótimo inicio para quem pretende escrever códigos melhores.
Minhas lições aqui partem dos ensinamentos desse livro, juntamente com outros materiais, e da minha experiência no desenvolvimento para iOS. Vamos lá!
A mentalidade necessária
Um código limpo deve ser feito do pequeno para o grande. Da menor parte para a maior. Dos detalhes para as arquiteturas.
“Honestidade em pequenas coisas não é uma coisa pequena”. Ditado dinamarquês.
“Quem é fiel no pouco é fiel no muito”. Ditado popular.
Esses dois ditados refletem qual deve ser a nossa mentalidade em busca do código limpo.
Os detalhes são importantes. Cada quebra de linha, palavra escolhida, quebra de funções se somam e garantem a qualidade de código do projeto.
Lembre-se do ensinamento do arquiteto Ludwig Mies van der Rohe:
A maçaneta é tão importante quanto o alicerce. Uma janela quebrada pode passar a impressão de uma casa grandiosa ser mal cuidada, e influenciará a ter mais janelas quebradas.
Quando você dá a devida importância as menores partes de seu código, essas frases vão fazer cada vez menos sentido:
"O impacto é pouco"
"Isso é frescura"
"Pra que escrever isso em 3 linhas se posso fazer em uma?"
"Essa regra não está escrita em pedra!"
"Mas para mim está claro a finalidade desse código"
A prática
Após mudar sua mentalidade, você vai precisar se esforçar.
Criar códigos limpos é uma tarefa árdua e requer mais do que o simples conhecimento dos princípios e padrões. Requer disciplina, atenção e estudo para que a cada dia, você escreva um código mais limpo que no dia anterior.
Leve consigo os seguintes ensinamentos:
1. Refinamento jamais acaba.
Um projeto com código limpo não nasce limpo e continua limpo. Ou se torna limpo e permanece assim. Ele deve ser sempre sendo refatorado. Porque o aumento do tamanho do projeto e do número de funcionalidades vão criar oportunidades de melhorias naturalmente. Para sistema mais complexos deve se adotar padrões mais robustos.
Pense em seu projeto como se fosse uma cidade. Um vilarejo não poderia já de inicio criar vias do 60m de largura para se tornarem, futuramente, vias expressas. Isso não é sustentável. A melhor forma é modernizar a cidade e adequa-la a partir de seu crescimento.
2. Mais tarde é igual a nunca.
Quando percebida uma duplicação de código, já planeje sua refatoração. Quando sabido de um novo padrão mais eficiente, já trabalhe pensando em sua implementação.
E por fim…
3. Deixe o código mais limpo do que quando você o encontrou.
Pegando emprestada o pensamento dos bandeirantes, essa é a regra básica da prática do código limpo.
Importância e Impacto
Robert Martin diz:
A taxa de velocidade para ler um código é 10x a taxa de escrever um.
Então, fazer seu código mais legível o torna absurdamente mais manutenível e incrementável.
E um código assim tem grande impacto na longevidade de um projeto.
Em um projeto que não é dado a devida importância às boas práticas arquiteturais e ao código, com o tempo, a confusão e complexidade aumentam.
Assim a produtividade da equipe diminui, assintoticamente, aproximando de zero. Nesses casos, a gerência faz a única coisa que acha que pode: aumenta o time. E com isso, a produtividade diminui mais ainda.
Essa é uma história de vários projetos.
Alguns deles, antes de chegar no caos total, começam a migrar para uma nova base de código. A equipe é dividida. Alguns vão para nova versão e outros continuam dando manutenção no legado. Porém, se as causas do problema, que são a falta de código limpo, refatoração, boas práticas e padrões de código, não são corrigidas, nada adiantará.
Então, lembre-se, a aplicação de código limpo tem consequências de:
PRODUTIVIDADE: no longo prazo a produtividade continua alta;
SATISFAÇÃO: o estresse e medo da equipe diminui por ter mais sensação de segurança, ordem e produtividade;
APRENDIZAGEM: quem é novo na equipe vai conseguir se integrar melhor e aprender os padrões mais rápido;
POSSIBILIDADE DE SOLUÇÕES INOVADORES: maior facilidade de implementação de novas arquiteturas, experimentos e funcionalidades.
Enfim, o que é o código limpo?
Juntando as respostas de algum dos maiores pesquisadores e pensadores na área do desenvolvimento para essa pergunta, o código limpo resumidamente é:
Simples
Eficiente
Direto
Legível
Testável
Além disso, se observa nele:
Nomes significativos
Mínima duplicação de código
Alta expressividade
Separação de responsabilidades
Cobertura total de erros
Pensando de forma mais abstrata, podemos dizer que foi escrito por alguém que se importou. Essa pessoa dedicou esforço e carinho para que quem o lesse pudesse desfrutar de entendimento e clareza.
E essa pessoa que o lê, tem a sensação que cada linha é exatamente como esperava. Com vários entusiasmos de “Simmmm!” e nenhum de “Quê????”.
Termino por aqui a primeira parte sobre Clean Code aplicado à Swift.
Neste artigo abordei mais questões abstratas e gerais, no(s) próximo(s) falarei totalmente sobre código, padrões e dicas.



## MVVM

Na arquitetura MVVM temos os componentes Model, View e a ViewModel.

Model: Segue com as mesmas responsabilidades das arquiteturas citadas anteriormente (MVC e MVP);
  View: Segue com as mesmas responsabilidades da arquitetura anterior (MVP);
  ViewModel: É definida como um intermediário entre um ou mais objetos da View e um ou mais objetos da Model, diferenciando da relação encontrada na MVP, onde existe uma relação de 1:1 entre os componentes. A ViewModel pode ser instanciada em várias Views distintas, na proporção 1:N, possibilitando maior reaproveitamento de código.
  
## principais vantagens e desvantagens do MVVM?

### Vantagens MVVM
Possibilidade do reaproveitamento de código, pois a ViewModel pode ser compartilhada entre diversas Views.

### Desvantagens MVVM
Para projetos de grande complexidade, a utilização de várias Views com a mesma ViewModel pode sobrecarregá-la.


## O que é uma arquitetura MVVM-C?

O Coordinator é um componente amplamente utilizado em algumas arquiteturas. Ele vem para complementar arquiteturas como o MVVM, por exemplo, assumindo a responsabilidade pelas ações de fluxo entre telas, tornando a ViewModel mais limpa.



## Orientação a Objetos

A programação orientada a objetos surgiu como uma alternativa a essas características da programação estruturada. O intuito da sua criação também foi o de aproximar o manuseio das estruturas de um programa ao manuseio das coisas do mundo real, daí o nome "objeto" como uma algo genérico, que pode representar qualquer coisa tangível.

## Se conhece Orientação a Objetos, descreva com poucas palavras

### Herança
Herança é um mecanismo que permite que características comuns a diversas classes sejam fatoradas em uma classe base, ou superclasse. A partir de uma classe base, outras classes podem ser especificadas. Cada classe derivada ou subclasse apresenta as características (estrutura e métodos) da classe base e acrescenta a elas o que for definido de particularidade para ela.

### Polimorfismo
Polimorfismo é o princípio pelo qual duas ou mais classes derivadas da mesma superclasse podem invocar métodos que têm a mesma assinatura, mas comportamentos distintos.

### Threads
o threading tem tudo a ver com gerenciar como o trabalho é priorizado em seu aplicativo. Fazer seu código ser executado mais rápido é ótimo, mas o que importa mais é a rapidez com que o usuário percebe que seu aplicativo é.
Seu objetivo como desenvolvedor é priorizar qualquer coisa com a qual o usuário possa ver e interagir. Isso faz com que seu aplicativo se sinta mais rápido e rápido. Não faça o usuário esperar por algo para carregar que ele não perceba ou se importe.


## Qual a diferença de Model para ViewModel ?

### Model
A camada de modelo é responsável pela lógica de negócios do aplicativo. Ele gerencia o estado do aplicativo. Isso também inclui leitura e gravação de dados, estado persistente do aplicativo e pode até incluir tarefas relacionadas ao gerenciamento de dados, como rede e validação de dados.

### ViewModel
A camada de ViewModel (visualização) tem duas tarefas importantes, apresentar dados ao usuário e lidar com a interação do usuário.


## Notificação de Pouca Memória
Se o sistema ficar com pouca memória livre e não conseguir recuperar a memória encerrando aplicativos suspensos, o UIKit enviará um aviso de baixa memória para aplicativos em execução. O UIKit fornece avisos de baixa memória das seguintes maneiras:
It calls the applicationDidReceiveMemoryWarning(_:) method of your app delegate.
It calls the didReceiveMemoryWarning() method of any active UIViewController classes.
It posts a didReceiveMemoryWarningNotification object to any registered observers.
Ele fornece um aviso para despachar filas do tipo DISPATCH_SOURCE_TYPE_MEMORYPRESSURE.
Quando seu aplicativo receber um aviso de baixa memória, libere o máximo de memória possível o mais rápido possível. Remova referências a imagens, arquivos de mídia ou quaisquer arquivos de dados grandes que já tenham uma representação no disco e possam ser recarregados posteriormente. Remova referências a quaisquer objetos temporários que você não precise mais. Se as tarefas ativas puderem consumir quantidades significativas de memória, pause as filas de despacho ou restrinja o número de operações simultâneas que seu aplicativo executa.
Importante
A falha em reduzir o uso da memória do seu aplicativo pode resultar no encerramento do seu aplicativo. Portanto, considere gravar quaisquer dados não salvos no disco como parte de seus esforços de limpeza.
Para testar a resposta do seu aplicativo a um aviso de baixa memória, use o comando Simular Aviso de Memória no iOS Simulator.


