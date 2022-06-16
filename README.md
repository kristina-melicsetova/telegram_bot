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

elif message.text == 'how are you?':
            markup = types.InlineKeyboardMarkup(row_width=2)
            item1 = types.InlineKeyboardButton("Хорошо",callback_data='good')
            item2 = types.InlineKeyboardButton("Не очень",callback_data='bad')
            
            markup.add(item1,item2)

            bot.send_message(message.chat.id, 'отлично, сам как?')
        else:
            bot.send_message(message.chat.id, 'да, и ответить не знаю чего тебе')
@bot.callback_query_handler(func=lambda call:True)
def callback_inline(call):
    try:
        if call.message:
            if call.data == 'good':
                bot.send_message(call.message.chat.id, 'Вот и отличненько')
            elif call.data == 'bad':
                bot.send_message(call.message.chat.id,'Крепись')
            #remove inline buttons
            bot.edit_message_text(chat_id=call.message.chat.id, message_id=call.message.message_id, text="how are you?",reply_markup=None)

            #chow alert
            bot.answer_callback_query(chat_id=call.message.chat.id, show_alert=False,text="Это тестовое уведомление") 

    except Exception as e:
        print(repr(e))
# #run
bot.polling(none_stop=True)

            
        

#run
bot.polling(none_stop=True)
