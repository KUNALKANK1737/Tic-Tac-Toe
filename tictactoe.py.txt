import random
def choose_first():
    flip = random.randint(0,1)
    if flip ==0:
        return 'player 1'
    else:
        return 'player 2'
def display_board(board):
    print("\n"*10)
   # clear_output()
    print(board[1]+'|'+board[2]+'|'+board[3])
    print("- - -")
    print(board[4]+'|'+board[5]+'|'+board[6])
    print("- - -")
    print(board[7]+'|'+board[8]+'|'+board[9])
    print("- - -")
def player_input():
    #output=player1 marker ,player 2 marker
    marker=""
    #keep asking player 1 to choose x or o
    while not(marker =='X' or marker =='O'):
        marker =input("Player 1 ,choose X or O:").upper()
    #asking the player 2, the opposite marker
    player1=marker
    if marker =="X":
         return('X','O')
    else :
        return('O','X')
def place_marker(board,marker,position):
    board[position]=marker
def win_check(board,mark):
    #win tic tac toe

    #all rows and check to see if they all share the same marker
    return(( board[7]== mark and board[8]== mark and board[9]==mark)or#row vise
    ( board[4]== mark and board[5]== mark and board[6]==mark) or #row vise
    ( board[1]== mark and board[2]== mark and board[3]==mark) or#row vise
    ( board[7]== mark and board[4]== mark and board[1]==mark) or# col from left start
    ( board[8]== mark and board[5]== mark and board[2]==mark) or# col from left to the right
    ( board[9]== mark and board[6]== mark and board[3]==mark) or# col to the right last position
    ( board[7]== mark and board[5]== mark and board[3]==mark) or#accros the diagonal from top to bottom
    ( board[9]== mark and board[5]== mark and board[1]==mark) )# accros the diagonal from bootom to top
 #all col check to see if marker matches

def space_check(board,position):
     return board[position]==' '
def full_board_check(board):
    for i in range(1,10):
        if space_check(board,i):
            return False
        #board is ful if retrun true
    return True
def player_choice(board):
    position=0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position = int(input("Choose a position : (1-9) "))
    return position
def replay():
    choice = input("Play again? Enter yes or no")
    return choice =='yes'
#while loop to keep runnning the game
print("Welcome to the TIC TAC TOE")
while True:
    #play the game here


 ###set everything up(board,whos first,choose markers)
    the_board=[' ']*10
    player1_marker,player2_marker = player_input()
    turn = choose_first()
    print(turn + " will go first")
    play_game=input('Ready to play? y or n :')
    if play_game =='y':
        game_on=True
    else:
        game_on =False
        #game play
    while game_on:
        if turn =='player 1':
            display_board(the_board)
            #choose the position
            position=player_choice(the_board)
            #place the marker on the position
            place_marker(the_board,player1_marker,position)
            
            #or check if they win
            if win_check(the_board,player1_marker):
                display_board(the_board)
                print("player 1 has won !")
                game_on =False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print("tie game !")
                    game_on = False 
                else:
                    turn = 'player 2'
        else:
           display_board(the_board)
            #choose the position
           position=player_choice(the_board)
            #place the marker on the position
           place_marker(the_board,player2_marker,position)
            
            #or check if they win
           if win_check(the_board,player2_marker):
                display_board(the_board)
                print("player 2 has won !")
                game_on =False
           else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print("Tie  Game !")
                    game_on = False 
                else:
                    turn = 'player 1'
        
    if not replay():
        break
#break out of the while loop on replay()
