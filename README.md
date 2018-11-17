"""
 BOUALI Ikram
 18/11/2018
 Matricule ULB: 000479199
 Projet Quoridor - partie 1 (sans murs,deplacement simple et 3 strategies d'apprentissage)
 """
 #Importation de tout les modules de random
import random

 # Strategie greedy qui prend les maximums des probabilites et qui renvoie l'etat s
def greedy(liste):
    b =[ ]
    for i in range(len(liste)): #on parcourt les indices de la liste
        b.append(liste[i][1])
    m = max(b) #m vaut la probabilite max
    if b.count(m) >= 1:
        i = random.choice([i for i,p in enumerate(b) if m == p])#on effectue un choix dans la liste en mettant les
        # indices face au proba max et on prend les indices des proba max
        s = liste[i][0] #on prend grace a cette indice le premier element qui est l'etat s
    return s,m #on renvoie l'etat apres coup et la proba max associe a greedy


 # strategie eps greedy qui renvoie la fonction greedy ou un choix aléatoire
def eps_greedy(eps,liste):
    r = random.random()
    s,m_greedy = greedy(liste)#on utilise l'etat s et la proba max dans greedy
    if r < eps:
        s,m_choice = random.choice(liste) #si r est plus petit que eps on prend un etat et une proba max qu'on va
        # associe a la proba du choix au hasard
    else:
        m_choice = m_greedy #sinon on renvoit la proba max greedy
    return s,m_choice,m_greedy #Il renvoie l'etat apres coup, la proba associe a l'etat et la proba associe au greedy


 # fonction qui renvoie le deplacement en fonction d'eps_greedy et en mettant a jour l'estimation de la  probabilite
def makeMove(M, last, strategy, eps, alpha) :
    s,m_choice,m_greedy = eps_greedy(eps,M)
    if last != None:
        if strategy == "Q-learning":
            last[1] = (1 - alpha) * last[1] + alpha * m_greedy
        elif strategy == "TD(0)":
            last[1] = (1 - alpha) * last[1] + alpha * m_choice
    return s #retourne l'etat apres coup


 # fonction fin du jeu qui met a jour les estimations des proba en fonction de la strategie
def endGame(won, history, strategy, alpha) :
    if won:
        r = 1
    else:
        r = 0
        if strategy == "Q-learning":
            history[-1][1] = (1-alpha) * history[-1][1] + alpha * r
        elif strategy == "TD(0)":
            history[-1][1] = (1-alpha) * history[-1][1] + alpha * r
        elif strategy == "Monte Carlo":
            history.reverse() #on retourne la liste pour Monte Carlo
            for i in range(len(history)):
                history[i][1] = (1 - alpha**i) * history[-1][1] + (alpha**i) * r
            history.reverse()#et on la remet a sa forme initiale a la fin
