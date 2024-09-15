### Questão 1
Observe o trecho de código:

int INDICE = 12, SOMA = 0, K = 1;

enquanto K < INDICE faça

{ K = K + 1; SOMA = SOMA + K;}

imprimir(SOMA);


Ao final do processamento, qual será o valor da variável SOMA?

### Resposta = 77

***

### Questão 2
Descubra a lógica e complete o próximo elemento:

a) 1, 3, 5, 7, ___

b) 2, 4, 8, 16, 32, 64, ____

c) 0, 1, 4, 9, 16, 25, 36, ____

d) 4, 16, 36, 64, ____

e) 1, 1, 2, 3, 5, 8, ____

f) 2,10, 12, 16, 17, 18, 19, ____

### Resposta

a) **<u>9</u>** => números impares

b) **<u>128</u>** => o dobro do número anterior

c) **<u>49</u>** => soma o número impar na posição correspondente para gerar o proximo número 

d) **<u>100</u>** => números pares ao quadrado

e) **<u>13</u>** => Fibonacci

f) **<u>200</u>** => números que começa com a letra D

***

### Questão 3
Dado um vetor que guarda o valor de faturamento diário de uma distribuidora de todos os dias de um ano, faça um programa, na linguagem que desejar, que calcule e retorne:

- O menor valor de faturamento ocorrido em um dia do ano;
- O maior valor de faturamento ocorrido em um dia do ano;
- Número de dias no ano em que o valor de faturamento diário foi superior à média anual.

a) Considerar o vetor já carregado com as informações de valor de faturamento.

b) Podem existir dias sem faturamento, como nos finais de semana e feriados. Estes dias devem ser ignorados no cálculo da média.

c) Utilize o algoritmo mais veloz que puder defini

### Resposta
```ts
type Resposta = {
    menorFaturamento: number
    maiorFaturamento: number
    diasAcimaDaMedia: number
}

function calcResposta(faturamentoDiario: (number | undefined)[]): Resposta {
    let soma = 0;
    let count = 0;

    for (const valor of faturamentoDiario) {
        if (valor) {
            soma += valor;
            count++;
        }
    }

    const media = count > 0 ? soma / count : 0;

    const resposta = faturamentoDiario.reduce((acc, faturamento) => {

        if (!faturamento) {
            return acc
        }

        if (!acc.menorFaturamento || faturamento < acc.menorFaturamento) {
            acc.menorFaturamento = faturamento
        }

        if (!acc.maiorFaturamento || faturamento > acc.maiorFaturamento) {
            acc.maiorFaturamento = faturamento
        }

        if (faturamento > media) {
            acc.diasAcimaDaMedia += 1
        }


        return acc

    }, { diasAcimaDaMedia: 0 } as Resposta)

    return resposta
}
```

***

### Questão 4
Uma empresa solicitou a você um aplicativo para manutenção de um cadastro de clientes. Após a reunião de definição dos requisitos, as conclusões foram as seguintes:

- Um cliente pode ter um número ilimitado de telefones;
- Cada telefone de cliente tem um tipo, por exemplo: comercial, residencial, celular, etc. O sistema deve permitir cadastrar novos tipos de telefone;
- A princípio, é necessário saber apenas em qual estado brasileiro cada cliente se encontra. O sistema deve permitir cadastrar novos estados;

Você ficou responsável pela parte da estrutura de banco de dados que será usada pelo aplicativo. Assim sendo:

- Proponha um modelo lógico para o banco de dados que vai atender a aplicação. Desenhe as tabelas necessárias, os campos de cada uma e marque com setas os relacionamentos existentes entre as tabelas;
- Aponte os campos que são chave primária (PK) e chave estrangeira (FK);
- Faça uma busca utilizando comando SQL que traga o código, a razão social e o(s) telefone(s) de todos os clientes do estado de São Paulo (código “SP”);

### Resposta

![diagram](https://github.com/EdmilsonESF/target-sistemas/blob/main/db_diagram.png?raw=true)

### Query SQL
```sql
SELECT estado.codigo, usuario.razao_social, ARRAY_AGG(telefone.numero) AS telefones
FROM estado
LEFT JOIN usuario ON usuario.estado_id = estado.id
LEFT JOIN telefone ON telefone.usuario_id = usuario.id
WHERE estado.codigo = 'SP'
GROUP BY estado.codigo, usuario.id;
```

***

### Questão 5
Dois veículos, um carro e um caminhão, saem respectivamente de cidades opostas pela mesma rodovia. O carro, de Ribeirão Preto em direção a Barretos, a uma velocidade constante de 90 km/h, e o caminhão, de Barretos em direção a Ribeirão Preto, a uma velocidade constante de 80 km/h. Quando eles se cruzarem no percurso, qual estará mais próximo da cidade de Ribeirão Preto?

a) Considerar a distância de 125km entre a cidade de Ribeirão Preto <-> Barretos.
b) Considerar 3 pedágios como obstáculo e que o carro leva 5 minutos a mais para passar em cada um deles, pois ele não possui dispositivo de cobrança de pedágio.
c)Explique como chegou no resultado.

### Resposta:
#### Informações fornecidas:
- **Distância total** entre as cidades: 125 km
- **Velocidade do carro**: 90 km/h
- **Velocidade do caminhão**: 80 km/h
- **Obstáculos**: O carro leva 5 minutos a mais em cada pedágio (3 pedágios).

Podemos considerar que o caminhão saiu 15 minutos antes do carro, devido aos pedágios

#### 1. Distância que o caminhão percorre a mais
Distância = 80km/h * 0.25h = 20km

#### 2. Tempo até o encontro

A soma das velocidades dos veículos, como eles estão indo um em direção ao outro, é:

90km/h+80km/h=170km/h

O tempo até eles se encontrarem após o caminhão ércorrer 20km pode ser calculado pela fórmula:

Tempo = (105km/170km/h) ≈ 37 minutos

#### 3. Distância percorrida por cada veículo até o encontro

- **Distância percorrida pelo carro** em 37 minutos:

Distância do carro = 90km/h × 0,617hora ≈ 55,5km

- **Distância percorrida pelo caminhão** em 37 minutos:

Distância do caminhão = 80km/h × 0,617horas ≈ 49.5km

#### 4. Resultado final

- **Distância do carro até Ribeirão Preto** no momento do encontro: 55,5 km
- **Distância do caminhão até Ribeirão Preto** no momento do encontro: 
125km - 49,5km + 20km = 95,5km

#### Conclusão

No momento em que os veículos se cruzarem, o **carro estará mais próximo de Ribeirão Preto**.
