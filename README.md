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

# Strategie greedy qui prend les maximums des probabilites et qui renvoie l'etat s
def greedy(liste):
    b =[ ]
    for i in liste:
        b.append(liste[1])
    m = max(b)
    if b.count(m) > 1:
        i = random.choice([s for s,p in enumerate(b) if m == p])
        s = liste[i][0]
    return s,m


# strategie eps greedy qui renvoie la fonction greedy ou un choix aléatoire
def eps_greedy(eps,liste):
    r = random.random()
    if r >= eps :
        s,m = greedy(liste)
    elif r < eps:
        s,m = random.choice(liste)
    return s,m


# fonction qui renvoie le deplacement en fonction d'eps_greedy et en mettant a jour l'estimation de la  probabilite
def makeMove(M, last, strategy, eps, alpha) :
    res,m = eps_greedy(eps,M)
    if last != None:
        if strategy == "Q-learning":
            last[1] = (1 - alpha) * last[1] + alpha * m
        elif strategy == "TD(0)":
            last[1] = (1 - alpha) * last[1] + alpha * ps
    return res


# fonction fin du jeu qui met a jour les estimations des proba en fonction de la strategie
def endGame(won, history, strategy, alpha) :
    r = 0
    if won == False:
        r = 1
        if strategy == "Q-learning":
            history[[-1],[1]] = (1-alpha) * history[[-1],[1]] + alpha * r
        elif strategy == "TD(0)":
            history[[-1],[1]] = (1-alpha) * history[[-1],[1]] + alpha * r
        elif strategy == "Monte Carlo":
            history[[-1],[1]] = (1 - alpha) * history[[-1],[1]] + alpha * r
    return history
