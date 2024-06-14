def depositar(saldo):
    while True:
        try:
            valor_deposito = float(input("Informe o valor do depósito: "))
            if valor_deposito > 0:
                saldo += valor_deposito
                print(f"Depósito de R$ {valor_deposito:.2f} realizado com sucesso.")
                break
            else:
                print("Por favor, insira um valor positivo.")
        except ValueError:
            print("Por favor, insira um valor válido.")
    return saldo

def sacar(saldo, limite, numero_saques):
    valor = float(input("Informe o valor do saque: "))
    if valor > saldo:
        print("Operação falhou! Você não tem saldo suficiente.")
    elif valor > limite:
        print("Operação falhou! O valor do saque excede o limite.")
    elif numero_saques >= LIMITE_SAQUES:
        print("Operação falhou! Número máximo de saques excedido.")
    elif valor > 0:
        saldo -= valor
        print(f"Saque de R$ {valor:.2f} realizado com sucesso.")
    else:
        print("Operação falhou! O valor informado é inválido.")
    return saldo, valor  

def exibir_extrato(saldo, extrato):
    print("\n================ EXTRATO ================")
    if extrato:
        print(extrato)
    else:
        print("Não foram realizadas movimentações.")
    print(f"\nSaldo: R$ {saldo:.2f}")
    print("==========================================")

saldo = 0
limite = 500
extrato = ""
numero_saques = 0
LIMITE_SAQUES = 3

while True:
    opcao = input("""

[d] Depositar
[s] Sacar
[e] Extrato
[q] Sair

=> """).strip().lower()

    if opcao == "d":
        saldo = depositar(saldo)
        extrato += f"Depósito: R$ {saldo:.2f}\n"  

    elif opcao == "s":
        saldo, valor_saque = sacar(saldo, limite, numero_saques)  
        extrato += f"Saque: R$ {valor_saque:.2f}\n"  
        numero_saques += 1

    elif opcao == "e":
        exibir_extrato(saldo, extrato)

    elif opcao == "q":
        print("Saindo...")
        break

    else:
        print("Operação inválida, por favor selecione novamente a operação desejada.")
