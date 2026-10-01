# LOCALIZAZ.js
### O LocaliZAZ é um script feito totalmente em JavaScript, o qual permite o programador adquirir Estados, Cidades, Número do IBGE, Códigos IATA e Códigos Postais (com detalhes como: Endereço, Bairro, GIA/ICMS, etc...).
```O uso do projeto é livre, peço somente que coloquem os créditos!```

Teste o **LocaliZaZ** no Github Pages: [https://artdsl.github.io/LocaliZAZ.js/](https://artdsl.github.io/LocaliZAZ.js/)

Testado o mesmo roda em navegadores **IE 8** à **IE 11** na versão [2.0.0.0](https://github.com/ArTDsL/LocaliZAZ.js/tree/2.0.0.0) (por hora), e nos navegadores mais novos com a versão 3.0.0.0 (atual), verifique a compatibilidade do seu navegador no [github pages](https://artdsl.github.io/LocaliZAZ.js/), caso queira dar um feedback ficarei muito grato ♥!


## Funcionalidades:
- Estados.
- Cidades.
- Códigos IBGE.
- Códigos IATA.<br>

**Busca por API (Gratuita com [ViaCEP](https://viacep.com.br))**
- Códigos Postais.
- Endereço
- Bairro
- Complemento
- Cidade
- Estado / UF
- Código IBGE (cidades) -> Atualizado
- GIA / ICMS
- DDD
- Código da Cidade SIAFI


## Implementação
Implementação fácil e simples;

### 1. Inicie o script

Chame o `src/localizaz.min.js` ou `src/localizaz.js` dentro do `<head>...</head>`:

#### 1.1. Versões atuais

Local (Branch atual):
```html
<script type="text/javascript" src="src/localizaz.min.js"></script>
```

**JSDelivr/CDN** (Master - **Faz update automático assim que uma nova versão é lançada**):
```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/ArTDsL/LocaliZAZ.js@master/src/localizaz.min.js"></script>
```

**JSDelivr/CDN** (Versão atual **_3.0.0.0_**):
```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/ArTDsL/LocaliZAZ.js@3.0.0.0/src/localizaz.min.js"></script>
```

#### 1.2. Versões anteriores

**JSDelivr/CDN** (Versão anterior **_2.0.0.0_**):
```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/ArTDsL/LocaliZAZ.js@2.0.0.0/src/localizaz.js"></script>
```
<small>A arquitetura da versão **2.0.0.0** é **diferente** da **3.0.0.0**, por favor verifique [aqui](https://github.com/ArTDsL/LocaliZAZ.js/tree/2.0.0.0).



### 2. Defina os campos:

Utilizando as classes disponíveis e o atributo de junção:<br>

#### 2.1. Classes Disponíveis 

- lzaz-estados
- lzaz-cidades
- lzaz-ibge-estado
- lzaz-ibge-cidade
- lzaz-iata

#### 2.2. Atributo de junção

O atributo de junção (`lzaz-id`) vai dentro da tag criada, informa ao **LocaliZAZ** que aquele campo em especifíco é **parte de um grupo**, ao atualiza-lo outros elementos distintos/iguais **com o mesmo atributo de junção** devem também ser automaticamente atualizados perante a informação do primeiro.

---

**_A ordem de atualização é:_**

**Estado** → **IBGE Estado**_(opcional)_ → **IATA**_(baseado no estado, opcional)_ → **Cidades** → **IBGE Cidades**_(opcional)_ → **IBGE Estado**_(opcional)_ → **IATA**_(baseado na cidade, opcional)_

---

Para verificar um exemplo de como isso funciona na prática verifique o [github pages](https://artdsl.github.io/LocaliZAZ.js/), na sessão **ESTADOS, CIDADES E CÓDIGOS DO IBGE (ELEM. MULTIPLOS COMBINADOS)**.

##### Elementos **SELECT**:
```html
<select class="lzaz-estados" lzaz-id="1"></select>
<select class="lzaz-cidades" lzaz-id="1"></select>
<select class="lzaz-iata" lzaz-id="1"></select>
...
```

##### Elementos **INPUT**:
```html
<input type="number" class="lzaz-ibge-estado" lzaz-id="1" placeholder="Cód. IBGE Estado" />
<input type="number" class="lzaz-ibge-cidade" lzaz-id="1" placeholder="Cód. IBGE Cidade" />
<input type="text" class="lzaz-cep" lzaz-id="1" placeholder="CEP" />
...
```

##### Elementos **TEXT** / **INPUT**:
```html
<strong>Cep Texto:</strong> <span lzaz-id="1" lzaz-vcepdata="cep"><small><i>...</i></small></span>
<strong>Cep Input:</strong> <input type="text" lzaz-id="1" lzaz-vcepdata="cep" />
...
```

_Se observar é possível notar que todos os elementos do exemplo possuem o `lzaz-id="1"` isso indica que todos estão conectados entre si._

---

## RETORNO DOS DADOS CEP
Utilizamos a API do [ViaCEP](https://viacep.com.br/) junto dos dados do **LocaliZAZ** para retornar as informações sobre os códigos postais, nesse caso é necessário que o desenvolvedor direcione os dados recebidos pela API para os campos necessários, para fazer isso basta:

### 1. Ativar API no campo de CEP

No campo de cep adicione o atributo `lzaz-viacep="on"`, isso indica que o LocaliZAZ está autorizado a enviar requests através desse campo;

```html
<input type="text" class="lzaz-cep" lzaz-id="1" lzaz-viacep="on" placeholder="CEP" />
```

### 2. Configuração de máscara

Caso seu campo de CEP tenha máscara _(#####-###)_ é necessário o comentário após a abertura da tag `<body>` a linha:
```html
<body>
    <!--LZAZ:MASKED_CEP-->
</body>
```
Isso irá informar o **LocaliZAZ** que seu **CEP contém máscara e deve ser enviado somente após 9 digitos**, caso contrário o mesmo enviará com 8 e a requisição retornará com erro.


### 3. Retorno

O desenvolvedor pode usar o atributo `lzaz-vcepdata` para retornar as informações, um exemplo disso pode ser visto abaixo:
```html
<strong>Cep:</strong> <input type="text" lzaz-id="1" lzaz-vcepdata="cep" />
<strong>Estado:</strong> <input type="text" lzaz-id="1" lzaz-vcepdata="estado" />
<strong>Cidade:</strong> <input type="text" lzaz-id="1" lzaz-vcepdata="localidade" />
```

É possível utilizar o `lzaz-vcepdata` juntamente com o `lzaz-id` e prévio carregamento de dados do **LocaliZAZ**:
```html
<select class="lzaz-estados" lzaz-id="1" title="Estados" lzaz-vcepdata="estado"></select>
<select class="lzaz-cidades" lzaz-id="1" title="Cidades" lzaz-vcepdata="localidade"></select>

```

_No último exemplo acima, ao preencher o CEP será selecionado o estado e logo em seguida a cidade, automaticamente, fazendo com que o ViaCEP interaja com os dados locais do **LocaliZAZ**._

#### 2.1. LZAZ-VCEPDATA Disponíveis 

- _"**estado**"_ → Retorna o **ESTADO** no campo / select / elemento indicado.
- _"**localidade**"_ → Retorna a **CIDADE** no campo / select / elemento indicado.
- _"**unidade**"_ → Retorna a **UNIDADE** no campo / elemento indicado.
- _"**uf**"_ → Retorna a **UF** no campo / elemento indicado.
- _"**cep**"_ → Retorna o **CEP** no campo / elemento indicado.
- _"**logradouro**"_ → Retorna o **ENDEREÇO** no campo / elemento indicado.
- _"**bairro**"_ → Retorna o **BAIRRO** no campo / elemento indicado.
- _"**complemento**"_ → Retorna o **complemento** no campo / elemento indicado.
- _"**regiao**"_ → Retorna o **REGIÃO da Cidade** no campo / elemento indicado.
- _"**ibge**"_ → Retorna o **Código IBGE da Cidade** no campo / elemento indicado.
- _"**gia**"_ → Retorna o **GIA/ICMS** no campo / elemento indicado.
- _"**ddd**"_ → Retorna o **DDD da Cidade / Região** no campo / elemento indicado.
- _"**siafi**"_ → Retorna o **Código SIAFI da Cidade** no campo / elemento indicado.


## DESABILITANDO OS LOGS NO CONSOLE

Para desabilitar os logs no console, assim como as **CONFIGURAÇÕES DE MÁSCARA** basta adicionar o seguinte comentário após a abertura da tag `<body>`:
```html
<body>
    <!--LZAZ:DISABLELOG-->
</body>
```

## Licença

O LocaliZAZ é distribuído gratuitamente sob a licença **GNU General Public License v3.0** que pode ser encontrada [aqui](https://github.com/ArTDsL/LocaliZAZ.js/blob/localizaz.js/LICENSE)

## Informações

Gostou do projeto? **Quer me ajudar a manter?** Ajude com uma **contribuição, fork, compartilhamento** ou _donate_ ^-^.

**X's** <small>_(antigo twitter)_</small>: [@ArT_DsL](https://x.com/ArT_DsL)
