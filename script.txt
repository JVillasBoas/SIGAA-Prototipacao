var matrizesArmazenadas = [];
var operacoesArmazenadas = [];
var matrizResultado = [];
var contador = 0;

function lerMatriz(operacao) {
    var qtd_colunas = document.getElementById("qtd_colunas").value;
    var qtd_linhas = document.getElementById("qtd_linhas").value;
    var matriz_txt = document.getElementById("matriz_txt").value;
    console.log(matriz_txt)
    matriz_txt = matriz_txt.replace("\n", "");
    matriz_txt = matriz_txt.split(",");
    var matrizLocal = [];

    for(l=0;l<qtd_linhas;l++){
        matrizLocal[l] = [];
        for(c=0;c<qtd_colunas;c++){
            matrizLocal[l][c] = parseInt(matriz_txt[0]);
            matriz_txt.shift();
        }
    }
    document.getElementById("msg_erro").innerHTML = 'Matriz lida com sucesso! 😁';
    console.log(matrizLocal);
    matrizesArmazenadas.push({matriz: matrizLocal, linha: qtd_linhas, coluna: qtd_colunas});
    if(operacao != '0') {
      operacoesArmazenadas.push(operacao);  
    }
}

function somaMatriz() {
    var matriz1 = matrizesArmazenadas[0];
    var matriz2 = matrizesArmazenadas[1];
    var matrizResultadoTxt = "";
    matrizResultado = [];
    if(matriz1.linha != matriz2.linha || matriz1.coluna != matriz2.coluna){
        document.getElementById("msg_erro").innerHTML = 'Matrizes de tamanhos diferentes não são possíveis de somar. 😢';
    } else {
        for(l=0;l<matriz1.linha;l++){
            matrizResultado[l] = []
            for(c=0;c<matriz1.coluna;c++){
                matrizResultado[l][c] = matriz1.matriz[l][c] + matriz2.matriz[l][c];
                //console.log(matriz1.matriz[l][c] + " + " + matriz2.matriz[l][c] + " = " + matrizResultado[l][c]);
            }
            matrizResultadoTxt += matrizResultado[l] + "\n";
        }
        console.log(matrizResultado);
    }
    document.getElementById("qtd_linhas").value = matriz1.linha;
    document.getElementById("qtd_colunas").value = matriz2.coluna;
    document.getElementById("matriz_txt").value = matrizResultadoTxt;
    document.getElementById("msg_erro").innerHTML = 'Operação de adição realizada com sucesso! 😁';
    matrizesArmazenadas.splice(0,2);
}

function subtracaoMatriz() {
    var matriz1 = matrizesArmazenadas[0];
    var matriz2 = matrizesArmazenadas[1];
    var matrizResultadoTxt = "";
    matrizResultado = [];
    if(matriz1.linha != matriz2.linha || matriz1.coluna != matriz2.coluna){
        document.getElementById("msg_erro").innerHTML = 'Matrizes de tamanhos diferentes não são possíveis de subtrair. 😢';
    } else {
        for(l=0;l<matriz1.linha;l++){
            matrizResultado[l] = []
            for(c=0;c<matriz1.coluna;c++){
                matrizResultado[l][c] = matriz1.matriz[l][c] - matriz2.matriz[l][c];
                //console.log(matriz1.matriz[l][c] + " + " + matriz2.matriz[l][c] + " = " + matrizResultado[l][c]);
            }
            matrizResultadoTxt += matrizResultado[l] + "\n";
        }
        console.log(matrizResultado);
    }
    document.getElementById("qtd_linhas").value = matriz1.linha;
    document.getElementById("qtd_colunas").value = matriz2.coluna;
    document.getElementById("matriz_txt").value = matrizResultadoTxt;
    document.getElementById("msg_erro").innerHTML = 'Operação de subtração realizada com sucesso! 😁';
    matrizesArmazenadas.splice(0,2);
}

function multiplicacaoMatriz() {
    var matriz1 = matrizesArmazenadas[0];
    var matriz2 = matrizesArmazenadas[1];
    matrizResultado = [];
    var matrizResultadoTxt = "";
    if(matriz1.coluna != matriz2.linha) {
        document.getElementById("msg_erro").innerHTML = 'Para multiplicar duas matrizes é necessário que a coluna da matriz A seja equivalente a linha da matriz B. 😢';
    } else {
        for(n=0;n<matriz1.linha;n++) {
            matrizResultado[n] = [];
            for(l=0;l<matriz2.coluna;l++) {
                matrizResultado[n][l] = 0;
                for(c=0;c<matriz1.coluna;c++) {
                    matrizResultado[n][l] += matriz1.matriz[n][c] * matriz2.matriz[c][l];
                    //console.log(matriz1.matriz[n][c] + " * " + matriz2.matriz[c][l] + " = " + matrizResultado[n][l]);
                }
            }
            matrizResultadoTxt += matrizResultado[n] + "\n";
        }
        console.log(matrizResultado);
    }
    document.getElementById("qtd_linhas").value = matriz1.linha;
    document.getElementById("qtd_colunas").value = matriz2.coluna;
    document.getElementById("matriz_txt").value = matrizResultadoTxt;
    document.getElementById("msg_erro").innerHTML = 'Operação de multiplicação realizada com sucesso!';
    matrizesArmazenadas.splice(0,2);
}

