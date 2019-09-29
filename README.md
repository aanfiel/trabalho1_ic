# Projetos de inteligência artificial
## Este repositório hospeda os trabalhos realizados durante os estudos de Inteligência Artificial

### 29/09/2019: Trabalho 1 de inteligência computacional

1. Encontre o máximo da função f(x,y) = |xsen(yπ/4) + ysen(xπ/4)| por meio do algoritmo hill-climbing. As variáveis x e y pertencem ao intervalo entre 0 e 20. Os vizinhos de determinado estado (x, y) são (x, y ± 0,01), (x ± 0,01, y) e (x ± 0,01, y ±
0,01). Por exemplo, os vizinhos do estado (1,00; 1,00) são (1,00; 1,01), (1,01; 1,01), (0,99; 0,99), (0,99; 1,00) etc.

2. Construa um programa baseado em lógica fuzzy (inferência de Mamdani) que receba três valores: pressão no pedal, velocidade da roda e velocidade do carro e que devolva a pressão no freio. Siga as regras disponibilizadas nos slides sobre Lógica Fuzzy.

3. Usando o conjunto de dados do aerogerador (variável de entrada: velocidade do vento – m/s, variável de saída: potência gerada – kWatts), determine os modelos de regressão polinomial (graus 2, 3, 4 e 5) com parâmetros estimados pelo método dos mínimos quadrados.
Avalie a qualidade de cada modelo pela métrica R2 e R2aj (equações 48 e 49, slides sobre Regressão Múltipla).

### Observações:

* Elabore um pequeno relatório sobre os resultados obtidos. 
* As implementações devem ser em C, Java, Python ou Matlab/Scilab. 

## Questão 1

### Iniciando 
Para a resolução desta questão foram usados dois arquivos:

* [questao1.sce](questao1.sce) - Código-fonte da aplicação proposta na questão
* *relatorio_q1.pdf* - Relatório descritivo dos resultados obtidos 

### Construído em

* [Scilab 6.0.2](https://www.scilab.org/) - Software open source para computação numérica
* [Linux Mint 19.2 Tina](https://www.linuxmint.com/) - Sistema operacional usado

## Autor

* **José Lopes de S. Filho** - [LinkedIn](https://www.linkedin.com/in/joselopesfilho/)
* *Engenharia da Computação (UFC) - Matrícula # 389097*

## Licença

Este projeto é licenciado sob a MIT License - ver o arquivo [LICENSE.md](LICENSE.md) para detalhes

## Código comentado

### Parte 1: Criação das matrizes
Primeiramente, foram criados os dados dos dois eixos *x* e *y*. Após a limpeza das variáveis armazenadas e do console para evitar possíveis conflitos, em seguida foram criados doid vetores com valores de 0 a 20 a intervalos de 0,01.
```
clear; // Limpa as variáveis armazenadas
clc; // Limpa o console

// Cria um vetor coluna de valores 0 a 20 com passo 0,01 e os atribui as variáveis x e y
x=[0: 0.01 : 20]';
y=[0: 0.01 : 20]';
```
### Parte 2: Definição da função solicitada
Em seguida, foi criado o vetor *z* com os valores de acordo com a função solicitada na questão.

```
// Cria uma função f(x,y) = |xsen(y.pi/4)+ysen(x.pi/4)| e a atribui a z
z=abs((x.*sin(y.*%pi/4))+(y.*sin(x.*%pi/4)));
```
### Parte 3: Plotagem do gráfico da função
No código abaixo, a janela gráfica é limpa, o gráfico da função solicitada na questão é plotado com os eixos e título do gráfico atribuídos.

```
clf; // Limpa a janela gráfica
plot3d(x,y,z)
xtitle('Gráfico da questão 1', 'Eixo X', 'Eixo Y', 'Eixo Z = f(x,y)');
```
### Parte 4: Implementação do algoritmo hill climbing
De início, gera-se um número aleatório entre 1 e o tamanho do vetor *z*

```
n=grand(1,1,"uin",1,size(z, "r"));
```
Em seguida, criou-se um laço while que irá durar enquanto o valor de *n* for menor ou igual ao tamanho máximo do vetor *z*.
```
while n<=size(z, "r") do
```
Foi criada uma variável para armazenar o valor de cada elemento do vetor *z* por iteração.
```
maior = z(n);
```
Nesse momento, iniciam-se os testes de valor - Para cada situação prevista, o algoritmo deve ter um dado comportamento. Analisemos cada uma delas:

Para o primeiro caso, se *n* for maior que 1 *(ou seja: não for o primeiro elemento do vetor - pois se fosse, ele poderia voltar a um elemento não existente e retornar erro)* e for menor que seu elemento anterior, atribua ao elemento anterior à variável *maior* e faça com que *n* volte 1 elemento no vetor.
```
    if(n>1 & maior < z(n-1))
        maior = z(n-1);
        n=n-1;
 ```
 Se *n* for menor que o tamanho máximo do vetor *(ou seja: se ele nao for o último elemento do vetor - pois se fosse, ele avançaria a um elemento não existente e retornaria erro)* e seu valor for menor que o do elemento posterior, atribua o valor da frente à variável *maior* e faça com que *n* avance 1 elemento no vetor.
 ```
    elseif(n<size(z, "r") & maior < z(n+1))
        maior = z(n+1);
        n=n+1;
  ```
  
    elseif(n==1)
        if(maior < z(n+1))
            maior = z(n+1);
            n=n+1;
        else
            disp(maior, n, "Máximo valor local da função: ");
            break
        end
    elseif(n==size(z, "r"))
        if(maior < z(n-1))
            maior = z(n-1);
            n=n-1;
        else
            disp(maior, n, "Máximo valor local da função: ");
            break
        end
    else
        disp(maior,n,"Máximo valor local da função: ");
        break
    end
end
