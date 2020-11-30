## NaNoGenMo with P.G. Wodehouse

### Summary
Train a TensorFlow model on P.G. Wodehouse, produce some novels, then name them with NLP and make bad cover art like so: 
![anything_make_way_eye_say_cover.png](attachment:anything_make_way_eye_say_cover.png)
- [Apologia](#apologia)
- [Technical Details](#technical_details)
- [Conclusion](#conclusion)
- [Sources](#sources)

### <a>apologia</a>Why this is a terrible idea, but I did it anyway

I'd been meaning to participate NaNoGenMo for a while now and while I certainly didn't expect that 2020 would be the year I'd do so. But I found myself with some free time I hadn't expected at the end of November.

I'd hoped to do something a little more interesting than this; I'd generally rather be playing with language and NLP directly, as I have with my TwitterBots. In  fact, it might have been a better use of my time to revisit the damned deployment flow for the bots, because that's generally what stops me from working on them. Maybe my goal for NaNoGenMo next year will be to accumulate 50,000 lines of narrative Tweets...

But I'd also wanted to play around with TensorFlow, having taken at least two extremely ~~boring~~ predictable workshops on the subject (yes, we see, regression of real estate prices sure is a thing!). I had also seen several articles about generating text based on particular authors, which was more in my wheelhouse, if terrible passé; I think this was hot in 2017 or so. I'm not really sure what the new hotness is, nor do I want to know.

Anyway. My favorite English-writing author is P.G. Wodehouse (hereafter PGW).

There are many ironies inherent in choosing PGW to train an AI model. He's generally regarded as one of the premiere comic stylists in the English language: his vocabulary borne of his English schoolboy reading (and inevtiably, England's colonialism too), his impeccable sense of comic timing in dialogue, and his generally sunny worldview, despite actually having been taken prisoner by the Nazis during WWII. 

None of these things were going to come through a machine learning algorithm and I knew that going in. 

A thing to know about comedy is this: is generally relies on surprise. It's a whole big thing and I'm gnot going to get into it, but I wrote a disseration on this subject a long time ago, so please trust me on this one point. So, for example, one of PGW's stylistic tricks is picking just the word you *wouldn't* expect.

The thing is, machine learning relies on probability, i.e. correctly predicting patterns, not even of words, but of characters. It literally tries to guess the mostly likely character (or word) to come next. The opposite of surprise, really. 

So you can probably see where this is going.

Trying to train a model to write funny text is a fool's errand, and a waste of computing resources. While I normally delight in using "serious" technologies for silly goals, I actually felt guilty wasting my own and other people's CPUs on this task. (And actually

I knew that, without a doubt, the result would be mediocre at best, just as one would expect from an algorithm that generally thinks 80% is a good score.

But in the spirit of 2020, Camus, and our good friend Sisyphus, I did it anyway. I tried to pretend I was a tech utopianist and had hope that something good would come of this exercise, or at the very least, that even if it was knowably futile from the outset, it was still somehow worth doing, over and over and over again, like either a machine learning model or Sisyphus or both.

There's also the fact that if you're a woman in tech -- well, a woman in general -- you will never be judged on your potential, so it never hurts to have a Git repo to point to, in order to "prove" that yes, you can in fact use this sort of code. Just in case anyone needs to know that you're "technical" (which you will actually never be, by the way, because that's how this game works!!)

Anyway, I felt ethically bound to write this preface, to clearly demonstrate why this is all a terrible idea even though I did it.

### <a>technical_details</a> Technical details

First I scraped all of PGW's available writings from Gutenberg org. I wrote each work into a separate text file because I don't like to rely on internet access and I wasn't sure how much data munging I'd have to do so I didn't want to keep making requests.

Then I combined the texts into one large training set. Before combining them, I cleaned them as best I could, to remove any text that was written by Project Gutenberg people and not PGW.

Then I followed this [TensorFlow tutorial](https://www.tensorflow.org/tutorials/text/text_generation#attach_an_optimizer_and_a_loss_function) that showed how to use Tensorflow to generate text. It was relatively reasonable, I thought, and had some good explanations.

It also gave a good TL;DR of how machine learning works, and this article gets more in depth about the process.

Now, training the model takes a lot of time and CPU. And if you don't like the first set of results, one way to better the model, according to the article, is to let it train for more "epochs" (let's just define this as imaginary units of time that the machine overlords use), and I wanted to generate at least a few "well-trained" novels out.

It was already quite a pain in the ass to train for 10 epochs on my own laptop, so I figured I would use the magic of cloud computing to make my life easier.

It didn't take to long to set up my notebooks on Microsoft Azure and Google's Compute Engine; I think it took under an hour. But the training wasn't as reliable as I'd wanted, and it kept hanging. Ironically, the dedicated TensorFlow environment provided by Google's Compute Engine was the one that kept crapping out; Azure finally got through it and produced some text. 

(Did I mention that Google is, like, the inventor of TensorFlow? So you'd think their machines would do better. Oh, and when I was trying to find and sign into these platforms, I found so much copy going on about how great it was that you could totally train models without actually knowing anything about AI, as if this were a good thing. So many flashbacks to Gabriel de Quiroz's keynote for Data Day 2018, in which she pointed out that opacity is not actually a good thing.)

In fact, the model trained for 30 epochs was much, much worse than the one trained for 10. It was less sensical and less amusing! Oh, well.

The last step I needed was to give these novels a name. I used a modified version of keyword searching NLP (described in this [article](https://medium.com/analytics-vidhya/automated-keyword-extraction-from-articles-using-nlp-bfd864f41b34) to pull some words; I wasn't really looking for this to make sense.

Then, I figured there should be a cover. A word cloud seemed like exactly what this fiasco demanded. So I made that the cover art.



### <a>conclusion</a> Conclusion
The novels generated by machine are exactly as mediocre and unreadable as one might expect. I don't even think the texts are as entertaining as some of the other authors.

TL;DR: *Don't try to train AI to be funny.*

A better exercise for any aspiring writing is to try to emulate a particular author's style by hand.  In fact, a better exercise for anyone is try to sort through what patterns the machine is trying to recognize, and to think about the labels they're using to get there. But then you'd be putting yourself into the position of a lowly labeler, the people that AI "makers" are trying not to be. 

And or course it's worth asking if we want an algorithm making whatever decisions they're making, or why we are so hell bent on replacing all repeated human effort, even if said humans haven't asked to be replaced.

(I am certainly not the first to make this point. There are many, many other scholars and technologists who make these points, over and over.)



### <a>sources</a>Sources
- https://www.tensorflow.org/tutorials/text/text_generation
- https://medium.com/analytics-vidhya/automated-keyword-extraction-from-articles-using-nlp-bfd864f41b34
- https://web.stanford.edu/class/cs20si/2017/lectures/notes_05.pdf
- https://www.tensorflow.org/guide/checkpoint
- https://docs.microsoft.com/en-us/azure/machine-learning/how-to-train-tensorflow
- https://towardsdatascience.com/no-hassle-machine-learning-experiments-with-azure-notebooks-e1a22e8782c3
- https://www.tensorflow.org/tensorboard/tensorboard_in_notebooks
- https://www.tensorflow.org/guide/checkpoint#loading_mechanics
