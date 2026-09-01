# Banco de dados simulado do estoque
estoque = {
    "101": {"nome": "Teclado USB", "preco": 100.0, "qtd": 10},
    "102": {"nome": "Mouse Óptico", "preco": 50.0, "qtd": 3},
    "103": {"nome": "Monitor 24'", "preco": 800.0, "qtd": 0}
}


# 🔴 Manutenção Corretiva
def processar_venda(cod_prod, qtd_desejada):
    prod = estoque.get(cod_prod)

    if not prod:
        print("Erro: Produto não encontrado!")
        return

    # Validação da quantidade
    if qtd_desejada <= 0:
        print("Erro: A quantidade da venda deve ser maior que zero!")
        return

    # Validação do estoque disponível
    if qtd_desejada > prod["qtd"]:
        print(
            f"Erro: Estoque insuficiente! "
            f"Disponível: {prod['qtd']} unidade(s)."
        )
        return

    # Processa a venda
    prod["qtd"] -= qtd_desejada
    total = prod["preco"] * qtd_desejada

    print(f"Venda concluída! Total: R$ {total:.2f}")


# 🔵 Manutenção Adaptativa
def emitir_nota(cod_prod, qtd):
    prod = estoque.get(cod_prod)

    if prod:
        total = prod["preco"] * qtd
        imposto = total * 0.10
        total_com_imposto = total + imposto

        print("--- NOTA FISCAL ---")
        print(f"Produto: {prod['nome']} | Qtd: {qtd}")
        print(f"Subtotal: R$ {total:.2f}")
        print(f"Imposto (10%): R$ {imposto:.2f}")
        print(f"Total com imposto: R$ {total_com_imposto:.2f}")
        print("-------------------")
    else:
        print("Erro: Produto não encontrado!")


# 🟣 Manutenção Evolutiva
def repor_estoque(cod_prod, qtd):
    prod = estoque.get(cod_prod)

    if not prod:
        print("Erro: Produto não encontrado!")
        return

    if qtd <= 0:
        print("Erro: A quantidade para reposição deve ser maior que zero!")
        return

    prod["qtd"] += qtd

    print(
        f"Estoque reposto com sucesso! "
        f"Produto: {prod['nome']} | "
        f"Quantidade adicionada: {qtd} | "
        f"Estoque atual: {prod['qtd']}"
    )


# Execução de teste inicial
processar_venda("101", 2)
emitir_nota("101", 2)

# Testes adicionais
processar_venda("102", 5)   # Estoque insuficiente
processar_venda("101", 0)   # Quantidade inválida
processar_venda("101", -2)  # Quantidade inválida

repor_estoque("103", 5)     # Reposição de estoque
