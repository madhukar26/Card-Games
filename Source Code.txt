"""This is a odified version of the card game WAR.
Rules:

1.In this game the deck of card is divided equally amongst the two players
2.Each player pulls out a card from their respective deck and compare the rank of their cards
3. The player with the higher rank wins that round and puts both the cards being compared into his deck.
4. if the rank of the cards is same there is a tie and both the cards are removed from the hand deck.
5. The player whose deck gets finished first loses the game

"""
import random

suits = ['spades','hearts','diamonds','clubs']
ranks = ['ace','two','three','four','five','six','seven','eight','nine','ten','jack','queen','king']

class Card:

    def __init__(self,suit,rank):
        self.suit=suit
        self.rank=rank
    def __str__(self):
        print("The card is {} of {}".format(self.rank,self.suit))


class Deck(Card):
    def __init__(self):
        self.cards=[]


        for i in suits:
            for j in ranks:
                card=Card(i,j)
                # print(card.__str__())
                self.cards.append(card)

    def display_deck(self):
        for i in range(len(self.cards)):
           print(self.cards[i].rank,self.cards[i].suit)

    def move_cards(self,count):
        self.hand_cards=[]

        for i in range(count):

            self.hand_cards.append(deck.pop_card())
            # print(Deck.pop_card(deck).suit)

    def hand_check(self):
        for i in range(len(self.hand_cards)):
            print(self.hand_cards[i].rank,self.hand_cards[i].suit)

    def rank_check(self,self2):
        if  self.hand_cards[-1].rank == self2.hand_cards[-1].rank:
            print("It's a tie")
            self2.hand_cards.remove(self2.hand_cards[-1])
            self.hand_cards.remove(self.hand_cards[-1])
        elif self.hand_cards[-1].rank > self2.hand_cards[-1].rank:
            print("Player1 won this round")
            player1.hand_cards.append(player2.pop_card())
            player2.hand_cards.pop()
        elif self.hand_cards[-1].rank < self2.hand_cards[-1].rank:
            print("player 2 won this round")
            player2.hand_cards.append(player1.pop_card())
            player1.hand_cards.pop()

    def add_card(self, card):
        self.cards.append(card)

    def remove_card(self, card):
        self.cards.remove(card)

    def pop_card(self, i=-1):

        return self.cards.pop(i)

    def shuffle(self):
        """Shuffles the cards in this deck."""
        random.shuffle(self.cards)


"""Creating a Card deck"""
deck=Deck()
"""Shuffling the deck"""

deck.shuffle()

"""Creating Players"""

player1=Deck()
player2=Deck()

"""distributing cards amongst two players"""
print("*"*10)
player1.move_cards(26)
player2.move_cards(26)
print("Player1 has: ",len(player1.hand_cards),"cards")
print("Player2 has: ",len(player2.hand_cards),"cards")
print("Cards left in deck:",len(deck.cards))
print("*"*10)


"Displaying both the players card to user"

print("displaying player1 cards:\n","*"*20)
player1.hand_check()
print("*"*20)
print("displaying player2 cards:\n","*"*20)
player2.hand_check()
print("*"*20)

"""Let the Game start"""
while (len(player1.hand_cards)>-1) or (len(player2.hand_cards)>-1):


    if (len(player2.hand_cards)==0) or (len(player1.hand_cards)==0):

        if len(player2.hand_cards) > len(player1.hand_cards):
            print("Player2 won this game after ")
        elif len(player2.hand_cards) < len(player1.hand_cards):
            print("Player1 won this game ")

        exit()
    else:
        player1.rank_check(player2)
        print("Now Player2 has : ", len(player2.hand_cards)," cards")
        print("Now Player1 has : ",len(player1.hand_cards)," cards")


player1.hand_check()
player2.hand_check()