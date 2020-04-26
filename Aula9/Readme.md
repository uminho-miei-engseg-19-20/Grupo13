## Pergunta 1


### Pergunta 1.1


O algoritmo tem o comportamento de armazenar numa lista(buffer) uma quantidade   
de numeros que são pedidos no inicio tantos numeros quantos aqueles que são colocados.   
Comparando o mesmo programa em três línguas distintas, verificamos essencialmente diferenças que caracterizam cada linguagem.   
Além disso, é possível verificar a existencia de erros na execuçao de cada um dos ficheiros.   
Mas ambos tem um problema em comum, a falta de um verificador no primeiro input colocado pelo user,   
visto que este está relacionado com a primeira variável do tipo inteiro, pois esta   
determina  o numero máximo de números no buffer.  
1º cria um buffer de tamanho 10  
2º recebe um input de numeros que queremos colocar nesse buffer.  
3º Na execuçao, se colocar-mos um valor superior a 10 numeros, o programa devolverá um erro de index, neste caso index fora de range.  

![image1.1](Imagens/overflow.png)



#### Java

No programa java foram observadas as seguintes exceçoes:  

Ao introduzir um inteiro superior a 10 no primeiro input, ao chegar ao 11 elemento, obtemos a seguinte exceção:  
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 10 out of bounds for length 10  
Variavel inicial que impossibilita inserir além do tamanho do buffer.  
  
Ao introduzir um numero com mais de 10 digitos, obtemos a seguinte exceção:  
Exception in thread "main" java.util.InputMismatchException:   
Isto deve-se ao fato de se tratar de um numero superior a 10.  

Ao introduzir um numero negativa, observamos que o programa é terminado de imediato.  
Visto que o valor é negativo no count, logo não entra no ciclo.  

Ocorreram outros problemas mas todos semelhantes aos já apresentados.  



#### Python



Ao introduzir valores além do tamanho da lista,mais de 10 numeros, obtemos esta exceção:  
IndexError: list assignment index out of range  
Deve-se ao fato de existir uma variável inicial que indica o tamanho do buffer como sendo de 10 posiçoes e nada mais que isso.  
 
Ao introduzir valores de comprimento exagerado observamos que não ocorre qualquer erro ou exceção, diferente da versão em java.  
Tal ocorrencia, deve-se pelo fato que os numeros inteiros Python tem uma precisao arbitraria, deste modo a possibilidade de Overflow é nula.  



Ao introduzir um valor exagerado no primeiro input, obtemos este erro:  
OverflowError: range() result has too many items  
Acontece pois o range() acaba por devolver demasiados resultados possíveis, logo havendo Overflow.  

Ao inserir valor negativo o programa termina de imediato.  
  
Além destes, também foi possível observar que era possível chamar funçoes no input do programa,  
sendo este, talvéz a parte mais suscetível em termos de segurança.  




#### C++



Aqui como nos outros é verificado praticamente os mesmos erros e exceçoes que os exemplos anteriores.   
Entre eles, o Overflow de inteiros, a introduçao de numeros negativos, inserçao de valores alem do indice 10 do buffer  
 e por ultimo a quantidade de digitos que um input pode ter, estando entre 0 e 10 digitos.  


Com esta analise, podemos concluir que a falta de verificadores de input está presente em ambos os exemplos,   
os erros apresentados são bastante semelhantes mesmo tratando-se de 3 linguagens distintas e por ultimo   
é possível verificar diversos cenários que apresentam possíveis vulnerabilidades.  



### Pergunta 1.2 – Buffer Overflow

Inicialmente é necessario analisar os scripts de modo a conseguir apurar qual a vulnerabilidade  
de Buffer Overflow existente e ainda o que tem de se fazer para explorar e obter as respetivas confirmaçoes e mensagens.  
Numa primeira execuçao do programa a IDE informa-nos do uso de funçoes “gets”,   
sendo estas perigosas e que não deveriam ser utilizadas. Desde logo,   
verificamos que a vulnerabilidade Stack Buffer Overflow está presente em ambos.  

#### RootExploit.C

**Variaveis:**
	o programa consta com duas variaveis:  
		- pass é usada no controlo de acesso root/admin.     
		- buff é usada para armazenar a password introduzida pelo utilizador.  

**Input:**
	o programa solicita que o utilizador insira uma password de root, usando a funçao gets  

**Verificação:**
	o programa compara essa password(string) com csi1(string), csi1 corresponde à password válida.  
	Só serão dadas as permissoes de root/admin, quando pass tiver valor 1.  

Com isto já podemos tirar algumas conclusoes, as variaveis inicialmente declaradas quando carregadas  
 para a stack vão do endereço mais alto para o mais baixo. Mas a escrita é feita no sentido contrario.   
Logo é possível ver que a variável pass encontra-se em cima do buff.  

![imagestack](Imagens/stack.png)



Deste modo, é possível verificar o espaço que a variável pass vai tomar, neste caso 4 bytes e a variável buff ocupa os 4 bytes seguintes.   
No caso da escrita continuar, o programa consequentemnete acaba por passar fora dos limites estabelecidos para a variável buff,   
assim sendo é possível alterar o valor da variável pass. Seguindo esta logica, o input sendo superior a 4 carateres,   
causamos um Buffer Overflow, na variável pass. e por ultimo, tendo em atençao que o ultimo caracter no caso de usarmos 5 bytes,   
o ultimo caracter tem de ser diferente de “0”. Se forem cumpridas todas estas condiçoes,  
é possível obter a confirmaçao que “Foram-lhe atribuidas permissoes de root/admin”.  
Com a imagem a baixo é possível observar o feito.  

![imageroot](Imagens/root.png)



#### O-simple.c

Como já referido, este também sofre do mesmo problema que o RootExploit   
(tanto no uso da função gets como na permissão de ir para alem do tamanho do buffer).   
Logo o conceito de exploração é semelhante apenas diverge no valor da variável buffer,   
que neste caso é 64. Dito isto, ao excedermos esse tanto de espaço de memoria da variável,   
conseguimos alterar o valor da variável acima(control) e obtemos o print (YOU WIN!!!).  

![imageroot](Imagens/youwin.png)