function opostaMatriz() {
    var matrizResultadoTxt = "";
    var matriz = matrizesArmazenadas[0];
    matrizResultado = [];
    for(l=0;l<matriz.linha;l++) {
        matrizResultado[l] = [];
        for(c=0;c<matriz.coluna;c++) {
            matrizResultado[l][c] = matriz.matriz[l][c] * (-1);
            matrizResultadoTxt += matrizResultado[l][c] + ",";
        }
        matrizResultadoTxt += "\n";
    }
    document.getElementById("matriz_txt").value = matrizResultadoTxt;
    document.getElementById("msg_erro").innerHTML = 'Operação de oposta realizada com sucesso! 😁';
    matrizesArmazenadas.splice(0,2);
}

function transpostaMatriz() {
    var matriz = matrizesArmazenadas[0];
    var matrizResultadoTxt = "";
    matrizResultado = [];
    for(l=0;l<matriz.coluna;l++) {
        matrizResultado[l] = [];
        for(c=0;c<matriz.linha;c++) {
            matrizResultado[l][c] = matriz.matriz[c][l];
            matrizResultadoTxt += matrizResultado[l][c] + ",";
        }
        matrizResultadoTxt += "\n";
    }
    document.getElementById("matriz_txt").value = matrizResultadoTxt;
    document.getElementById("msg_erro").innerHTML = 'Operação de transposta realizada com sucesso! 😁';
    matrizesArmazenadas.splice(0,2);
}

function identidadeMatriz() {
    var qtd_linhas = document.getElementById("qtd_linhas").value;
    var qtd_colunas = document.getElementById("qtd_colunas").value;
    var matrizResultadoTxt = "";
    matrizResultado = [];
    if(qtd_linhas == qtd_colunas) {
        for(l=0;l<qtd_linhas;l++) {
            matrizResultado[l] = [];
            for(c=0;c<qtd_colunas;c++) {
                if(l == c) {
                    matrizResultado[l][c] = 1;
                } else {
                    matrizResultado[l][c] = 0;
                }
                matrizResultadoTxt += matrizResultado[l][c] + ",";
            }
            matrizResultadoTxt += "\n";
        }
        document.getElementById("matriz_txt").value = matrizResultadoTxt;
        document.getElementById("msg_erro").innerHTML = 'Matriz identidade gerada com sucesso! 😁';
    } else {
        document.getElementById("msg_erro").innerHTML = 'Matriz identidade só pode ser gerada para matrizes quadradas. 😢';
    }
}

function determinante(matriz, ordem) {
    det = 0;
    var diagonal1 = 1
    var diagonal2 = 1
    if(ordem == 1) {
        det = matriz.matriz[0][0];
    } else if(ordem == 2) {
        console.log('for')
        for(l=0;l<ordem;l++) {
            for(c=0;c<ordem;c++) {
                if(c == l) {
                    diagonal1 *= matriz.matriz[l][c];
                } else {
                    diagonal2 *= matriz.matriz[l][c];
                }
            }
        }
        det = diagonal1 - diagonal2;
    } else if (ordem == 3) {
        for(i=0;i<ordem;i++) {
            diagonal1 += (matriz.matriz[0][(0+i)%3] * matriz.matriz[1][(1+i)%3] * matriz.matriz[2][(2+i)%3]);
            diagonal2 += (matriz.matriz[0][(2+i)%3] * matriz.matriz[1][(1+i)%3] * matriz.matriz[2][(0+i)%3]);
        }
        det = diagonal1 - diagonal2
    }
    return det;
}

