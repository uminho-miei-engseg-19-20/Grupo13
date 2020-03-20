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

Sendo que ```Date()``` dá-nos o dia atual, e a hora.

O output será algo assim:

```bash
"chain": [
        {
            "index": 0,
            "timestamp": "Fri Mar 20 2020 21:31:19 GMT+0000 (GMT)",
            "data": "Bloco inicial da koreCoin",
            "previousHash": "0",
            "hash": "5373580d3e1a5ccd906bd11afb9b7a60f7937657023d1d929ec483c86969b1f3"
        },
```
