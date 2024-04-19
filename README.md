# Desvendando o Código: Uma Jornada pela Busca em Profundidade (DFS)

## O Cenário
Imagine um mapa, não um mapa qualquer, mas um mapa de cidades interconectadas por estradas. Cada cidade é um "nó" e cada estrada é uma "aresta". Este é o nosso grafo, o mundo que a DFS vai explorar.

## A Busca Começa (Função dfs)
- **Marcando o Território**: Ao chegar numa cidade (nó inicial), a primeira coisa que fazemos é marcá-la como visitada (`nos_visitados[inicial] = true`). Assim, não nos perdemos em círculos.
- **Anunciando a Chegada**: Com orgulho, anunciamos a cidade que acabamos de conquistar: `cout << inicial << " ";`.
- **Explorando os Arredores**: Para cada cidade vizinha (visinho) conectada por uma estrada (presente na lista `grafo[inicial]`), verificamos se já a visitamos.
- **Aventura Continua**: Se a cidade vizinha ainda não foi explorada (`!nos_visitados[visinho]`), embarcamos em uma nova jornada DFS a partir dela: `dfs(visinho, grafo, nos_visitados);`.

## Construindo o Mapa (Função main)
- **Lendo o Mapa**: Primeiro, precisamos saber quantas cidades (`num_nos`) e estradas (`num_arestas`) existem. Pedimos essa informação ao usuário.
- **Criando o Grafo**: Com um toque de magia, criamos nosso mapa (grafo) como uma lista de listas. Cada cidade tem sua própria lista de vizinhos.
- **Conectando as Cidades**: Lemos cada estrada (`u, v`) e registramos a conexão entre as cidades em ambas as direções: `grafo[u].push_back(v); grafo[v].push_back(u);`.
- **Preparando a Exploração**: Criamos uma lista para registrar as cidades visitadas (`nos_visitados`), inicialmente todas como false (não visitadas).
- **Iniciando a Jornada**: Escolhemos uma cidade inicial (no caso, a cidade 1) e começamos nossa busca em profundidade: `dfs(1, grafo, nos_visitados);`.

## O Código Completo
```cpp
#include<bits/stdc++.h>
using namespace std;

void dfs(int inicial, vector<vector<int>> &grafo, vector<bool> &nos_visitados){
    nos_visitados[inicial] = true;
    cout << inicial << " ";
    
    for(int visinho : grafo[inicial]){
        if(!nos_visitados[visinho]){
            dfs(visinho, grafo, nos_visitados);
        }
    }
}

int main()
{
    int num_nos, num_arestas;
    cin >> num_nos >> num_arestas;
    vector<vector<int>> grafo(num_nos);
    
    for(int i = 0; i < num_arestas; i++){
        int u, v;
        cin >> u >> v;
        grafo[u].push_back(v);
        grafo[v].push_back(u);
    }
    vector<bool> nos_visitados(num_nos, false);
    dfs(1, grafo, nos_visitados);
    return 0;
}
