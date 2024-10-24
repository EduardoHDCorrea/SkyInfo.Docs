# Dúvidas técnicas do projeto de declaração do ISSQN

<secondary-label ref="discussão"/>
<secondary-label ref="backend"/>

## Propriedades do RPS

Lista de dúvidas sobre as propriedades do RPS atribuídos na emissão do documento fiscal.

### Forma de Apresentação do Pagamento {collapsible="true" default-state="expanded"}
O valor deste campo é um enumerado com as seguintes opções:

    AVista 
    APrazo 
    NaApresentação 
    CartãoDeCrédito 
    CartãoDeDébito

- Dúvida: Esse campo será problemático de obter da nota de serviço do core?

### Situação Tributária {collapsible="true" default-state="expanded"}
O valor deste campo é um enumerado com as seguintes opções:

    TributadaNoPrestador 
    TributadaNoTomador 
    Isenta 
    Imune 
    NãoTributada

- Dúvida: Como será obtido esse valor?
- Observação: Dependendo do provedor, também será requisitado esse campo no serviço prestado de cada ato, por exemplo, no caso do provedor `IPM`.

### Tipo do RPS {collapsible="true" default-state="expanded"}

O valor deste campo é um enumerado com as seguintes opções:

    Rps 
    NotaFiscalConjugada 
    Cupom

- Dúvidas:
    - Como será obtido esse valor?
    - Temos algum caso em que não seja `Rps`?

### Tipo de Tributação {collapsible="true" default-state="expanded"}

O valor deste campo é um enumerado com as seguintes opções:

    Isenta 
    NãoIncidência 
    Imune 
    ExigibilidadeSuspensa 
    NãoTributável 
    Tributável 
    TributávelFixo 
    TributávelIsenção 
    MicroEmpreendedorIndividual

- Dúvida: como será obtido esse valor?

### Tipo do Tomador {collapsible="true" default-state="expanded"}

O valor deste campo é um enumerado com as seguintes opções:

    PessoaFísicaNãoIdentificada 
    PessoaFísica 
    PessoaJurídicaDoMunicípio 
    PessoaJurídicaDeForaDoMunicípio 
    PessoaJurídicaDoExterior

- Dúvidas:
    - Como será obtido esse valor?
    - Quando será pessoa física não identificada?

### Código IBGE do Município do Tomador {collapsible="true" default-state="expanded"}

Infelizmente, é um campo obrigatório para alguns provedores, como `IPM`. Será um problema para obter esse valor?

### Código do Serviço Prestado {collapsible="true" default-state="expanded"}

O código do serviço prestado é emitido por nota e, em alguns casos, por item de serviço. Terá algum cliente que terá códigos diferentes por nota, ou podemos manter esse valor atribuído à organização?

### Exigibilidade do ISS {collapsible="true" default-state="expanded"}

O valor deste campo é um enumerado com as seguintes opções:

    Exigível
    NãoIncidência
    Isenção
    Exportação 
    Imunidade 
    ExigibilidadeSuspensaPorDecisãoJudicial
    ExigibilidadeSuspensaPorProcessoAdministrativo
    IssFixo

- Dúvidas:
    - Será uma informação por nota ou podemos manter esse valor atribuído à organização?
    - Se for por nota, como será definido esse valor?

### Tipo de Operação {collapsible="true" default-state="expanded"}

O valor deste campo é um enumerado com as seguintes opções:

    SemDedução 
    ComDeduçãoDeMaterial 
    ImuneOuIsenta 
    DevoluçãoSimplesDaRemessa 
    Intermediário

- Dúvidas:
    - Como será definido esse valor?
    - Como esse valor é definido conforme o serviço prestado, podemos assumir que ele será atribuído na configuração da organização?

### Tipo de Retenção do ISS {collapsible="true" default-state="expanded"}

O valor deste campo é um enumerado com as seguintes opções:

    Retido 
    Normal
    Substituição

- Dúvidas:
    - Como será definido esse valor?
    - Será parte da configuração da organização ou será definido por nota?

### Tipo de 'Regime de Recolhimento' {collapsible="true" default-state="expanded"}

Esse campo é um enumerado com as seguintes opções:

    RegimeDeMovimento
    RegimeCancelado
    RegimeIsento
    RegimeImune
    RegimeDeNãoIncidência
    RegimeDeEstimativa 
    RegimeDeSociedadeLiberal
    RegimeDeSimplesNacional 
    RegimeDeMicroEmpreendedorIndividual

- Observações:
    - Esse campo usado apenas pelo `Governa`.
    - Nome do campo foi definido por mim por adivinhação, pois na documentação da ACBr só diz `RegRec`.

### Responsável pela Retenção {collapsible="true" default-state="expanded"}

Será sempre `Prestador`, ou teremos casos em que o responsável será `Tomador` ou `Intermediário`?