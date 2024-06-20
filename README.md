#!/bin/bash

# Função para exibir o menu
mostrar_menu() {
    echo "Menu de Backup"
    echo "1. Configurar diretórios"
    echo "2. Executar backup"
    echo "3. Sair"
    echo "Escolha uma opção:"
}
 
# Função para configurar diretórios
configurar_diretorios() {
    echo "Digite o diretório de origem:"
    read dir_origem
    echo "Digite o diretório de destino:"
    read dir_destino
 
    if [ ! -d "$dir_origem" ]; then
        echo "Diretório de origem não existe. Criando..."
        mkdir -p "$dir_origem"
    fi
 
    if [ ! -d "$dir_destino" ]; then
        echo "Diretório de destino não existe. Criando..."
        mkdir -p "$dir_destino"
    fi
}
 
# Função para executar o backup
executar_backup() {
    echo "Iniciando o backup de $dir_origem para $dir_destino"
    for arquivo in "$dir_origem"/*; do
        if [ -f "$arquivo" ]; then
            cp "$arquivo" "$dir_destino"
            echo "Copiado: $arquivo"
        fi
    done
    echo "Backup concluído!"
}
 
# Loop principal do menu
while true; do
    mostrar_menu
    read opcao
 
    case $opcao in
        1)
            configurar_diretorios
            ;;
        2)
            if [ -z "$dir_origem" ] || [ -z "$dir_destino" ]; then
                echo "Por favor, configure os diretórios primeiro."
            else
                executar_backup
            fi
            ;;
        3)
            echo "Saindo..."
            break
            ;;
        *)
            echo "Opção inválida. Tente novamente."
            ;;
    esac
done



