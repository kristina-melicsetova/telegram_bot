# telegram_bot
from ctypes import resize
import telebot
import config
import random
from telebot import types

bot = telebot.TeleBot(config.TOKEN)


@bot.message_handler(commands=['start'])
def welcome(message):
    sti = open('/home/kris/Desktop/static/welcome.webp', 'rb')
    bot.send_sticker(message.chat.id, sti)
