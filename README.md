# LOCALIZAZ.js
### O localizaz é um script feito totalmente em JavaScript, o qual permite o programador adquirir Estados, Cidades, Número do IBGE, Códigos IATA e Códigos Postais (com detalhes como: Endereço, Bairro, IAG/ICMS, etc...).
```O uso do projeto é livre, peço somente que coloquem os créditos!```

Testado o mesmo roda em navegadores **IE 8+**, verifique a compatibilidade do seu navegador executando o arquivo de teste, caso queira dar um feedback ficarei muito grato ♥!


## Funcionalidades:
- Estados.
- Cidades.
- Códigos IBGE.
- Códigos IATA.
- Códigos Postais.


## Implementação
Diria que a implementação é a mais simples possível, basta abrir o script e alterar os **ID's** das variáveis globais pelos ids das **SelectBoxes** em sua página html:

```
const estado_box = "estado_sb";
const cidade_box = "cidade_sb";
const ibge_estado_inp = "ibge_estado_input";
const ibge_cidade_inp = "ibge_cidade_input";
const iata_aeroportos = "iata_input";
const cod_postal = "codpostal_input";
```

### RETORNO DOS DADOS CEP
Utilizamos a API do [ViaCEP](https://www.viacep.com.br/) junto dos dados do LocaliZAZ para retornar as informações sobre os códigos postais, nesse caso é necessário que o desenvolvedor direcione os dados recebidos pela API para seu sistema ou campos necessários, para fazer isso procure pela linha:

```
// _________PROGRAME___AQUI___O___DESTINO___DOS___DADOS___RECEBIDOS_________ //
```

O desenvolvedor pode usar os seguintes objetos JSON para retornar os dados:

```
[-] retorno.logradouro: Endereço do CEP digitado,
[-] retorno.bairro: Bairro do CEP digitado,
[-] retorno.cep: CEP formatado contendo apenas números e traço,
[-] retorno.complemento: Complemento do CEP digitado (Endereço),
[-] retorno.localidade: Cidade do CEP digitado,
[-] retorno.uf: Estado do CEP digitado,
[-] retorno.ibge: Código do IBGE referente a Cidade,
[-] retorno.gia: GIA/ICMS da cidade/região onde se localiza o CEP,
[-] retorno.ddd: DDD da cidade/região onde se localiza o CEP,
[-] retorno.siafi: Código da Cidade S.I.A.F.I (Sistema Integrado de Administração Financeira) da cidade/região onde se localiza o CEP.
```

Gostou do projeto? Quer me ajudar a manter o mesmo? Ajude com uma contribuição, fork, compartilhamento ou donate ^-^.


Paypal: arthur@artdslgames.com.br

Twitter: @ArT_DsL
