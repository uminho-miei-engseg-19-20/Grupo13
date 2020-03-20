## Questão 1

#### 1.1

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

#### 1.2

Para adicionar novos blocos apenas temos de invocar a função addBlock(), e introduzir os dados necessários, neste caso, o index, o timestamp e a os dados associados

```javascript
koreCoin.addBlock(new Block (1, "01/01/2018", {amount: 20}));
koreCoin.addBlock(new Block (2, "02/01/2018", {amount: 40}));
koreCoin.addBlock(new Block (3, "02/01/2018", {amount: 40}));
//novos blocos
koreCoin.addBlock(new Block (4, Date(), {amount: 100}));
koreCoin.addBlock(new Block (5, Date(), {amount: 200}));
koreCoin.addBlock(new Block (5, Date(), {amount: 200}));
``` 

O output:

```bash
{
    "chain": [
        {
            "index": 0,
            "timestamp": "Fri Mar 20 2020 21:46:22 GMT+0000 (GMT)",
            "data": "Bloco inicial da koreCoin",
            "previousHash": "0",
            "hash": "9b484af541bea8fd64a71748e5f4c5c948c8c30271fb8b4a3d87e697fb9ac4db"
        },
        {
            "index": 1,
            "timestamp": "01/01/2018",
            "data": {
                "amount": 20
            },
            "previousHash": "9b484af541bea8fd64a71748e5f4c5c948c8c30271fb8b4a3d87e697fb9ac4db",
            "hash": "3628885b4d3b93082db9c7c9dd1d0370f9fd481e5a04bf36be4fdc84982db99e"
        },
        {
            "index": 2,
            "timestamp": "02/01/2018",
            "data": {
                "amount": 40
            },
            "previousHash": "3628885b4d3b93082db9c7c9dd1d0370f9fd481e5a04bf36be4fdc84982db99e",
            "hash": "6598fa0e526f13f6b6903e87ac00df117bffc422f4c90ebcf9b0774ed697a227"
        },
        {
            "index": 3,
            "timestamp": "02/01/2018",
            "data": {
                "amount": 40
            },
            "previousHash": "6598fa0e526f13f6b6903e87ac00df117bffc422f4c90ebcf9b0774ed697a227",
            "hash": "93091a951bd37c1fb323215ced0ae9d1515917c335ac76d0df90939157342fa5"
        },
        {
            "index": 4,
            "timestamp": "Fri Mar 20 2020 21:46:22 GMT+0000 (GMT)",
            "data": {
                "amount": 100
            },
            "previousHash": "93091a951bd37c1fb323215ced0ae9d1515917c335ac76d0df90939157342fa5",
            "hash": "fa170eda0075f42607900ad4e3d13b1baa66e139c7e278cc1a8bfcc146223f31"
        },
        {
            "index": 5,
            "timestamp": "Fri Mar 20 2020 21:46:22 GMT+0000 (GMT)",
            "data": {
                "amount": 200
            },
            "previousHash": "fa170eda0075f42607900ad4e3d13b1baa66e139c7e278cc1a8bfcc146223f31",
            "hash": "85a9a22b1c14c680a7d9bf1fe5a6478edbd243a02fa56a276f3b8946db417ad0"
        },
        {
            "index": 5,
            "timestamp": "Fri Mar 20 2020 21:46:22 GMT+0000 (GMT)",
            "data": {
                "amount": 200
            },
            "previousHash": "85a9a22b1c14c680a7d9bf1fe5a6478edbd243a02fa56a276f3b8946db417ad0",
            "hash": "efb3d7e4ef417d8b43ca8d1a3195dfc77bcaf7de59d71a165694bf6dadd37067"
        }
    ]
}
```

