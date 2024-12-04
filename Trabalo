import requests
from deep_translator import GoogleTranslator
import os

# URL da API de conselhos
URL = 'https://api.adviceslip.com/advice'
ARQUIVO_CONSELHOS = 'Conselhos.txt'

# Função para consumir a API e obter um conselho
def obter_conselho():
    try:
        response = requests.get(URL)
        data = response.json()
        return data["slip"]["advice"], data["slip"]["id"]
    except Exception as e:
        print(f"Erro ao obter conselho: {e}")
        return None, None

# Função para salvar o conselho no arquivo de texto
def salvar_conselho(conselho, conselho_id):
    try:
        with open(ARQUIVO_CONSELHOS, "a") as file:
            file.write(f"{conselho_id}: {conselho}\n")
        print("Conselho salvo com sucesso!")
    except Exception as e:
        print(f"Erro ao salvar conselho: {e}")

# Função para exibir os conselhos salvos no arquivo de texto
def mostrar_conselhos_salvos():
    try:
        if not os.path.exists(ARQUIVO_CONSELHOS):
            print("Nenhum conselho guardado.")
            return
        with open(ARQUIVO_CONSELHOS, "r") as file:
            conselhos = file.readlines()
            if not conselhos:
                print("Nenhum conselho guardado.")
            else:
                for conselho in conselhos:
                    print(conselho.strip())  # Exibe cada linha com strip
    except Exception as e:
        print(f"Erro ao ler os conselhos salvos: {e}")

# Função para traduzir o conselho do inglês para português
def traduzir_conselho(conselho, idioma_destino='pt'):
    try:
        traducao = GoogleTranslator(source='en', target=idioma_destino).translate(conselho)
        return traducao
    except Exception as e:
        print(f"Erro ao traduzir conselho: {e}")
        return None

# Função para relembrar as dicas e traduzi-las, se necessário
def relembrar_dicas(traduzir=False):
    try:
        if not os.path.exists(ARQUIVO_CONSELHOS):
            print("Nenhum conselho guardado.")
            return
        with open(ARQUIVO_CONSELHOS, "r") as file:
            conselhos = file.readlines()
            if not conselhos:
                print("Nenhum conselho guardado.")
            else:
                for conselho in conselhos:
                    conselho_id, conselho_text = conselho.split(":", 1)
                    print(f"Conselho ID {conselho_id.strip()}: {conselho_text.strip()}")
                    if traduzir:
                        traducao = traduzir_conselho(conselho_text.strip())
                        if traducao:
                            print("Tradução:", traducao)
    except Exception as e:
        print(f"Erro ao ler os conselhos: {e}")

# Função principal para gerenciar o menu
def menu():
    while True:
        print("\nMenu do Seu Zé:")
        print("1. Ouvir o Seu Zé: Perguntar quantos conselhos ele quer receber.")
        print("2. Mostrar os Conselhos: Exibir os conselhos mágicos da API.")
        print("3. Guardar a Sabedoria: Salvar conselhos no arquivo.")
        print("4. Mostrar os Conselhos guardados.")
        print("5. Traduzir para o 'Gringo': Traduzir conselhos do inglês para português.")
        print("6. Relembrar as Dicas: Acessar conselhos salvos e traduzi-los.")
        print("7. Sair")

        opcao = input("Escolha uma opção (1-7): ").strip()

        if opcao == "1":
            try:
                quantidade = int(input("Quantos conselhos você quer receber? "))
                for _ in range(quantidade):
                    conselho, conselho_id = obter_conselho()
                    if conselho:
                        print(f"Conselho ID {conselho_id}: {conselho}")
            except ValueError:
                print("Por favor, insira um número válido.")
        elif opcao == "2":
            conselho, conselho_id = obter_conselho()
            if conselho:
                print(f"Conselho ID {conselho_id}: {conselho}")
        elif opcao == "3":
            conselho, conselho_id = obter_conselho()
            if conselho:
                salvar_conselho(conselho, conselho_id)
        elif opcao == "4":
            mostrar_conselhos_salvos()
        elif opcao == "5":
            conselho, _ = obter_conselho()
            if conselho:
                print(f"Conselho em inglês: {conselho}")
                traducao = traduzir_conselho(conselho)
                if traducao:
                    print("Tradução:", traducao)
        elif opcao == "6":
            traduzir_input = input("Você deseja traduzir os conselhos? [S/N]: ").strip().lower()
            traduzir = traduzir_input == 's'
            relembrar_dicas(traduzir)
        elif opcao == "7":
            print("Saindo... Até logo, Seu Zé!")
            break
        else:
            print("Opção inválida! Tente novamente.")

if __name__ == "__main__":
    menu()
