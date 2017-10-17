---
 layout: post		
 title: Weapons of Math Destruction
 excerpt:		
 categories: personal		
 tags: ["Book Summary"]		
 published: true		
 comments: true		
 share: true		
 image:
    feature: WeaponsOfMathDestruction_BookSum.jpg
    credit: Enes Kemal Ergin
---

[Weapons of Math Destruction](https://www.goodreads.com/book/show/28186015-weapons-of-math-destruction) is a book by [Cathy O'Neil](https://twitter.com/mathbabedotorg) (also the author of the blog called [mathbabe](https://mathbabe.org/)) which I can define in 4 words: captivating, haunting, honest, and enlightening.

## Weapons of Math Destruction: How Big Data Increases Inequality and Threatens Democracy

I've found myself reading books about technology more than ever. Starting with [The Second Machine Age](https://www.goodreads.com/book/show/17986396-the-second-machine-age), [Weapons of Math Destruction](https://www.goodreads.com/book/show/28186015-weapons-of-math-destruction), and currently reading [Machine, Platform, Crowd](https://www.goodreads.com/book/show/32606599-machine-platform-crowd), they are the ones that I've finished any many more is in my to read list. But why am I interested in reading these? Answer is really simple, because I want to know what are the larger scale effects of the technologies that I am using, developing in daily basis. These concepts are not taught in the class or practiced in any project. __We as developers or as users, should be aware of the effects of the technology to come up with better solutions, policies, and bridges to connect user and application.__

The book [Weapons of Math Destruction](https://www.goodreads.com/book/show/28186015-weapons-of-math-destruction) is a little different than other books that I am reading, in terms of its tone. __The tone of the author is more warning and notice of the mathematical algorithms, and their chaotic effects on the large scale than the overview of new emerging technologies.__ One can see the darker tone in the book, and cannot take him/herself from thinking that how math and computer science is in everything and changing our life in a way that needs regulation. It needs regulation because the systems they are using is feeding a negative feedback to the system which creates inequality in a greater scale every time its being put to use.

The author touches so many ethical dilemmas created by these WMDs [(__W__)eapons of (__M__)ath (__D__)estruction)] and gives reader a space to think about them. __The reason that WMDs are creating ethical dilemmas is that they penalize the poor, the ethnically diverse, or simply the non-target audience of the profit WMDs.__


As a developer of Machine Learning technologies, I use math, statistics, and data science quite a lot. And learning that intentionally or un-intentionally misusing those methods could result in catastrophic effects in the large scale. That's why the points I get from this book is really important for me. By reverse engineering the WMDs, I get what I should be doing and be more careful to.


After giving my review about the book, let me also share some of the notes taken from the book:

Author is going over different areas in each chapter to show the cause and effects of each WMDs populating the area with unequalities, and feedback loops that is creating more and more imbalance. In each WMD we see in the book, the author explains how opaque the model, the scale and the damage of the models.

The book starts with the teacher assesment tool IMPACT, by introducing IMPACT and it's impact (:D), author shows the main 3 features which makes WMD, a corrupted use of mathematics. Here are the 3 main features:

- __Opacity:__ This part comes from how hidden the algorithm is, do the users know how it works, or even it's existence in the first place.
- __Scale:__  This part comes from the effects increases exponentially to large number of people, creating a never seen before effects.
- __Damage:__ This part comes from the results penalizing the poor, or ethnically diverse, or simply the non-target audience.


These algorithms misuse of math and statistics, by taking variables in a fashion that will make it a biased. Taking account of variables that they could easily obtain and measure is not always the ones important to use as a prediction base. So there are a lot of variables left out and most of the time they are the most complex and correlated ones.

Another big issue with these misused algorithms, is that they don't have a good feedback mechanism, meaning that it cannot update the importance of the variables (commonly used as weighting variables) or simply selecting variables to use for the job at hand.

- Statistical systems require feedback, statisticians use errors to train their models and make them smarter.  
- Without feedback, however, a statistical algorithm can continues spinning out faulty and damaging while never learning from its mistakes.
- WMDs is the same, they define their own reality and use it to justify their results. This type of model is self-perpetuating, highly destructive, and very common.
- WMDs as in their nature is secretive. They don't give away how the algorithm works, which parameters used and variables accounted for. Only the analysis is outsourced to coders and statisticians and they let the machines do the talking. (__They Opaque__)

The tactics used in baseball teams are perfect example of math and statistics usage. They create models to analyze their opponents and devise their play accordingly. After each play they feed whatever they learn from the play into their model to refine it. That's how trusthworthy models should operate. They maintain a constant back-and-forth with whatever in the world they're trying to understand or predict. Conditions change, and so must the mode.

A model is nothing more than an abstract representation of some process, be it a baseball game, and oil company's supply chain, a foreign government's actions, or a movie theater's attendance. And a dynamic model is when you constantly update and adjust the model with feedback.

- There would always be mistakes, however, because models are, by their very nature, simplifications. No model can include all of the real world's complexity or the nuance of human communication.  
- Our own values and desires influence our choices, from the data we choose to collect to the questions we ask. Models are opinions embedded in mathematics.  
- The quality of the model does not correlate with the complexity of the models, sometimes the simple one variable models prove the be very effective on the task they needed to be doing, like smoke alarms.
- __Signature quality of WMD is a toxic feedback loop that contributes and sustains inequality.__
- Baseball models are healthy, they are transparent, and continuously updated, with assumptions and conclusions are interpretable and clear to see.
- __So to sum up, these are the three elements of WMD: Opacity, Scale, and Damage. All of them will be present, to one degree or another.__


The biased models are everywhere. They are infiltrated our lifes from job applications to civil justice, and they have huge effects. Author is mentioning the role of biased financial models is huge in the market crash in 2008.

- People were using formulas to impress rather than clarify.
- I saw all kinds of parallels between finance and big data.  
- __Fallacious conclusion that whatever they're doing to bring in more money is good.__
- After a couple of years working and learning in the Big Data space, my journey to disillusionment was more or less complete, and the misuse of mathematics was only accelerating with incredible pace.  
- I quit my job as data scientist to investigate the issue of misusing math to gain.


Have you ever wonder how U.S. News rank the universities? or Have you ever wondered how they are so influential? In 1983 U.S.News and World report stated to evaluate 1,800 colleges and universities and rank them for their excellence. But how? Okay, features like SAT scores, AP classes, student-teacher ratio, acceptence rate is definetely a big factor and used but is it enough? Creating a system that higly accepted by the colleges and universities, created an unfair race.  

- First data driven ranking came out 1988, at first it was ok/bearable but when ranking grew to national standard, vicious feedback loop materialized.
- U.S. News college ranking is operates at great scale, inflicts widespread damage, and generates an almost endless spiral of destructive feedback loops, even though is less opaque than other WMDs the other things are enough to count ranking as WMD.  
- The schools are start to race to get better ranking on the list ever year, and sometimes taking it as far as cheating by lying about the scores.
- Even though it created a WMD and have devastating effects, we cannot say that it's all negative. It kind of created a competitive environment where school has to improve every year to be able to get better ranking.
- However this nice looking competition is also resulted in increasing the tuition.
- Between 1985 and 2013, the cost of higher education rose by more than 500 percent, nearly four times the rate of inflation.
- This increase in the tuitions could be explained by the spending of universities to attract students, like building new stadium, dorm, gyms, etc.
