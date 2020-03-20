## Questão 1

Para utilizar a data de hoje e para a data incluida ser "Bloco inicial da koreCoin" , mudamos:


```javascript
createGenesisBlock(){
        return new Block(0, "02/01/2018", "Genesis Block", "0");
    }
```

para:

```javascript
 createGenesisBlock(){
        return new Block(0, Date(), "Bloco inicial da koreCoin", "0");
    }
```

Sendo que ```javascript Date()``` 

O output será algo assim:
