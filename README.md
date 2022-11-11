<!--
**gregsoos/gregsoos** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.
-->

# Welcome to my GitHub profile!

My name is **Greg Soos** (he/him). I'm a former physics researcher who's done work in classical physics, experimental particle physics, and most recently computational astrophysics. This journey has led me to interact with and/or learn a variety of programming languages.

My introduction to coding began earlier, however, during my first two years of undergraduate study. At **Cal Poly, San Luis Obispo**, I majored in aerospace engineering and learned MATLAB as a requirement in my classes thanks to its ubiquity in the field. I was not long for the aerospace life however, and decided after my sophomore year to change not just my major, but my university too.

I spent my last two years of undergraduate study at the **University of Pennsylvania**, earning a Bachelor of arts in physics with a minor in mathematics. Through both my classes and research there, I picked up a variety of languages, chief among them being Python. 

In the hopes of showcasing some of those skills I've picked up, I've uploaded a variety of my code from the past six years in a number of repositories. If you're not me and you're reading this, and you're actually interested in seeing any of that, I hope you enjoy! 

---

## Python

<details>
<summary>Perceptron</summary>
The perceptron represents one of the earliest great leaps for machine learning. Invented in 1943 by Warren McCulloch and Walter Pitts[^1], and first put into application in 1958 by Frank Rosenblatt[^2], the idea is quite simple. You give the perceptron a certain input, and the perceptron responds by telling you whether that input belongs to a specified class. For example, say we want our perceptron to tell us whether something is a quadrilateral. We give it a series of many quadrilaterals and non-quadrilaterals (circles, triangles, etc.), and over time the perceptron should "learn" to distinguish quadrilaterals from non-quadrilaterals.

In practice, the perceptron is quite rudimentary and has limitations to achieving 100% identification. However, given enough time to learn, the perceptron can become significantly better than random guessing. Below, I will include a sample of code and a repository link for a perceptron I programmed to distinguish filled-in rectangles from unfilled rectangles. After 100,000 trials of randomly generating either a filled or unfilled rectangle, the perceptron was able correctly to identify the rectangle class roughly 67% of the time.

[^1]: McCulloch, W; Pitts, W (1943). ["A Logical Calculus of Ideas Immanent in Nervous Activity"](https://www.bibsonomy.org/bibtex/13e8e0d06f376f3eb95af89d5a2f15957/schaul). Bulletin of Mathematical Biophysics. 5: 115–133.
[^2]: Rosenblatt, F. (1958). [The Perceptron: A Probabilistic Model for Information Storage and Organization in the Brain](https://psycnet.apa.org/doiLanding?doi=10.1037%2Fh0042519). Psychological Review, 65(6), 386-408.

```Python
#Let's generate the weight array for a given n trials (say, let's start with 100k)
#I'm not sure how it'd affect the weights if we did an uneven number of filled vs. unfilled
#But for now, I'll just do an equal number (50k each), switching off between them after each trial
trials=100000
bias=0
weights=np.zeros((20,20), dtype=int)
acc_counter = np.array([]) #We'll add a 1 for correct identification and 0 for improper identification
i=0
while i<trials:
    if i%2==0: #Determing if even; even will be filled rectangles; then dot rectangle with weights
        xlength_fill=random.randint(2,19); ylength_fill=random.randint(2,19)
        xcorner_fill=random.randint(0,19-xlength_fill); ycorner_fill=random.randint(0,19-ylength_fill)
        randomrectangle_fill = np.zeros((20,20), dtype=int)
        randomrectangle_fill[ycorner_fill:(ycorner_fill+ylength_fill+1),xcorner_fill:(xcorner_fill+xlength_fill+1)]=int(1)
        weightedactivation=np.dot(weights.flatten(), randomrectangle_fill.flatten())
        if weightedactivation>bias: #Is the dot product greater than bias? If it is, fire; else, don't
            weights=weights #Correctly identified filled rectangle, weights unchanged
            acc_counter = np.concatenate((acc_counter, np.array([1])))
        else:
            weights=weights+randomrectangle_fill  #Improper identification, change weights
            acc_counter = np.concatenate((acc_counter, np.array([0])))
                     
    elif i%2==1: #Determine if odd; odd will be unfilled rectangles; then dot rectangle with weights
        xlength_notfill=random.randint(2,19); ylength_notfill=random.randint(2,19)
        xcorner_notfill=random.randint(0,19-xlength_notfill); ycorner_notfill=random.randint(0,19-ylength_notfill)
        randomrectangle_notfill = np.zeros((20,20), dtype=int)
        randomrectangle_notfill[ycorner_notfill:(ycorner_notfill+ylength_notfill+1),xcorner_notfill]=int(1) #Fill in left side
        randomrectangle_notfill[ycorner_notfill:(ycorner_notfill+ylength_notfill+1),xcorner_notfill+xlength_notfill]=int(1) #Fill in right side
        randomrectangle_notfill[ycorner_notfill,xcorner_notfill:(xcorner_notfill+xlength_notfill+1)]=int(1) #Fill in top side
        randomrectangle_notfill[ycorner_notfill+ylength_notfill,xcorner_notfill:(xcorner_notfill+xlength_notfill+1)]=int(1) #Fill in bottom side
        weightedactivation=np.dot(weights.flatten(), randomrectangle_notfill.flatten())
        if weightedactivation>bias:
            weights=weights-randomrectangle_notfill #Improper identification, change weights
            acc_counter = np.concatenate((acc_counter, np.array([0])))            
        else:
            weights=weights #Correctly identified unfilled rectangle, weights unchanged
            acc_counter = np.concatenate((acc_counter, np.array([1])))

    else:
        print 'Error in counter.'
    i=i+1
```
If the details of what the weights, bias, dot products, etc. all mean in the above context, don't worry! Just check out my repository where I explain all this in the readme.
</details>

## MATLAB

<!--
## Mathematica
## R
## C++
-->

Hey! If you're still reading this far down, mind if I self-promote one thing? One of my biggest passions is physics, and in the years since college, I started a YouTube channel to go through some physics problems from undergraduate and graduate textbooks. If that interests you, the channel is called [Greg Does Physics](https://www.youtube.com/channel/UCowsP9riC0Jspn6ndGpfzqA). Check it out if you want!



<picture>
 <source media="(prefers-color-scheme: dark)" srcset="https://upload.wikimedia.org/wikipedia/commons/9/92/UPenn_shield_with_banner.svg">
 <source media="(prefers-color-scheme: light)" srcset="https://upload.wikimedia.org/wikipedia/commons/9/92/UPenn_shield_with_banner.svg">
 <img alt="Coat of arms of the University of Pennsylvania" src="https://upload.wikimedia.org/wikipedia/commons/9/92/UPenn_shield_with_banner.svg">
</picture>

Another way of inputting a picture is like this:
![A picture of the Cal Poly arms](https://upload.wikimedia.org/wikipedia/en/d/d9/CalPoly_Seal.svg)

<sub>1</sub> <sup>2</sup>H (Deuterium for life baby) <sub> Oh gosh it doesn't look right </sub>
Added backticks let's us do this: `git push`
Let's try referencing a file from another repository. I made a [file called `index.md`](/../../../communicate-using-markdown/blob/main/index.md/) in another GitHub skills tutorial. :+1:
\#Escaping Markdown syntax by putting a backslash first
