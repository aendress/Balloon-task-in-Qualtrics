# Balloon-task-in-Qualtrics
This is the codes about Balloon Analogue Risk Task which can be deployed in Qualtrics.

What you need to do:
 
 1. Adding the html codes into Qualtrics. You can do this clicking the "HTML View" when you edit questions in Qualtrics.
  
 
 2. Adding Javascript codes in Qualtrics. You can refer to the Qualtrics Support to know how to add javascript, here is the link:       https://www.qualtrics.com/support/survey-platform/survey-module/question-options/add-javascript/
  
  
 3.Upload the Balloon image to your Qualtrics library, and change the link address of the picture. After you upload the image successfully, you could find the link in your library.
  
  
 4.In the "survey flow", add "Set Embedded Data" to save the data. The codes are as below: 
       exploded = ${e://Field/number_pumps}
       number_pumps= ${e://Field/number_pumps}
       
 
 5.Run the game and check the data.
