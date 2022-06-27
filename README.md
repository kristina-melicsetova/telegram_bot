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
    elif message.text == 'Напишем эссе!':
 
            markup = types.InlineKeyboardMarkup(row_width=2)
            item1 = types.InlineKeyboardButton("Что такое эссе?", callback_data='good')
            item2 = types.InlineKeyboardButton("Зачем писать эссе?", callback_data='bad')
 
            markup.add(item1, item2)
 
            bot.send_message(message.chat.id, 'Будем писать!', reply_markup=markup)
        else:
            bot.send_message(message.chat.id, 'Я не знаю что ответить 😢')rdButton("Зачем писать эссе?", callback_data='zachem')
            markup.add(item1, item2)
        elif message.text == 'Как дела?':

            markup = types.InlineKeyboardMarkup(row_width=2)
            item1 = types.InlineKeyboardButton("Что такое эссе?", callback_data='what is asse')
            item2 = types.InlineKeyboardButton("Зачем писать эссе?", callback_data='zachem')
            markup.add(item1, item2)

def callback_inline(call):
    try:
        if call.message:
            if call.data == 'good':
                bot.send_message(call.message.chat.id, 'Эссе – это сравнительно короткий текст по определенной теме. Однако, слово essay (в английском) также значит пробу или попытку. Таким образом, эссе – это короткий текст, написанный кем-то в попытке исследовать тему или ответить на вопрос.')
            elif call.data == 'bad':
                bot.send_message(call.message.chat.id, 'В большинстве случаев студенты пишут эссе только потому, что их преподаватель требует этого. Поэтому студенты думают, что эссе важны прежде всего для демонстрации их знаний учителю или профессору. Это понятная, и опасная, ошибка (хоть написание текстов для демонстрации и может быть практически необходимым.)')
 
            # remove inline buttons
            bot.edit_message_text(chat_id=call.message.chat.id, message_id=call.message.message_id, text="Напишем эссе!",
                reply_markup=None)
 
            # show alert
            bot.answer_callback_query(callback_query_id=call.id, show_alert=False,
                text="Удачи!")
 
    except Exception as e:
        print(repr(e))


bot.polling(none_stop=True)
