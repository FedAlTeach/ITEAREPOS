import telebot
import  requests
import json



myBot = telebot.TeleBot('7075505732:AAH76IP7JpzE1Xr5P_sLsmnfbM3KSaC9z88')

@myBot.message_handler(commands=['start'])
def start(message):
    myBot.send_message(message.chat.id, 'Hello! its a weather bot', reply_markup='Markdown')


@myBot.message_handler(content_types=['text'])
def weather(message):
    city = message.text
    url = 'https://api.openweathermap.org/data/2.5/weather?q='+city+'&units=metric&lang=ru&appid=50ea35c7b6eded0eb9dc2a89a662b482'
    jsondata = requests.get(url).json()
    temp = jsondata['main']['temp']
    clouds = jsondata['clouds']['all']
    usertep = 'Temp in you city  is' +str(temp)+ 'C'
    # usercloud ='Clouds   ' +clouds
    myBot.send_message(message.chat.id, usertep)
    # myBot.send_message(message.chat.id, usercloud)

myBot.polling()
