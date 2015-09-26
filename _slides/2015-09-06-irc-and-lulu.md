---
title: IRC and Lulu
description: >
  This is a workshop for HacSoc "OpenHacks".  Learn about the basics of IRC: how
  to log in, what the jargon means, and how to use it for fun and profit.
  Finally, meet our IRC bot "Lulu", and learn how to hack new features into it!
layout: presentation
theme: night  
---

{{site.startslide}}

# IRC and Lulu

OpenHacks 9/6/15

Stephen Brennan

{{site.endslide}}
{{site.startvertical}}
{{site.startslide}}

## What is IRC?

- **I**nternet **R**elay **C**hat
- A chat protocol used all over the world.
- Anyone connected to the same server can chat with others on it.
- We host our own [IRC server](http://irc.case.edu)!

{{site.nextslide}}

## What isn't IRC?

- Private!
    - Anyone can log onto IRC, and possibly log conversations.
- Facebook chat
    - IRC doesn't save messages for you.  If you're not connected, you may miss
      something.

{{site.nextslide}}

## So why should I use it?

- Great instant communication among HacSoc members.
- Good for getting quick answers.
- Create discussion channels for any topic or class.
- Good experience: some companies have internal company-wide IRC.
- Plus, it's fun!

{{site.nextslide}}

## Where do I sign up?

- There's no sign-up!  Just connect and go.
- Mibbit web client: <http://irc.case.edu>
- Download a client.
    - Windows: [HexChat](https://hexchat.github.io/)
    - Mac: [LimeChat](http://limechat.net/mac/)
    - Linux: XChat (gtk), or Konversation (KDE).
        - Get these from your package manager
    - iOS: I hear LimeChat has a mobile version
    - Android:
      [AndroIRC](https://play.google.com/store/apps/details?id=com.androirc)

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## How does it work?

- First, you connect to the server (I'll cover that shortly).
- Then, you choose a *nickname*.  This is like a username.
    - IRC doesn't by default protect your nick.
    - I'll cover how to keep others from using it.
- Next, join some *channels*.  These are just "chat rooms".

{{site.nextslide}}

## Connecting

- Server: irc.case.edu
- Port: 6697
- Use SSL? Yes.
    - If you see an option to accept invalid certificates, enable it.  If you
      see warnings about invalid certificates, ignore them (sorry!).

{{site.nextslide}}

## Choosing a nick

- Your client may offer a textbox when you connect.
- Otherwise, use the command `/nick [your nickname here]`.
    - This is an IRC command!

{{site.nextslide}}

## IRC Commands

- Besides just sending messages to channels, IRC has some commands you can use.
- All clients allow you to do commands by starting your message with a `/`
  (forward slash).
- Many clients give you GUI options to run these commands.
    - I can't teach you every GUI, but I can teach you what the commands are.

{{site.nextslide}}

## Some commands

- `/list` - list all channels on the server
- `/join #channel` - joins the channel `#channel` (creates it if it doesn't
  exist).
- `/part [#channel]` - leave a channel
- `/msg username message` - sends `username` a `message` directly (only they see
  it).
- `/me [message]` - "emote" your message.
    - EG: If I send `/me laughs`, the channel will see `brenns10 laughs`.

{{site.nextslide}}

## Keeping your nick safe

- "`NickServ`" prevents others from using your username.
- It associates a password with your nickname.
- `/nick [whatever-you-want]`
- `/msg NickServ register [password] [email]`
- `/msg NickServ set kill on`
- Each time you connect:
    - `/msg NickServ identify [password]`

{{site.nextslide}}

## Making it all easier

- Most clients make IRC very easy.
- They remember the channels you use.
- They can automatically set your nick.
- They can automatically identify you to `NickServ`.

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## CWRU IRC channels

- `#cwru` - general conversation, "lobby".  **Most conversation happens here**.
- `#acm` - conversation related to our ACM chapter
- `#ieee` - conversation related to our IEEE chapter
- `#hackers` - conversation related to HacSoc
- `#eecs132` - you can have a channel for any class you're in!
- Create your own for any topic you'd like.  `/invite` your friends in!

{{site.nextslide}}

## CWRU IRC people

- `siretrm` - Thomas Murphy
- `mason` - Andrew Mason
- `brenns10` - Stephen Brennan
- `jay_wild` - Aidan Campbell
- Feel free to ask anyone on IRC who they are, but they may prefer to keep their
  identity private.

{{site.nextslide}}

## Meet Lulu!

- Lulu is our IRC chatbot!
- It exists to make IRC more fun.
- `lulu, pug me` - gives you a picture of a pug
- `lulu, kitten me` - gives you a picture of a kitten
- `lulu, youtube me [query]` - searches YouTube and gives you a link
- Lots more commands at <http://hacsoc.org/lulu>.

{{site.nextslide}}

## How does Lulu work?

- Lulu is based on GitHub's bot, Hubot.
- We have our own fork.
- Its source lives at <https://github.com/hacsoc/lulu>
- It's written in [CoffeeScript](http://coffeescript.org), a language that
  compiles to JavaScript.

{{site.nextslide}}

## Can I make Lulu do more cool stuff?

Why yes, yes you can!

- First, install [Node](https://nodejs.org/en/) (if you use Linux, use your
  package manager).
- Then, fork [Lulu](https://github.com/hacsoc/lulu) on GitHub.
- Then, clone your copy of Lulu.
- Run `npm install` in the root of your clone.
- Run `bin/hubot` to run Lulu on your terminal.

{{site.nextslide}}

## Making Lulu plugins

- Write your plugin in the `scripts/` directory, using either Javascript or
  CoffeeScript.
- Test it by doing `bin/hubot`.
- When you're done, git commit, git push, and create a pull request!
- Hubot Documentation:
    - <https://hubot.github.com/docs/>
- Look at the code for other scripts to help you get started.

{{site.endslide}}
{{site.endvertical}}

{{site.startslide}}

## Conclusion

- That's all I have for IRC!
- Lulu is ready for your pull requests.
- We'll see you on IRC!

Questions?

{{site.endslide}}
