# botpython
telegrambot on replit.com Изучение Python💖

import telebot
from random import choice
TOKEN ="4UaU"

bot = telebot.TeleBot(TOKEN)

@bot.message_handler(commands=["start"])
def start(message):
    
    keyboard = telebot.types.ReplyKeyboardMarkup()

    red_button = telebot.types.KeyboardButton("♥️")
    black_button = telebot.types.KeyboardButton("♠️")

    keyboard.row(red_button)
    keyboard.row(black_button)
    bot.send_message(message.chat.id, "Угадай цвет масти карты:♥️ or ♠️", reply_markup=keyboard)
    
    bot.register_next_step_handler(message, compare_answers)

def compare_answers(message):
    
    CARD_NUMBER, CARD_SUIT = generate_card()
    player_answer = message.text

    correct_answer = "That is correct, card is:" + CARD_NUMBER + CARD_SUIT

    incorrect_answer = "That is not correct, card is:" + CARD_NUMBER + CARD_SUIT
    
    if player_answer =="♥️" and CARD_SUIT in ["Б", "Ч"]:
       bot.send_message(message.chat.id,correct_answer)
    elif player_answer =="♠️" and CARD_SUIT in["П","К"]:
       bot.send_message(message.chat.id,correct_answer)
    else:
       bot.send_message(message.chat.id,incorrect_answer)


def generate_card():
    CARD_NUMBER = ["2","3","4","5","6","7","8","9","10","J","Q","K","A"]
    CARD_SUIT = ["Б","Ч","П","К"]
    
    random_card_numb = choice(CARD_NUMBER)
    random_card_suit = choice(CARD_SUIT)
    return [random_card_numb,random_card_suit]
    
bot.infinity_polling()


