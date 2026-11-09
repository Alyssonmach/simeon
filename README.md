# SimEON

Simulador de redes ópticas elásticas (Elastic Optical Networks).

Para detalhes científicos do simulador, consulte o [artigo do projeto](https://link.springer.com/article/10.1007/s11107-017-0697-9).

## Requisitos no macOS

O roteiro abaixo foi verificado em um Mac Apple Silicon com Homebrew instalado em `/opt/homebrew`.

1. Instale as ferramentas de linha de comando do Xcode:

   ```sh
   xcode-select --install
   ```

2. Instale Homebrew, caso ainda não esteja instalado, e as dependências do projeto:

   ```sh
   brew install qt boost armadillo googletest libomp
   ```

O projeto usa C++17, qmake, Armadillo, Boost.Program_options, GoogleTest e OpenMP. O arquivo `adamant-broccoli.pro` contém os caminhos Homebrew `/opt/homebrew`. Em Macs Intel, ajuste esses caminhos para o prefixo retornado por `brew --prefix` e `brew --prefix libomp`.

## Compilar

A partir da pasta raiz do repositório, gere a compilação dentro de `build`:

```sh
mkdir -p build
cd build
"$(brew --prefix qt)/bin/qmake6" -spec macx-g++ ../adamant-broccoli.pro
make -j4
make install
```

`make install` copia as topologias usadas pelo simulador para `build/data/topologies`. Execute o programa a partir de `build`, pois ele procura os dados usando esse caminho relativo:

```sh
./adamant-broccoli
```

O programa é interativo e roda no Terminal. Escolha o tipo de simulação no menu e responda aos prompts numéricos. Os resultados são gravados na pasta atual junto com `SimConfigFile.ini`.

## Limpeza da compilação

Para remover objetos e recompilar após mudar opções do qmake, rode `make clean` dentro de `build`, gere novamente o Makefile com `qmake6` e repita `make` e `make install`.
