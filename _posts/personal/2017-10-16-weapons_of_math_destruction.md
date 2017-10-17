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


Another threat is coming from online advertising. In this section of the book author explores the how online advertising is used to create a WMD on behalf of the for-profit colleges and leave students with huge student loans.

- Online advertising and predatory ads are define the genre of the WMDs.
- Online profit college ads are targeting isolated, impatient individuals with low self-esteem.
- With machine learning, a fast-growing domain of artificial intelligence, the computer dices into the data, following only basic instructions. The algorithm then finds patterns on its own, and then, through time, connects them with outcomes. In a sense, it learns.
- A machine learning algorithm in contrast to Human learning, will often require millions or billions of data points to create its statistical models of cause and effect.
- But with the internet, people across the earth have produced quadrillions of words about our lives and work, our shopping, and our friendships. By doing this, we have unwittingly built the greatest ever training corpus for natural-language machines. As we turned from paper to e-mail and social networks, machines could study our words, compare them to others, and gather something about their context.  
- The programs "know" what a word means, at least enough to associate with certain behaviors and outcomes, at least some of the time.
- Yet a crucial component of a WMD is that it's damaging to many people's lives, and with these types of predatory ads, the damage doesn't begin until students start taking out big loans for their tuition and fees.
- Research created by CALDER found that diplomas from for-profit colleges were worth less in the community colleges and about the same as a high school diploma. And yet these colleges cost on average 20 percent more than flagship public universities.
- For-profit colleges, sadly, are hardly alone in deploying predatory ads, payday load industry operates WMDs too.

WMDs are also present in civil justice area, where police departments across USA using predictive software programs, and unwillingly creating WMDs. These predictive softwares are creating a vicious feedback loop that creates a huge racial profiling unknowingly.

- Predictive software programs like PredPol used in budget-strapped police departments, that predicts the hot-spots, which has a potential to have a crime occur.  
- PredPol doesn't target individual but targets the geography.
- However when police setup the system they have choice to select either Part 1 crimes (violent crimes, like homicide, arson, assault) or Part 2 crimes (vagrancy, aggressive panhandling, selling and consuming small amounts of drug)
- Including Part 2 crimes skew the model and creates a pernicious feedback loop.  
- Policing itself spans new data in part 2 crime sites which justifies more policing, and our prisons are fill up with hundreds of thousands of people found guilty of victimless crimes, most of them from black and hispanic neighbors because the model feeds their neighbors. This is not color blind

There is inequality even in the job applications caused by WMDs nowadays. The models that reads and predicts the availability, fitness of the applicant by looking at resumes and personality test results. It doesn't really matter if you are top-notch applicant, the machine/model could mark you with it's read flags.

- A perfect SAT or a school with high ranking in USA does not help to beat the vicious feedback loop of WMD that decides which applicant to call for an interview.  
- Personality tests are used as a criteria in algorithms, primary purpose of the test  is not to find the best employee but to exclude as many as people as cheaply as possible.  
- 72 percent of CVs or resumes are not seen by human eyes, but by computers pulling out the skills and experiences that employee is looking for.  
- So crafting CV and Resumes is very crucial in job specific level.
- There are somethings that machines cannot process in cv or the algorithm is simply not built to except them, like images, or fancy fonts.  
- Using Ariel and Courier fonts, and not including images or different inserts is the best way to avoid trashing your resume by machine.
- WMDs are designed to cut administrative costs and to reduce the risk of bad hires (or ones that might require more training.) The objective of the filters, in short, is to save money.  
- Naturally many hiring models attempt to calculate the likelihood that each job candidate will stick around.
- There are different correlation to get the metric that calculate the likelihood of candidate leaving, such as type of person, or geography (the place the candidate live)

Another example of WMD author uses in another section is how scheduling models are creating unbalanced schedules for people working.

- _"Clopening"_, that’s when an employee works late on night to close the store or café and returns a few hours later, before down to open it.
- These irregular schedules are a product of the data economy.
- Scheduling tech has its roots in a powerful discipline of applied math called "operations research, or OR"
- This means using big scheduling modes, big retailers and restaurants can twist the workers' lives to ever-more-absurd schedules without suffering from excessive churn.
- These WMDs are massive, and it's entirely opaque. Workers don't have clue about when they'll be called to work.  
- The model is optimized for efficiency and profitability, not for justice or the good of the "team." (Nature of the Capitalism)
- Intelligence Systems are depended on the feedback they receive(error feedback, false positives) to delve into forensic analysis and figure out what went wrong, what was misread, what data was ignored, that's how the systems improve. However loads of WMDs from recidivism models to teacher scores, blithely generate their own reality.

Calculating credit scores are also in hands of WMDs.

- FICO an algorithm devised by Earl Isaac and Bill Fair, evaluates the risk that an individual would default on a loan.
- This score was color blind and the criteria taken into account were clear and known.
- Today we're added up to it in every conceivable was as statisticians and mathematicians patch together a mishmash of data, from our zip codes and Internet surfing patterns to our recent purchases.  
- Many pseudoscientific  models attempt to predict our creditworthiness, giving each of us so-called e-scores, unlike FICO, they resemble, e-scores are arbitrary, unaccountable, unregulated, and often unfair-in short, they are WMDs.
- Nasty feedback loop created by e-scores: E-scoring system will give person lives in a low-income (demographic) area  a low score thus the loans will have higher interest rate and more advertisement about credit cards, which will put the buyer into a worst place.
- There are a lot of data points called proxies are used to calculate e-score. E-scores nourished by millions of proxies exist in the shadows.
- Errors caused by algorithm because of the name similarity is so often, in 2013 5% of the people reported an error.


There are couple of more examples in the book, that I won't put it here. In the book author visited different areas of life; schools, colleges, courts, workplaces, and she showed us the destructive usages of misused math as WMDs. However she also gives some ideas about how we can regulate these WMDs and possibly stop them:

- Injustice, whether based in greed or prejudice, has been with us forever, and WMDs are reflecting it since the humans are the ones writing their algorithm.
- Big Data Processes codify the past. They do not invent the future.
- She is suggesting an oath something like Hippocratic Oath, one that focuses on the possible misuses and misinterpretations of math in the models.
- To eliminate WMDs, we must advance beyond establishing the best practices in our data guild. To change our laws in data guild we need to reevaluate our metric of success.  
- Nowadays, success of a model is measured in terms of profit, efficiency, or default rates.  
- To disarm WMDs, we also need to measure their impact and conduct algorithmic audits.


What I would take from this book is that Big Data has a huge influence in our life, but currently the way we use it and take advantage of it just increases the inequality and bias, which effects millions of people in a very depressing way. Big data is one of the strongest super powers of our century, and if we keep using it for power and profit by ignoring human rights and actual fairness we'll create a community which will never come back from. So everyone should be careful about these sinister misused models, and people who works on the industry should come up with strict regulations before it would leave an irreversible mark on our society.

> This is my notes from the book. Most of the bulletin points are exactly quoted from the book. I wanted to combine my views and review about the book with exact quotations from the book, and I hope I could've achieved it.
