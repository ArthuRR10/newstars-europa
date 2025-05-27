from flask import Flask, jsonify
from threading import Thread
import random

app = Flask(__name__)

nomes = [
    "Luca", "Sofia", "Arthur", "Maja", "Hugo", "Isla", "Mateo", "Elena",
    "Dimitri", "Anouk", "Bjorn", "Freya", "Carlos", "Giulia", "Erik", "Nina",
    "Theo", "Anastasia", "Oscar", "Clara", "Nikolai", "Emma", "Alessio", "Ines",
    "Jakub", "Zara", "Rafael", "Leonie", "Tobias", "Mirela", "Andrei", "Greta",
    "Felix", "Chiara", "Jonas", "Ivana", "Sebastian", "Helena", "Aksel", "Liliana"
]

sobrenomes = [
    "Dubois", "Rossi", "Müller", "Silva", "Kowalski", "Nielsen", "Papadopoulos", "Ivanov",
    "Bianchi", "López", "Novak", "Petrov", "Andersson", "Nowak", "Ricci", "Fernandez",
    "Popescu", "Santos", "Gruber", "Horvat", "Costa", "Kovačić", "Fischer", "Moreau",
    "Lindberg", "Martínez", "Szabó", "Romano", "Barros", "Smirnov", "Hansen", "Demir",
    "Varga", "Vasiliev", "Marino", "Dimitrova", "Esposito", "Olofsson", "Bakos", "Dragomir"
]

nacionalidades = [
    "🇪🇸 Espanha", "🇩🇪 Alemanha", "🇮🇹 Itália", "🇬🇧 Inglaterra", "🇫🇷 França",
    "🇳🇱 Países Baixos", "🇵🇹 Portugal", "🇧🇪 Bélgica", "🇷🇸 Sérvia", "🇨🇭 Suíça",
    "🇭🇷 Croácia", "🇷🇴 Romênia", "🇦🇹 Áustria", "🇸🇪 Suécia", "🇬🇷 Grécia"
]

posicoes = ["Goleiro", "Zagueiro", "Lateral Direito", "Lateral Esquerdo", "Volante", "Meia Central", "Meia Ofensivo",
            "Ponta Direita", "Ponta Esquerda", "Centroavante"]

comparacoes = [
    "André Silva", "Ruben Neves", "Nicolo Zaniolo", "Pedri", "Florian Wirtz", "Dominik Szoboszlai",
    "Mykhailo Mudryk", "Josko Gvardiol", "Martin Ødegaard", "Cody Gakpo", "Federico Chiesa",
    "Rasmus Højlund", "Fábio Vieira", "Karim Adeyemi", "Benjamin Šeško", "Jamal Musiala"
]

capacidade_atual = [
    "Reserva na Championship", "Titular na Championship",
    "Reserva na NLEDF", "Titular na NLEDF"
]

capacidade_potencial = [
    "Titular na Championship", "Reserva na NLEDF", "Titular na NLEDF",
    "Reserva em time de Champions League", "Titular em time de Champions League"
]

# Estrelas com maior chance para 4 ou 5 estrelas
estrelas_pesos = [(2, 5), (3, 20), (4, 45), (5, 30)]

@app.route('/')
def gerar_jogador():
    nome = f"{random.choice(nomes)} {random.choice(sobrenomes)}"
    nacionalidade = random.choice(nacionalidades)
    posicao = random.choice(posicoes)
    comparacao = random.choice(comparacoes)
    atual = random.choice(capacidade_atual)
    potencial = random.choice(capacidade_potencial)
    estrelas = random.choices([e[0] for e in estrelas_pesos], weights=[e[1] for e in estrelas_pesos])[0]
    estrelas_txt = "<:sstar:1214063700886036532>" * estrelas

    return jsonify({
        "nome": nome,
        "nacionalidade": nacionalidade,
        "posicao": posicao,
        "comparacao": comparacao,
        "cap_atual": atual,
        "cap_potencial": potencial,
        "estrelas": estrelas_txt 
    })

def run():
    app.run(host='0.0.0.0', port=8080)

Thread(target=run).start()

