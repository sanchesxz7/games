import random

# Classe para o personagem
class Personagem:
    def __init__(self, nome, saude, mana, ataque):
        self.nome = nome
        self.saude = saude
        self.mana = mana
        self.ataque = ataque

    def atacar(self, inimigo):
        dano = random.randint(self.ataque - 2, self.ataque + 2)
        inimigo.saude -= dano
        print(f"{self.nome} atacou {inimigo.nome} e causou {dano} de dano!")

    def usar_magia(self, inimigo):
        if self.mana >= 5:
            dano = random.randint(10, 15)
            inimigo.saude -= dano
            self.mana -= 5
            print(f"{self.nome} usou magia e causou {dano} de dano!")
        else:
            print(f"{self.nome} não tem mana suficiente para usar magia!")

    def esta_vivo(self):
        return self.saude > 0

# Classe para inimigos
class Inimigo:
    def __init__(self, nome, saude, ataque):
        self.nome = nome
        self.saude = saude
        self.ataque = ataque

    def atacar(self, personagem):
        dano = random.randint(self.ataque - 2, self.ataque + 2)
        personagem.saude -= dano
        print(f"{self.nome} atacou {personagem.nome} e causou {dano} de dano!")

    def esta_vivo(self):
        return self.saude > 0

# Função de combate
def combate(personagem, inimigo):
    while personagem.esta_vivo() and inimigo.esta_vivo():
        print("\nEscolha uma ação:")
        print("1. Atacar")
        print("2. Usar Magia")
        print("3. Fugir")
        escolha = input("Escolha (1/2/3): ")

        if escolha == "1":
            personagem.atacar(inimigo)
        elif escolha == "2":
            personagem.usar_magia(inimigo)
        elif escolha == "3":
            print(f"{personagem.nome} fugiu da batalha!")
            break
        else:
            print("Escolha inválida. Tente novamente.")

        if inimigo.esta_vivo():
            inimigo.atacar(personagem)
        else:
            print(f"{inimigo.nome} foi derrotado!")

    if personagem.esta_vivo():
        print(f"{personagem.nome} venceu a batalha!")
    else:
        print(f"{personagem.nome} foi derrotado...")

# Função para apresentar o cenário e escolhas iniciais
def inicio_jogo():
    print("Bem-vindo ao mundo de Aetheria!")
    nome = input("Qual é o seu nome, aventureiro? ")

    personagem = Personagem(nome, saude=100, mana=20, ataque=15)
    print(f"\nBem-vindo, {personagem.nome}! Você começa sua jornada com 100 de saúde, 20 de mana e 15 de ataque.")

    print("\nVocê está em uma estrada sombria, com uma floresta à sua frente.")
    print("De repente, um inimigo aparece!")

    inimigo = Inimigo("Goblin", saude=50, ataque=10)

    combate(personagem, inimigo)

    if personagem.esta_vivo():
        print("\nVocê continua sua jornada...")
        # Mais opções e eventos podem ser adicionados a
inicio_jogo()

