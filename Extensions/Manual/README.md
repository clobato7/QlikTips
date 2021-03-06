# Desenvolvimento de extensões para o Qlik Sense

Este artigo tem como objetivo exemplificar e detalhar alguns passos e tecnicas que podem ser utilizados durante o processo de criação de uma extensão qualquer.

# Estrutura do código padrão

## Função Paint
A função paint é a responsável por manipular o que será exibido e como será exibido na sua extensão. Toda vez que tiver alguma alteração na extensão (ex: largura, altura, posicionamento, etc), esta função será executada.

 **<em>Dica: cuide com o que irá fazer e chamar dentro desta função, pois poderá sobrecarregar o processamento, deixando sua extensão/aplicação lenta.</em>**

 ## Função Definition
 A função definition é a responsável pelas definições da sua extensão (ex: as seções são definidas nesta parte).

# Seção
Uma seção é o componente responsável por organizar as configurações da extensão (cores, medidas, dimensões, classificação, etc.). A seção fica dentro do menu lateral direito.

Para acrescentar seções de sua extensão, deve ser declarado a função? definition: {} acima de paint: {}

## Tipos de Seções

Existem alguns tipos de seções pré-definidas pela Qlik, que são:

### Aparência
```javascript
var aparencia = {
	uses: "settings"
};
```
> ![Aparencia](https://github.com/jjonasramos/QlikTips/blob/master/Extensions/Manual/assets/images/aparencia.PNG)

### Dados
```javascript
var dados = {
	uses: "data"
};
```
> ![Dados](https://github.com/jjonasramos/QlikTips/blob/master/Extensions/Manual/assets/images/dados.PNG)

### Medidas
```javascript
var medida = { 
        uses: "measures",
	min: 0,
	max: 1
};
```
> ![Medida](https://github.com/jjonasramos/QlikTips/blob/master/Extensions/Manual/assets/images/medida.PNG)

### Dimensões
```javascript
var dimensão = {
	uses: "dimensions",
	min: 0,
	max: 1
};
```
> ![Dimensão](https://github.com/jjonasramos/QlikTips/blob/master/Extensions/Manual/assets/images/dimensao.PNG)


## Criando seções customizadas

Primeiro criamos o header1.

```javascript
var header1 = {
	ref: "item1",
	label: "Expressão",
	type: "string",
	expression: "optional"
};
```

Depois criamos uma seção. Não é necessário definir o **type**, pois o componente "expandable-items" já define isso automaticamente.

```javascript
var minhaSecao = {
	component: "expandable-items",
        label: "Minha Seção",
        items: {
		h1: {
			type: "items",
			label: "Header 1",
                	items: {
                    		header1,
                    		header2
                	}
            	}            
        }
};
```
> ![Custom Section](https://github.com/jjonasramos/QlikTips/blob/master/Extensions/Manual/assets/images/custom_section.PNG)
