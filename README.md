# firstcommit
Projet Quoridor - Partie 1 - Ikram Bouali
"""
BOUALI Ikram
18/11/2018
Matricule ULB: 000479199
Projet Quoridor partie 1
"""
#Importation de tout les modules de random
from random import *
import random

# strategie greedy
def greedy(liste):
    b =[ ]
    for i in liste:
        b.append(liste[1])
    m = max(b)
    if b.count(m) > 1:
        ps = random.choice([e for e,j in enumerate(b)])

# boucle for pour parcourir les elements de la liste
def changement_etat(liste)
    for i in liste:
        if liste[0][0] > liste[0][1]:
            res = liste[0][0]
        else:
            res = liste[0][1]

# strategie eps greedy
def eps_greedy(eps,r,liste):
    r = random()
    if r => eps :
        greedy(liste)
    elif r < eps:
        s = random.choice(liste)

# fonction qui renvoie le deplacement
def makeMove(M, last, strategy, eps, alpha) :
    if last == None:
        s = random.randint(len-1)
    else:
        if strategy == "Q-learning":
            last = (1- alpha) * ps + alpha * ps
        elif strategy =="TD(0)":
            last = (1-alpha)* ps + alpha* ps

# fonction fin du jeu
def endGame(won, history, strategy, alpha) :
    if strategy == "Q-learning":
        history[[-1],[1]] = (1-alpha) * ps + alpha * r
    elif strategy == "TD(0)":
        history[[-1],[1]] = (1-alpha) * ps + alpha * r
    elif strategy == "Monte Carlo":
        history[[-1],[1]] = (1 - alpha) * ps + alpha * r
