# -*- coding: utf-8 -*-
import telebot # подключение библиотеки pyTelegramBotAPI
import sqlite3
import requests  
import datetime

# для запуска скриптов
from subprocess import call
from telebot import types
#-----------------------------------------------------------------------------------------

class BotHandler:
 
    def __init__(self, token):
        self.token = token
        self.api_url = "https://api.telegram.org/bot792428361:AAFeqG97-q50_uR7Tm1IsWdeGKMl2Cqal7U/"
 
    def get_updates(self, offset=None, timeout=30):
        method = 'getUpdates'
        params = {'timeout': timeout, 'offset': offset}
        resp = requests.get(self.api_url + method, params)
        result_json = resp.json()['result']
        return result_json
 
    def send_message(self, chat_id, text):
        params = {'chat_id': chat_id, 'text': text}
        method = 'sendMessage'
        resp = requests.post(self.api_url + method, params)
        return resp
 
    def get_last_update(self):
        get_result = self.get_updates()
 
        if len(get_result) > 0:
            last_update = get_result[-1]
        else:
            last_update = get_result[len(get_result)]
 
        return last_update


#-----------------------------------------------------------------------------------------


#from log import log # Для сборов лога!!

# создание бота с его токеном API
bot = telebot.TeleBot("792428361:AAFeqG97-q50_uR7Tm1IsWdeGKMl2Cqal7U")

# текст справки
help_string = []
help_string.append("/start - task\n")
help_string.append("/vin \n")
help_string.append("/qr\n")
help_string.append("/Look_at_the_photo\n")
help_string.append("/site\n")
help_string.append("/Vanga\n")
help_string.append("/ssh\n")
help_string.append("/traffic_light\n")
help_string.append("/youtube\n")
help_string.append("/find\n")


# --- команды


