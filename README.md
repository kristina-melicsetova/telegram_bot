# telegram_bot
import telebot
import config 
import random 

from telebot import types

bot = telebot.TeleBot(config.TOKEN)# берём при создании в father bot

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
            item3 = types.InlineKeyboardButton("Заметка о технологии", callback_data='zametka')
            item4 = types.InlineKeyboardButton("Об использовании времени", callback_data='time')
            item5 = types.InlineKeyboardButton("Слова, предложения, абзацы и более", callback_data='part2')
            item6 = types.InlineKeyboardButton("Дополнительные уровни", callback_data='dop')
            markup.add(item1, item2,item3,item4,item5,item6)
 
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
if call.data == 'good':
                markup = types.InlineKeyboardMarkup(row_width=2)
                item2 = types.InlineKeyboardButton("Зачем писать эссе?", callback_data='bad')
                markup.add(item2)
                bot.send_message(call.message.chat.id, 'https://telegra.ph/Nachnem-06-30', parse_mode='html', reply_markup=markup)
            if call.data == 'bad':
                markup = types.InlineKeyboardMarkup(row_width=2)
                item3 = types.InlineKeyboardButton("Заметка о технологии", callback_data='zametka')
                markup.add(item3)
                bot.send_message(call.message.chat.id, 'https://telegra.ph/ap-06-29-2', parse_mode='html', reply_markup=markup)
                                                       
            elif call.data == 'zametka':
                markup = types.InlineKeyboardMarkup(row_width=2)
                item3 = types.InlineKeyboardButton("Об использовании времени", callback_data='time')
                markup.add(item3)
                bot.send_message(call.message.chat.id, 'https://telegra.ph/Zametka-o-tehnologii-06-30', parse_mode='html', reply_markup=markup)
            if call.data == 'time':
                markup = types.InlineKeyboardMarkup(row_width=2)
                item4 = types.InlineKeyboardButton("Слова, предложения, абзацы и более", callback_data='part2')
                markup.add(item4)
                bot.send_message(call.message.chat.id, 'https://telegra.ph/Ob-ispolzovanii-vremeni-06-30', parse_mode='html', reply_markup=markup)
            elif call.data == 'part2':
                markup = types.InlineKeyboardMarkup(row_width=2)
                item5 = types.InlineKeyboardButton("Дополнительные уровни", callback_data='dop')
                markup.add(item5)
                bot.send_message(call.message.chat.id, 'https://telegra.ph/CHAST-VTORAYA-UROVNI-RAZRESHENIYA-06-30', parse_mode='html', reply_markup=markup)
            if call.data == 'dop':
                bot.send_message(call.message.chat.id, 'https://telegra.ph/Dopolnitelnye-urovni-06-30')
                
 
            # show alert
            bot.answer_callback_query(callback_query_id=call.id, show_alert=False,
                text="Удачи!")
 
    except Exception as e:
        print(repr(e))


bot.polling(none_stop=True)
