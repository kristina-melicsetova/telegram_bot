# telegram_bot
import telebot
import config 
import random 

from telebot import types

bot = telebot.TeleBot(config.TOKEN)

@bot.message_handler(commands=['start'])
def welcome(message):
    # sti = open('Documents/sticker.wepb', 'rb')
    # bot.send_stiker(message.chat.id,sti)

    markup= types.ReplyKeyboardMarkup(resize_keyboard=True)
    item1 =types.KeyboardButton("Рандомное число")
    item2 =types.KeyboardButton("Как дела?")

    markup.add(item1,item2)

    bot.send_message(message.chat.id,"добро пожаловатть, {0.first_name}!\n я -<b>{1.first_name}</b>".format(message.from_user, bot.get_me()),parse_mode='html',reply_markup=markup)

@bot.message_handler(content_types=['text'])
def lalala(message):
    if message.chat.type == "private":
        if message.text == 'Рандомное число':
            bot.send_message(message.chat.id, str(random.randint(0,100)))
        elif message.text == 'Как дела?':

            markup = types.InlineKeyboardMarkup(row_width=2)
            item1 = types.InlineKeyboardButton("Хорошо", callback_data='good')
            item2 = types.InlineKeyboardButton("Не очень", callback_data='bad')
            markup.add(item1, item2)

            bot.send_message(message.chat.id,'отлично,сам как?', reply_markup=markup)
        else:
            bot.send_message(message.chat.id,'я не знаю, что ответить')
    
@bot.callback_query_handler(func=lambda call: True)
def callback_inline(call):
    try:
        if call.message:
            if call.data == 'good':
                bot.send_message(call.message.chat.id,'вот и отличненько')
            elif call.data == 'bad':
                bot.send_message(call.message.chat.id,'бывает')
            bot.edit_message_text(chat_id=call.message.chat.id, message_id=call.message.message_id, text="Как дела?", reply_markup=None)

            bot.answer_callback_query(chat_id=call.message.chat.id, show_alert=False, text="Это тестовое ")
    except Exception as e:
        print(repr(e))


bot.polling(none_stop=True)
