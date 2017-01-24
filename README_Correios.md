![valid XHTML][checkmark]
[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/Red_star_32_32.png "MOZG"
[url-method]: http://correios.com.br/
[requerimentos]: http://mozgbrasil.github.io/requerimentos/
[limites-de-dimensoes-e-de-peso]: http://www.correios.com.br/para-voce/precisa-de-ajuda/limites-de-dimensoes-e-de-peso
[mao-propria-mp]: http://www.correios.com.br/para-voce/correios-de-a-a-z/mao-propria-mp
[aviso-de-recebimento-ar]: http://www.correios.com.br/para-voce/correios-de-a-a-z/aviso-de-recebimento-ar
[valor-declarado]: http://www.correios.com.br/para-voce/correios-de-a-a-z/valor-declarado
[contact-correios]: http://www2.correios.com.br/sistemas/falecomoscorreios/
[encomendas-prazo]: http://www2.correios.com.br/sistemas/precosprazos/default.cfm
[magento-cron]: http://devdocs.magento.com/guides/m1x/install/installing_install.html#install-cron
[mozg-cron]: https://mozg.com.br/dicas/dicas-magento1#como-ativar-a-cron-no-magento
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[github-boxpacker]: https://github.com/mozgbrasil/magento-boxpacker-php56#mozgboxpacker
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove

# Mozg\Correios

## Sinopse

Integração ao [Correios][url-method]

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Recursos

- Definir dimensões para os produtos

- Definir dimensões, peso e valor da Embalagem/Caixa

- Opção para embalar os produtos separadamente ou combinar na mesma Embalagem/Caixa

- Embalagem do produto inteligente, exibe como os produtos serão agrupados e calcula o peso dimensional fazendo o envio fracionado se necessário

- Armazenamento das requisições em Cache

- Notificação automática do rastreamento

- Impressão de etiquetas

~~- Definir como diferentes combinações de produtos são embalados em conjunto # TODO~~

~~- Atribuir produtos a determinadas caixas (produtos múltiplos podem ser atribuídos à mesma caixa) # TODO~~

## Característica técnica

Atualmente diversos módulos de terceiros relativo a métodos de entrega sempre soma o peso e dimensões dos produtos gerando falha na requisição a transportadora devido não terem um sistema que separa os produtos em sua devida embalagem distribuindo seu peso.

O nosso módulo foi desenvolvido visando total transparência dos processos executados, para efeito de análise visualize os processos armazenado em log.

A extensão permite você definir as dimensões de seus produtos, as dimensões de suas embalagens e regras de como empacotar diferentes combinações de produtos em conjunto.

A extensão escolhe qual embalagem será utilizado para embalar os produtos para o pedido.

A extensão pode distribuir os produtos em diversas embalagens até o peso máximo suportado para a embalagem.

Como será cadastrado a embalagem com as dimensões e peso suportado pelas transportadoras não deve ocorrer falha relativa as dimensões ou peso.

A primeira coisa a se levar em consideração no uso do módulo é o [Gerenciamento de Embalagem/Caixa][github-boxpacker], como já vem alguns registros pré inseridos certifique se de atualizar os registros conforme sua necessidade.

Certifique se ter cadastrado as devidas dimensões para os produtos.

Para cada embalagem é feito uma requisição a transportadora onde é passado os devidos parâmetros

O módulo possui armazenamento de cache

Na finalização do pedido é armazenado no histórico do pedido um comentário contendo um identificador único que poderá ser usado para consulta no arquivo de log a discriminação dos pacotes seus itens e a visualização de cada pacote com seus itens em 3D

Sempre confira as informações de frete antes de processar cada pedido, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

Para o rastreamento do pacote é feito acesso ao WebService onde é passado os devidos parâmetros e exibido o devido retorno

O módulo possui notificação automática do rastreamento sendo enviado e-mail sobre a mudança de status das suas encomendas ou pacotes do site do correios

Para usar esse recurso, configure o Magento para usar a [CRON][magento-cron] | [CRON][mozg-cron]

## Instalação - Atualização - Desinstalação - Desativação

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Antes de executar os processos, [clique aqui][requerimentos] e leia os pré-requisitos e sugestões

--

Certique se da existencia do arquivo composer.json na raiz do projeto Magento e que o mesmo tenha os trechos "minimum-stability", "prefer-stable", "repositories" e '"magento-root-dir":"./"', conforme https://gist.github.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba

Caso não exista o arquivo composer.json na raiz do projeto Magento, efetue o download

	wget https://gist.githubusercontent.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba/raw/9b514bc896171b6d75833b6f165065356f62ca59/composer.json

--

Para qualquer atualização no Magento sempre mantenha o Compiler e o Cache desativado

--

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor

	composer require mozgbrasil/magento-correios-php56:dev-master

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor

	composer clear-cache && composer update

Na ocorrência de erro, renomeie a pasta /vendor/mozgbrasil e execute novamente

Para checar a data do módulo execute o seguinte comando

	grep -ri --include=*.json 'time": "' ./vendor/mozgbrasil

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor

	composer remove mozgbrasil/magento-correios-php56 && composer clear-cache && composer update

--

### Para desativar o módulo

Renomeie a pasta do módulo

Cada módulo tem a sua pasta no diretório /vendor/mozgbrasil/

## Como configurar o método de entrega

Antes de configurar o módulo você deve cadastrar o CEP de origem, indo ao backend em:

	STORES -> Configuration -> Sales/Shipping Settings -> Origin

Para configurar o método de entrega, acesse no backend em:

	STORES -> Configuration -> Sales/Shipping Methods -> Correios (powered by MOZG)

Você terá os campos a seguir

### • **Ativar**

Para "ativar" ou "desativar" o uso do método

### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

### • **Título**

Nome do método que deve ser exibido

### • **Serviços**

Selecione os serviços desejado, para selecionar mais de um, segure a tecla "Ctrl" e clique nos serviços

### • **Serviço Para Entrega Gratuita**

Quando houver um desconto de frete grátis, esse serviço terá o valor zero

### • **Calcular taxa de manuseio**

Podendo ser fixo ou percentual

### • **Taxa de Manuseio**

Será adicionado o valor ao frete

### • **Mostrar método se não aplicável**

Quando configurado como "Não", caso seja retornado algum serviço com erro, não será exibido o método de entrega

### • **Debug**

Deve ser armazenado os processos do módulo em var/log/

O arquivo 

DATE_mozg.log

se trata de log do módulo sendo um log mais detalhado contendo todos os processos inclusive das execuções realizadas pelas bibliotecas externas do módulo

O arquivo

shipping_METHOD.log

se trata de log nativo do magento relativo ao método de entrega

### • **Enviar para países aplicáveis**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

### • **Enviar para países específicos**

Você deve selecionar os países que o método deve ser funcional

### • **Identificador do atributo largura dos produtos**

Permite definir o nome do atributo de largura dos produtos usado no projeto

### • **Identificador do atributo comprimento dos produtos**

Permite definir o nome do atributo de comprimento dos produtos usado no projeto

### • **Identificador do atributo altura dos produtos**

Permite definir o nome do atributo de altura dos produtos usado no projeto

### • **Unidade de medida**

Sendo o padrão do peso do produto como kilo

Caso esteja usando a unidade de massa em gramas, tanto os produtos como as embalagens devem respeitar o mesmo padrão

Ao informar na configuração do método o uso da unidade de massa em gramas é feito a conversão do peso de grama para kilo

1 Kg no formato "Kilo" será "1.000", já em "Gramas" será "1000.000"

### • **Exibir Prazo de Entrega**

Se será ou não mostrado o prazo de entrega para seu cliente

### • **Mensagem que Exibe o Prazo de Entrega**

Se será ou não mostrado o prazo de entrega para seu cliente

### • **Adicionar (dias) ao prazo de entrega**

Quantidade de dias que será adicionado ao prazo

### • **Mostrar serviço com retorno de erro**

Quando configurado como "Não", caso seja retornado algum serviço com erro, o mesmo não deve ser exibido no método de entrega

### • **Ativar rastreamento automático via CRON**

Quando alterado o registro para Não o processo não deve ser executado pela CRON em execução do Magento

### • **Código administrativo junto à ECT**

Se você possui contrato com os Correios, preencha nesse campo o número do contrato

*Lojistas com contrato possuem valor diferenciado de postagem junto aos Correios*

### • **Senha Administrativa dos Correios (Serviços Com Contrato)**

Senha do seu contrato, por padrão são os 8 primeiros dígitos do CNPJ

### • **Utilizar Serviço de Mão Própria**

É o [serviço][mao-propria-mp] adicional pelo qual o remetente recebe a garantia de que o objeto, por ele postado sob Registro, será entregue somente ao próprio destinatário, através da confirmação de sua identidade

### • **Utilizar Serviço de Aviso de Recebimento**

É o [serviço][aviso-de-recebimento-ar] adicional que, por meio do preenchimento de formulário próprio, físico ou digital, permite comprovar, junto ao remetente, a entrega do objeto.

### • **Utilizar Serviço de Valor Declarado**

É o [serviço][valor-declarado] adicional que garante o valor real do objeto postado sob registro em caso eventual de avaria ou extravio.

## Quais os recursos do módulo

- [✓] Cálculo do frete
- [✓] Rastreamento
- [✓] Notificação automática do rastreamento
- [✓] Impressão de etiquetas

## Perguntas mais frequentes "FAQ"

### Como usar o recurso de Impressão de etiquetas

--

O módulo oferece a integração com os serviços do SIGEP Web do Correios, possibilitando a organização das postagens da sua empresa.

Para ter acesso a este serviço será necessário:

Possuir contrato com o Correios.

Solicitar ao representante comercial da ECT permissão de acesso para utilização do Web Service através de login e senha.

Você não pode gerar etiquetas usando o servidor de homologação dos Correios. Então você vai precisar de um usuário e senha real (que você consegue com o Correios).

--

No Magento, na configuração do método do Correios temos um bloco relativo a "Configurações SIGEP"

Onde deve ser feito o devido preenchimento

Na visualização do pedido é exibido o bloco "Correios SIGEP", informe as dimensões da embalagem e em seguida clique em "Imprimir etiqueta"

--

Para mais informações sobre o SIGEP Web, acesse

http://www.correios.com.br/para-sua-empresa/encomendas/sigep-web

http://www.corporativo.correios.com.br/encomendas/sigepweb/doc/Manual_do_Usuario_SigepWeb.pdf

### Como conferir os valores dos fretes junto a transportada

Você pode visualizar no log os parâmetros enviado a transportada

Quando finalizado o pedido é armazenado no historico as dimensões da caixa que foi usada para o obter o frete

#### Simulação da requisição do preço

Ao efetuar o calculo do frete do produto

É usado as dimensões da embalagem para cálculo do peso cúbico

Caso o valor do peso cúbico seja maior que o peso esse deve ser enviado

A fórmula do peso cúbico é "(largura_embalagem)×(comprimento_embalagem)×(altura_embalagem)/coeficiente" sendo o coeficiente 6000 

Temos o devido retorno ao processar a seguinte requisição 

	curl --header 'Content-Type: text/xml;charset=UTF-8' --header 'CalcPrecoPrazo' --data '<?xml version="1.0" encoding="UTF-8"?>
	<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://tempuri.org/">
	<SOAP-ENV:Body>
	    <ns1:CalcPrecoPrazo>
	        <ns1:nCdEmpresa />
	        <ns1:sDsSenha />
	        <ns1:nCdServico>40045</ns1:nCdServico>
	        <ns1:sCepOrigem>08215430</ns1:sCepOrigem>
	        <ns1:sCepDestino>08215430</ns1:sCepDestino>
	        <ns1:nVlPeso>1.05</ns1:nVlPeso>
	        <ns1:nCdFormato>1</ns1:nCdFormato>
	        <ns1:nVlComprimento>18</ns1:nVlComprimento>
	        <ns1:nVlAltura>9</ns1:nVlAltura>
	        <ns1:nVlLargura>14</ns1:nVlLargura>
	        <ns1:nVlDiametro>0</ns1:nVlDiametro>
	        <ns1:sCdMaoPropria>N</ns1:sCdMaoPropria>
	        <ns1:nVlValorDeclarado>0</ns1:nVlValorDeclarado>
	        <ns1:sCdAvisoRecebimento>N</ns1:sCdAvisoRecebimento>
	    </ns1:CalcPrecoPrazo>
	</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>' http://ws.correios.com.br/calculador/CalcPrecoPrazo.asmx?WSDL

ou

	http://wsdlbrowser.com/soapclient?wsdl_url=http%3A%2F%2Fws.correios.com.br%2Fcalculador%2FCalcPrecoPrazo.asmx%3FWSDL&function_name=CalcPrecoPrazo

#### Simulação da requisição da consulta

Temos o devido retorno ao processar a seguinte requisição 

	curl --header 'Content-Type: text/xml;charset=UTF-8' --header 'SOAPAction:buscaEventos' --data '<?xml version="1.0" encoding="UTF-8"?>
	<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://resource.webservice.correios.com.br/">
	<SOAP-ENV:Body>
	    <ns1:buscaEventos>
	        <usuario>ECT</usuario>
	        <senha>SRO</senha>
	        <tipo>L</tipo>
	        <resultado>T</resultado>
	        <lingua>101</lingua>
	        <objetos>PG781754484BR</objetos>
	    </ns1:buscaEventos>
	</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>' http://webservice.correios.com.br/service/rastro/Rastro.wsdl

ou

	http://wsdlbrowser.com/soapclient?wsdl_url=http%3A%2F%2Fwebservice.correios.com.br%2Fservice%2Frastro%2FRastro.wsdl&function_name=buscaEventos

#### Simulação de autenticação SIGEP

Nesse caso usando a URL do ambiente de teste

Para o ambiente de produção deve ser usado 

https://apps.correios.com.br/SigepMasterJPA/AtendeClienteService/AtendeCliente?wsdl

Temos o devido retorno ao processar a seguinte requisição 

	curl --header 'Content-Type: text/xml;charset=UTF-8' --header 'verificaDisponibilidadeServico' --data '<?xml version="1.0" encoding="UTF-8"?>
	<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://cliente.bean.master.sigep.bsb.correios.com.br/">
	  <SOAP-ENV:Body>
	    <ns1:verificaDisponibilidadeServico>
	      <codAdministrativo>08082650</codAdministrativo>
	      <numeroServico>40215</numeroServico>
	      <cepOrigem>70002900</cepOrigem>
	      <cepDestino>81350120</cepDestino>
	      <usuario>sigep</usuario>
	      <senha>n5f9t8</senha>
	    </ns1:verificaDisponibilidadeServico>
	  </SOAP-ENV:Body>
	</SOAP-ENV:Envelope>' --insecure https://apphom.correios.com.br/SigepMasterJPA/AtendeClienteService/AtendeCliente?wsdl

ou

	http://wsdlbrowser.com/soapclient?wsdl_url=https%3A%2F%2Fapphom.correios.com.br%2FSigepMasterJPA%2FAtendeClienteService%2FAtendeCliente%3Fwsdl&function_name=verificaDisponibilidadeServico

#### Simulação de solicitaEtiquetas SIGEP

Temos o devido retorno ao processar a seguinte requisição 

	curl --header 'Content-Type: text/xml;charset=UTF-8' --header 'verificaDisponibilidadeServico' --data '<?xml version="1.0" encoding="UTF-8"?>
	<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://cliente.bean.master.sigep.bsb.correios.com.br/">
	<SOAP-ENV:Body>
	<ns1:solicitaEtiquetas>
	  <tipoDestinatario>C</tipoDestinatario>
	  <identificador>?CNPJ?</identificador>
	  <idServico>104625</idServico>
	  <qtdEtiquetas>1</qtdEtiquetas>
	  <usuario>?</usuario>
	  <senha>?</senha>
	</ns1:solicitaEtiquetas>
	</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>' --insecure https://apps.correios.com.br/SigepMasterJPA/AtendeClienteService/AtendeCliente?wsdl

ou

	http://wsdlbrowser.com/soapclient?wsdl_url=https%3A%2F%2Fapphom.correios.com.br%2FSigepMasterJPA%2FAtendeClienteService%2FAtendeCliente%3Fwsdl&function_name=solicitaEtiquetas

### Como é feito o cálculo de preços

[Clique aqui][encomendas-prazo] para calcular o preço da encomenda o sistema utiliza a distância origem/destino(CEP), o peso e as dimensões do objeto, aplicando a seguinte fórmula relativa a peso cúbico:

	(Comprimento x Altura x Largura)/6000cm³

O preço adotado pelo sistema será o maior entre o peso cúbico e peso real.

### Como aplicar o Frete Grátis

Na configuração do módulo para o método de entrega é possível definir o "Serviço Para Entrega Gratuita" recurso que deve ser aplicado quando definido a ação de "Frete Grátis" nas "Regras da Promoção"

No Backend do Magento, acesse o menu: Promoções -> Regras de Promoção -> Criar regra -> Crie uma regra e defina na aba "Ações" o uso do Frete Grátis

Dessa forma na exibição do cálculo do frete será exibido para o serviço escolhido o valor zerado

Esse recurso se trata de regra nativa do Magento caso tenha algum problema sugiro desativar todas as regras de promoção e ativar uma de cada vez até encontrar o motivo da ocorrência

### Método retornando: "Peso excedido"
### Método retornando: "Dimensões dos produtos fora do permitido"

No link a seguir vemos os [limites de dimensões e de peso][limites-de-dimensoes-e-de-peso]

### Dados de contato - Correios

Para entrar em contato com o [Correios][contact-correios]

## Manual

http://www.correios.com.br/para-voce/correios-de-a-a-z/pdf/calculador-remoto-de-precos-e-prazos/manual-de-implementacao-do-calculo-remoto-de-precos-e-prazos

http://blog.correios.com.br/comercioeletronico/wp-content/uploads/2011/10/Guia-Tecnico-Rastreamento-XML-Cliente-Vers%C3%A3o-e-commerce-v-1-5.pdf

http://blog.correios.com.br/comercioeletronico/

http://blog.correios.com.br/comercioeletronico/?p=404

http://blog.correios.com.br/comercioeletronico/?p=155

http://www.correios.com.br/encomendas/prazo/Formato.cfm

http://www.correios.com.br/produtosaz/produto.cfm?id=8560360B-5056-9163-895DA62922306ECA

http://www.correios.com.br/para-sua-empresa/encomendas/sigep-web

http://www.corporativo.correios.com.br/encomendas/sigepweb/doc/Manual_do_Usuario_SigepWeb.pdf

http://www2.correios.com.br/hotsites/ecommerce/

:cat2:
