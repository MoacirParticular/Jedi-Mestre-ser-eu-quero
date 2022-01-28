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
 protocol EmployeeProtocol { var emplname: String {get} descrição da var: String {get} var salary: Int {get set} func paySalary (salary: Int)-> String
}
```

Normalmente, se usarmos get , podemos torná-lo um const , var , let ou propriedade computada. No entanto, usando a declaração de propriedade get set para os limites de propriedade salary var salary: Int {get set} para var .

Se quisermos escrever uma classe que siga este protocolo, como a classe Employee , temos o seguinte:

```
 class Employee: EmployeeProtocol { var emplname: String="Victor Jonah" var description: String="Software Engineer" salário var: Int=5000 func paySalary (salary: Int)-> String { return"Salário desembolsado para {emplname}" }
}
```

Em resumo, os protocolos nos permitem agrupar nossos métodos, propriedades e funções. No entanto, esses protocolos só podem estar em conformidade com classes, enums e structs.

Mais de um protocolo pode estar em conformidade com um objeto, mas devem ser separados por vírgulas:

```
 struct Player: MainPlayer, EnemyPlayer { //definição de código
}
```

Além disso, se uma classe tem uma superclasse, podemos definir quaisquer protocolos após o nome da superclasse:

```
 class TheClass: ItsSuperclass, FirstProtocol, SecondProtocol { //a definição da classe vai aqui
}
```

Podemos usar enum com nossos protocolos para propriedades computadas, mas eles não funcionam para propriedades armazenadas:

```
 enum Employer: EmployerProtocol { var name: String { retornar"Alex" } var description: String { retornar"CEO" } var salary: Int { obter { Retorna } }
}
```

O Swift também gera um erro no tempo de compilação se o protocolo não estiver em conformidade com a classe, estrutura ou enum.

#### Um exemplo de protocolo móvel Swift
Vejamos um caso de uso mais comum para o protocolo com um exemplo móvel:

```
 protocol Mobile { var name: String {get} var iEMICode: Int {get} var sIMCard: String {get} processador var: String {get} var internalMemory: Int {get} var isSingleSIM: Bool {get} função mutante GetIEMICode ()-> String função SendMessage ()-> String função Dial ()-> String função Receive ()-> String init (nome: String)
} struct Apple: Mobile { var name: String="Apple" init (nome: String) { self.name=name } var iEMICode: Int=3244332 var sIMCard: String="Vodaphone" processador var: String="Snapdragon" var internalMemory: Int=213424 var isSingleSIM: Bool=true função mutante GetIEMICode ()-> String { retornar"IEMEICode" } função SendMessage ()-> String { retornar"Mensagem enviada" } func Dial ()-> String { retornar"discado" } função Receive ()-> String { retornar"Recebendo chamada" }
} struct Samsung: Mobile { var name: String="Samsung" init (nome: String) { self.name=name } var iEMICode: Int=3243433 var sIMCard: String="TMobile" processador var: String="Snapdragon" var internalMemory: Int=324432 var isSingleSIM: Bool=false função GetIEMICode ()-> String { retornar"IEMEICode" } função SendMessage ()-> String { retornar"Mensagem enviada" } func Dial ()-> String { retornar"discado" } função Receive ()-> String { retornar"Recebendo chamada" }
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
 protocolo Pessoa { var name: String {get} var age: Int {get} var gender: String {get} func speak ()
} extensão Pessoa { func speak () { print ("Olá, isso funciona!") }
} classe Masculino: Pessoa { nome da var: String="" var age: Int=23 var gender: String="Masculino"
} struct Feminino: Person { var name: String var age: Int var gender: String
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
## Libs para Request






