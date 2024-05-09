#include <stdio.h>
#include <stdlib.h>

// Definição da estrutura da célula da lista encadeada
struct reg {
    int conteudo;
    struct reg *prox;
};
typedef struct reg celula;

// Função para imprimir todos os valores da lista
void imprimirLista(celula *inicio) {
    celula *atual = inicio;
    while (atual != NULL) {
        printf("%d ", atual->conteudo);
        atual = atual->prox;
    }
    printf("\n");
}

// Função para remover os elementos da lista e liberar memória
void removerLista(celula *inicio) {
    celula *atual = inicio;
    while (atual != NULL) {
        celula *prox = atual->prox;
        free(atual); // libera a memória alocada para a célula atual
        atual = prox;
    }
}

int main() {
    // Criação de três instâncias da célula
    celula c1, c2, c3;
    
    // Atribuição de valores para cada célula
    c1.conteudo = 10;
    c2.conteudo = 20;
    c3.conteudo = 30;
    
    // Ligação entre as células para formar a lista encadeada
    c1.prox = &c2;
    c2.prox = &c3;
    c3.prox = NULL;
    
    // Impressão dos valores da lista
    printf("Valores na lista: ");
    imprimirLista(&c1);
    
    // Remoção dos elementos da lista
    removerLista(&c1);
    
    // Cálculo da quantidade de memória gasta por cada instância da célula
    int tamanho_celula = sizeof(celula);
    printf("Tamanho de uma célula: %d bytes\n", tamanho_celula);
    
    // Cálculo do máximo de elementos possíveis na fila, considerando a memória disponível no computador
    // Suponhamos que temos 1GB de memória disponível
    long memoria_disponivel = 1024 * 1024 * 1024; // 1GB em bytes
    int max_elementos = memoria_disponivel / tamanho_celula;
    printf("Máximo de elementos na fila considerando 1GB de memória: %d\n", max_elementos);
    
    return 0;
}