function adjunta(matriz, ordem) {
    var adjuntaMatriz = [];
    if (ordem == 2) {
        adjuntaMatriz[0] = [];
        adjuntaMatriz[1] = [];
        adjuntaMatriz[0][0] = matriz.matriz[1][1];
        adjuntaMatriz[1][0] = -matriz.matriz[0][1];
        adjuntaMatriz[0][1] = -matriz.matriz[1][0];
        adjuntaMatriz[1][1] = matriz.matriz[0][0];
    } else if (ordem == 3) {
        console.log('teste ordem 3');
        adjuntaMatriz[0] = [];
        adjuntaMatriz[1] = [];
        adjuntaMatriz[2] = [];
        adjuntaMatriz[0][0] = matriz.matriz[1][1] * matriz.matriz[2][2] - matriz.matriz[1][2] * matriz.matriz[2][1];
        adjuntaMatriz[1][0] = -(matriz.matriz[1][0] * matriz.matriz[2][2] - matriz.matriz[1][2] * matriz.matriz[2][0]);
        adjuntaMatriz[2][0] = matriz.matriz[1][0] * matriz.matriz[2][1] - matriz.matriz[1][1] * matriz.matriz[2][0];
        adjuntaMatriz[0][1] = -(matriz.matriz[0][1] * matriz.matriz[2][2] - matriz.matriz[0][2] * matriz.matriz[2][1]);
        adjuntaMatriz[1][1] = matriz.matriz[0][0] * matriz.matriz[2][2] - matriz.matriz[0][2] * matriz.matriz[2][0];
        adjuntaMatriz[2][1] = -(matriz.matriz[0][0] * matriz.matriz[2][1] - matriz.matriz[0][1] * matriz.matriz[2][0]);
        adjuntaMatriz[0][2] = matriz.matriz[0][1] * matriz.matriz[1][2] - matriz.matriz[0][2] * matriz.matriz[1][1];
        adjuntaMatriz[1][2] = -(matriz.matriz[0][0] * matriz.matriz[1][2] - matriz.matriz[0][2] * matriz.matriz[1][0]);
        adjuntaMatriz[2][2] = matriz.matriz[0][0] * matriz.matriz[1][1] - matriz.matriz[0][1] * matriz.matriz[1][0];
    }
    return adjuntaMatriz;
}

function inverteMatriz() {
    var matriz = matrizesArmazenadas[0];
    var matrizResultadoTxt = "";
    matrizResultado = [];
    if(matriz.linha != matriz.coluna) {
        document.getElementById("msg_erro").innerHTML = 'Matriz não é quadrada, não é possível inverter. 😢';
    } else {
        var det = determinante(matriz, matriz.linha);
        if(det == 0) {
            document.getElementById("msg_erro").innerHTML = 'Matriz não pode ser invertida, determinante igual a zero. 😢';
        } else {
            var adj = adjunta(matriz, matriz.linha);
            for(l=0;l<matriz.linha;l++) {
                matrizResultado[l] = [];
                for(c=0;c<matriz.coluna;c++) {
                    matrizResultado[l][c] = adj[l][c] / det;
                    matrizResultadoTxt += matrizResultado[l][c] + ",";
                }
                matrizResultadoTxt += "\n";
            }
            document.getElementById("matriz_txt").value = matrizResultadoTxt;
            document.getElementById("msg_erro").innerHTML = 'Matriz invertida com sucesso! 😁';
        }
    }
    matrizesArmazenadas.splice(0,2);
}



function efetuarOperacao() {
    switch(operacoesArmazenadas[contador]){
        case "adicao":
            lerMatriz('0');
            somaMatriz();
            break;
        case "subtracao":
            lerMatriz('0');
            subtracaoMatriz();
            break;
        case "multiplicacao":
            lerMatriz('0');
            multiplicacaoMatriz();
            break;
        case "oposta":
            opostaMatriz();
            break;
        case "transposta":
            transpostaMatriz();
            break;
        case "determinante":
            lerMatriz('0');
            if (document.getElementById("qtd_colunas").value == document.getElementById("qtd_linhas").value & document.getElementById("qtd_linhas").value > 0 & document.getElementById("qtd_linhas").value < 4) {
                determinante(matrizesArmazenadas[0], document.getElementById("qtd_colunas").value);
                document.getElementById("matriz_txt").value = det;
                document.getElementById("msg_erro").innerHTML = 'Determinante gerada com sucesso! 😁';
            } else {
                document.getElementById("msg_erro").innerHTML = 'A determinante da matriz só pode ser gerada para matrizes quadradas e neste site de ordem dois ou três. 😢';
            }
            matrizesArmazenadas.splice(0,2);
            break;
        case "inversa":
            inverteMatriz();
            break;
        // default:
        //     document.getElementById("msg_erro").innerHTML = 'Operação não selecionada. Selecione-a ou clique em <a href="url">Manual de instruções</a>';
    }
    contador++;
    console.log(operacoesArmazenadas);
    console.log(contador);
}
