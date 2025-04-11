# Balloon-task-in-Qualtrics

## Installation
Here are the codes and images that you may need to deploy Balloon Analogue Risk Task into Qualtrics. 
1. HTML page
2. Javascript code
3. balloon_new.png

The steps you should follow to make the BART function well in Qualtrics:
 
 1. Put the HTML codes into Qualtrics. You can start a new question in your survey, then click the "HTML View" where you edit questions in Qualtrics. Just copy and paste the codes I have uploaded (HTML page).
 
 2. Put Javascript codes in Qualtrics. You can refer to the Qualtrics Support to know how to add javascript, here is the link: https://www.qualtrics.com/support/survey-platform/survey-module/question-options/add-javascript/. Just copy and paste all the codes I have created (Javascript code).
 
 3.Download the balloon picture and upload the Balloon.png to your Qualtrics library, and change the related link address of the picture. After you upload the image successfully, you could find the concerned link address in your Qualtrics library.
 And find the code you need to revise:   <img src=https://erasmusuniversity.eu.qualtrics.com/ControlPanel/Graphic.php?IM=IM_e40vZ7nffgjMnul id="ballon" alt="Ballon">, which you could find this in the HTML.
 
 4.In the "survey flow", add "Set Embedded Data" to save the related data by clicking on the "add a new element here". The codes are as below: 
       
       exploded = ${e://Field/exploded}
       number_pumps = ${e://Field/number_pumps}
       total_win = ${e://Field/total_win}
       
 Note that you need to create block of "set embedded data" AFTER the balloon block. Please refer to the picture named "embedded data".
       
 5.Run the game and check the data.

## Details 

### Difference from Lejuez et al, 2002 https://pubmed.ncbi.nlm.nih.gov/12075692/ and http://people.uncw.edu/ogler/Experimental/Fall%2008%20Final%20Paper%20Resources/BART.pdf

#### Probablity of bursting and number of trials

In Lejuez et al, 2002, there were 30 trials for each of three balloons associated with different probabilities of explosion. For the blue balloon:

> The probability that a balloon would explode was arranged by constructing an array of N numbers. The number 1 was designated as indicating a balloon explosion. On each pump of the balloon, a number was selected without replacement from the array. The balloon exploded if the number 1 was selected. For example, the array for blue balloons contained the integers 1–128. Thus, the probability that a blue balloon would explode on the first pump was 1/128. If the balloon did not explode after the first pump, the probability that the balloon would explode was 1/127 on the second pump, 1/126 on the third pump, and so on up until the 128th pump, at which the probability of an explosion was 1/1 (i.e., 100%).

Two other balloons were used with maximal numbers of pumps of 8 and 32, respectively. However, the correlation between risk taking (as measured by BART) and other measures of risk taking were strongest for the blue balloon, which is thus used here (see Magin et al., for a review, https://www.frontiersin.org/journals/neuroscience/articles/10.3389/fnins.2023.1237734/full)

To adjust the probability of bursting, change the following code:

```
var maximal_pumps=32;
```

To adjust the number of trials, change the following code

```
var rounds_played = 10;
```


### Scoring 

Each successful pump adds 0.25 points to present_win (the amount for the current round). To change this, change the following code (lines 166/167)

```
pumps += 1;
present_win +=0.25;
```


## Other

The "tada" sound is from https://freesound.org/s/397353/

The explosion sound is from https://freesound.org/s/563197/