@bot.message_handler(commands=['start'])
def send_start(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Ты решил изменить свою жизнь и пришел на правильное собеседование, на данный момент мы находимся в стадии развития , по-этому мы подготовили тебе несколько заданий, благодаря которым ты в конце получишь ссылку, записывай все ответы которые получишь, из каждого задания будут флаги, они называются Exp, ответ надо отправлять с ними, то есть если ты отправишь боту сообщение Exp{test}, то  бот тебе скажет привет, ну вот теперь ты знаешь что ответ надо писать в виде  Exp{...} Удачи тебе и помни, мы не сдаемся, для того чтобы пройти на следующий этап собеседования, ты должен выполнить все задания\n Дальше Мы даем тебе сами задания\n /ssh\n /Look_at_the_photo\n /qr\n /vin\n /site\n /Vanga\n /traffic_light\n /youtube\n /find\n По техническим вопросам, ты можешь нам писать сюда https://vk.com/explabs")

@bot.message_handler(commands=['vin'])
def send_task1(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Привет, мы знаем, что у такого как ты обязательно должен быть автомобиль, мы его тебе нашли. Ты обязан найти его, ведь мы приложили максимум усилий чтобы он у тебя появился, вот тебе данные про него, Марка: Opel Модель: Astra H GTC и чуть-чуть про него историю тебе расскажем. Данный автомобиль первоночально создан в Германии, но построили его на Бельгийском заводе в 2009году и его серийный номер - 021925. Найди его") 

@bot.message_handler(commands=['Look_at_the_photo'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Смотри, что я нашел в интернете, там надо .... Хотя ты и сам все знаешь прекрасно https://clck.ru/EZRdY")

@bot.message_handler(commands=['qr'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Я надеюсь, ты сумеешь это сделать :-D	 https://clck.ru/EaKkr")

@bot.message_handler(commands=['site'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Во это да, мы умудрились забыть пароль от сайта, вот же дырявая голова у нашего веб-программиста. Помоги нам зайти в админскую панель ")

@bot.message_handler(commands=['Vanga'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Baba Vanga")

@bot.message_handler(commands=['ssh'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Вот это да, мы со своей работой совершенно забыли тебе сказать, что у нас есть свой сервер,который поможет в достижении твоей цели. Он находится в МИРЭА по адресу Проспект вернадского 78, только вот незадача , к нему можно подключится только по локальной сети, но пароль от wifi забыли. Не расстраивайся,ведь мы оставили включенный pin на нем. Уверены, что такое тебе по силам!\n P.S. А, чуть не забыл help@192.168.1.1")

@bot.message_handler(commands=['traffic_light'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Все что надо программисту это пицца, чашка кофе и компьютер . IT-специалисты могут почти все, даже запрограммировать светофор.Кстати, раз зашла речь про светофор, то вот тебе задачка, у нас тут завалялись 3 светодиода и arduino. Конечно же ты не должен собирать уличный светофор, но вот написать программу нужно. Отправь нам код светофора на почту light@explabs.ru. Как только у нас в лаборатории заработает светофор, мы сразу же отправим тебе подтверждение обратно на почту. Ты справишься !")
@bot.message_handler(commands=['youtube'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Вот это да, мы очень долго старались над данным видео роликом, надеюсь он тебе понравится https://youtu.be/-rJNmtyah1Q ")

@bot.message_handler(commands=['find'])
def send_Look_at_the_photo(message):
    # отправка простого сообщения
    bot.send_message(message.chat.id, "Мы вот-вот завершим один проект, но вот тут произошла одна проблема, мы попросили курьера доставить нам одно послание, а он столкнулся с каким-то студентом в коридоре и случайно потерял данный лист, все что мы знаем что потерян он был где-то рядом со столовой, помоги пожалуйста нам его найти")
  

# --- Специальный фильтр сообщений 


@bot.message_handler(func=lambda message: message.text == "Exp{test}")

def command_text_explabs(m):
   bot.send_message(m.chat.id, "Привет")
#log_file = config['Export_params']['log_file']
		
@bot.message_handler(func=lambda message: message.text == "Exp{photoExpLabs}")
def command_text_explabs(m):
   bot.send_message(m.chat.id, "e")

@bot.message_handler(func=lambda message: message.text == "Exp{WOLOAHL0895021925}")
def command_text_hi(m):
   bot.send_message(m.chat.id, "x")

@bot.message_handler(func=lambda message: message.text == "Exp{You_can_think_logically}")
def command_text_hi(m):
   bot.send_message(m.chat.id, "p")

@bot.message_handler(func=lambda message: message.text == "Exp{Baba Vanga}")
def command_text_hi(m):
   bot.send_message(m.chat.id, "l")

@bot.message_handler(func=lambda message: message.text == "Exp{Your brain is unique}")
def command_text_hi(m):
   bot.send_message(m.chat.id, "a")

@bot.message_handler(func=lambda message: message.text == "Exp{There is light in you too}")
def command_text_hi(m):
   bot.send_message(m.chat.id, "b")

@bot.message_handler(func=lambda message: message.text == "Exp{youtube one love}")
def command_text_hi(m):
   bot.send_message(m.chat.id, "s")

@bot.message_handler(func=lambda message: message.text == "Exp{Sherlock Holmes would be proud of you}")
def command_text_hi(m):
   bot.send_message(m.chat.id, ".")

@bot.message_handler(func=lambda message: message.text == "1 WOLOAHL0895021925")
def command_text_hi(m):
   bot.send_message(m.chat.id, "r")

@bot.message_handler(func=lambda message: message.text == "1 WOLOAHL0895021925")
def command_text_hi(m):
   bot.send_message(m.chat.id, "u")


# Обработка для другого текста 
@bot.message_handler(func=lambda message: True, content_types=['text'])
def command_default(m):
    # Стандартный ответ 
    bot.send_message(m.chat.id, "Вы где-то допустили ошибку, перепроверьте свой ответ")
 


# запуск приёма сообщений
bot.polling()
