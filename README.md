# telegram_bot
import telebot
import config
import random 
 
from telebot import types


bot = telebot.TeleBot(config.TOKEN)

@bot.message_handler(commands=['start'])
def welcome(message):
    sti = open('Downloads/for_telegram.webp','rb')
    bot.send_sticker(message.chat.id, sti)


    #keyboard
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    item1= types.KeyboardButton("how are you?")
    item2 = types.KeyboardButton("rundom number")

    markup.add(item1,item2)


    bot.send_message(message.chat.id, "welcome, {0.first_name}!\n Я <b> {1.first_name} </b> - бот в стадии полуфабриката".format(message.from_user, bot.get_me()),parse_mode='html', reply_markup=markup)

@bot.message_handler(content_types=['text'])
def lalala(message):
    if message.chat.type == 'private':
        if message.text == 'random number':
            bot.send_message(message.chat.id, str (random.randint(0,100)))
        elif message.text == 'how are you?':
            bot.send_message(message.chat.id, 'отлично, сам как?')
        else:
            bot.send_message(message.chat_id, 'да, и ответить не знаю чего тебе')
        

#run
bot.polling(none_stop=True)
