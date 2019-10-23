# Evaluating Videogrep + Pocketsphinx with Singaporean English

I did this to quickly 1) evaluate how the inbuilt PocketSphinx handles varying "intensities" of Singaporean english and 2) see how digestable the supercuts are vs watching the entire video to quickly isolate subject matter or when gisting a video.

The following videos were used:
- [Joker - Movie Review](https://www.youtube.com/watch?v=1gzdlfCp2Iw) by chris Stuckman for American english
- [Singapore National Day Rally 2019 speech](https://www.youtube.com/watch?v=bINTmky4vCA) by PM Lee for more "proper" and formal Singaporean English
- [Learning Singlish (Singaporean English) - Xiaxue's Guide To Life: EP178](https://www.youtube.com/watch?v=pb4XSy-d2Ck) by Xiaxue for everyday grammatically 'OK' Singlish and what I (personally) think is the most common kind of Singpaorean tongue.

I'm so sorry I picked Xia Xue but it kind of reflects our "english-based creole language" the best I think. I didn't realise it was loaded with hokkien vulgarities but on hindsight its XX, what did I expect?

Also, all the videos have decent Subs. I will also use pocketsphinx to generate subs you can compare yourself.

## Overall Impressions

### #1 Pocketsphinx
In general the transcriptions are bad for #3. How bad? You could open them and take a look yourself but I think you can just trust me. 

However its not a lost cause, you can [train](https://cmusphinx.github.io/wiki/tutorialam/) or [adapt](https://news.ycombinator.com/item?id=11174762) it like [this guy](https://news.ycombinator.com/item?id=11174762) but its not trivial. I think Singlish can count as a language or dialect.

In their [own words](https://cmusphinx.github.io/wiki/tutorialam/):

>## When you need to train
>You need to train an acoustic model if:
>
>- You want to create an acoustic model for a new language or dialect
>- OR you need a specialized model for a small vocabulary application
>- AND you have plenty of data to train on:
> - 1 hour of recording for command and control for a single speaker
> - 5 hours of recordings of 200 speakers for command and control for many speakers
> - 10 hours of recordings for single speaker dictation
> - 50 hours of recordings of 200 speakers for many speakers dictation
>- AND you have knowledge on the phonetic structure of the language
>- AND you have time to train the model and optimize the parameters (~1 month)
>## When you don’t need to train
>You don’t need to train an acoustic model if:
>
>- You need to improve accuracy – do acoustic model adaptation instead
>- You do not have enough data – do acoustic model adaptation instead
>- You do not have enough time
>- You do not have enough experience
>Please note that the amounts of data listed here are required to train a model. If you have significantly less data than listed you can not expect to train a good model. For example, you cannot train a model with 1 minute of speech data.


### #2 Supercut-ting stuff
I don't particualrly find it useful to supercut, perhaps there needs to be a greater amount of padding around the words of interest. Also the search is like a simple string match, even case-sensitive so I just put partial strings like "ingapore" to catch all Singapore/singapore/singaporean/singaporeans. However there are more interesting things like searching for adjectives and nouns. I guess its a quick way to find snippets in super long videos that you would otherwise play at x2 speed to gist.

If you're ready to play, here are the instructions.

## Install Videogrep and youtube-dl

The instructions [here](http://antiboredom.github.io/videogrep/) went mostly ok on my mac.

Don't forget to `brew install youtube-dl`

I also had to install xcode and already installed ffmpeg previously. Its pretty much a bit of an adventure but still easier than putting Videogrep together.

## Get the videos, subs and transcriptions, create supercut

### Video 1
```
youtube-dl http://youtube.com/watch?v=rnyuxpky1Cw --write-auto-sub
videogrep --input ./Joker\ -\ Spoiler\ Review-rnyuxpky1Cw.mkv --transcribe
videogrep --input ./Joker\ -\ Spoiler\ Review-rnyuxpky1Cw.mkv --search 'Joker' --use-vtt --output "Joker - supercut-youtube-subs.mp4"
videogrep --input ./Joker\ -\ Spoiler\ Review-rnyuxpky1Cw.mkv --search 'Joker' --use-transcript --output "Joker - supercut-pocketspinx-transcription.mp4"
```

### Video 2
```
youtube-dl https://www.youtube.com/watch?v=wa5rgV3eti0 --write-auto-sub
videogrep --input ./National\ Day\ Rally\ 2019-bINTmky4vCA.mp4 --transcribe
videogrep --input ./National\ Day\ Rally\ 2019-bINTmky4vCA.mp4 --search 'ingaporean' --use-vtt --output "National Day Rally 2019-bINTmky4vCA - supercut-youtube-subs.mp4"
videogrep --input ./National\ Day\ Rally\ 2019-bINTmky4vCA.mp4 --search 'ingaporean' --use-transcript --output "National Day Rally 2019-bINTmky4vCA - supercut-pocketspinx-transcription.mp4"
```

### Video 3
```
youtube-dl http://youtube.com/watch?v=rnyuxpky1Cw --write-auto-sub
videogrep --input "./Learning Singlish (Singaporean English) - Xiaxue's Guide To Life - EP178-pb4XSy-d2Ck.mkv" --transcribe
videogrep --input "./Learning Singlish (Singaporean English) - Xiaxue's Guide To Life - EP178-pb4XSy-d2Ck.mkv" --search 'apore' --use-vtt --output "Learning Singlish (Singaporean English) - Xiaxue's Guide To Life - EP178-pb4XSy-d2Ck - supercut-youtube-subs.mp4"
videogrep --input "./Learning Singlish (Singaporean English) - Xiaxue's Guide To Life - EP178-pb4XSy-d2Ck.mkv" --search 'apore' --use-transcript --output "Learning Singlish (Singaporean English) - Xiaxue's Guide To Life - EP178-pb4XSy-d2Ck - supercut-pocketspinx-transcription.mp4"
```