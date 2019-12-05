# Christmas_Delay

Welcome to the README of the Christmas_Delay application. 

Prerequisites: 

To enjoy the full user experience, the Jupyter Notebook is needed. The download instruction can
be found under: https://jupyter.org/install (17.11.2019) There are no further prerequisites as 
all the needed libraries will be installed in the first lines of code. 

ATTENTION: Jupyter as well as Anaconda require the newest version to have the full user experience! 
Jupyter needs to be run at least on Version 6.0.2., whereas the anaconda version needed is at least 
1.9.7. The older Version includes some bugs, which makes this application not smoothly runnable as some 
features are not supported and the output is not predicted correctly (although there is an output).

Aim of the application:

The aim of the application is to predict, whether you can make it home on time for Christmas (25.12.) 
or not. Therefore, the application predicts the chance that your flight will on time. 
The data is based on real flight data from the year 2015. To make the application run smoothly, 
we decided to focus on the largest 10 airports in the united states 
(source: https://www.tripsavvy.com/busiest-airports-in-the-usa-3301020). Furthermore, we already 
proceeded to further reduce the data set before importing it into python by just keeping the data for 
the 25th of December. This was a necessary step to reduce data volume in order to improve file handling 
and upload the file on GitHub. 
 
How the code works: 

Data cleaning:
	
	In a first step, all the libraries used in the text will be loaded as well as the underlying 
	data as a CSV-File. In a first step, we deleted all the columns which were not needed. 

		
		ASSUMPTION: In airline business, it often time happens that a flight has a delay of 
			    several minutes. We therefore set a limit of 10 minutes, which means that 
			    if a flight is delayed for 10 or more minutes, it will count as "delayed".
			    Furthermore, the data contains empty values for the delay if the flight was 
			    cancelled. To take those cancelled flights into account, we assigned them 
			    during the the cleaning procedure the value of 10 to count them as delayed 
			    (>= 10).

	As our Machine Learning Model only predicts "delayed" or "on time", we assigned boolean values 
	to the delay times (>= 10 min --> "delayed", <10 min --> "on time")
	
	We then further reduced the dataset by only selecting 25.12. as input date. After getting rid
	of the now redundant columns, we further reduced the data to the biggest 10 airports of the USA.
	To increase the accuracy of the model, we quantitate the departure hours to only have 24 different 
	values (0-23) as departure time as this creates the opportunity to cluster the departure times. 
	In a last step, we use pandas get_dummies function and assign a dummy variable (0 or 1) to each
	airport in order to have only one value for the destination and arrival airport. This step is crucial to
	assign the values to the machine learning model to predict the outcome as the calculation is based on a binary
	classification.

Build the Machine Learning Model:

	The Machine Learning Model used by this application is the RandomForestClassifier using the sklearn
	library. In Machine Learning, underlying data sets are usually split into training- and test-dataset
	with a classic split-ratio of 80%/20%. The logic behind this split is that the prediction model is first
	trained with 80% of the data which is randomly chosen by the machine learning model. The included random
	state describes a potential data-split selection and differs from state to state chosen. The ratio chosen 
	by us is 70%/30%, as this split improved the accuracy of our model. 

Accuracy Measurements:

	To measure the accuracy of the model, we make use of different approaches. One Method used by us is the 
	ROC AUC Score. The ROC (receiver operating characteristics) curve describes the relationship of true and 
	false answers given by the model. The AUC score therefore describes the area below the ROC-Curve, where a
	higher score means that the prediction of the model is higher. The measure taken is the integral of the 
	area below the ROC-curve. 

	Further, the confusion matrix is used to create an array showing the results of the test and train split, 
	differentiating between wrong and false answers created by the model. In a last step, score measurements 
	such as precision_- and recall_score are used to measure the exact precision of the model.

Visualise model output:

	The ROC Curve is then plotted using an inbuilt sklearn feature. The plotted graph shows two different 
	curves. The ROC Curve itself shows the value as described in the section above. The curve is above the 
	average curve. The average curve shows the perfect relation of the score in case the model predicts every 
	second case correctly.

Prediction model: 
	
	We created a function we called predict_delay, which uses an input function to filter dummy variables 
	according to the user input. Furthermore, we improved the input mechanism by adding a loop to ensure 
	that the entered time format is correct, so the machine can predict the chance of the delay correctly.

Bot conversation:

	The application includes a bot, which is having a conversation with the user while guiding him through the 
	questions. We therefore defined various lists including the responses which the user expects the bot to give, 
	as well as a set of predefined inputs the user can actually give to the bot. All these functions include 
	conditions and loops to ensure the user is guided through all the questions correctly and gets the chance to 
	re-enter an input in order to get the desired result. Some of the variables in the functions are defined as 
	global variables, as they are used also outside of the original function. During the conversation, you will 
	be asked all the needed information to predict wether with a percentage of certainty that you're flight is 
	on time. 


Plot on-time-arrival for user input: 

	The derived output out of the model will first just be displayed as probability. To improve the user 
	experience and 	increase the benefits, the complete result of all connections leaving on that day will 
	be displayed. We therefore used the pyplot function of the matplotlib library to plot the results 
	accordingly. The plot shows all the predicted percentages of arriving on time over the whole day and 
	gives the user the chance to change the departure time in case he still has the chance, so the user 
	still arrives on time at christmas.
	
Image plot: 
	
	In order to visualize the effect of the delay even more, we use the matplotlib library again to this 
	time plot a picture of a santa. In case the predicted chance of an on time arrival is over 50%, a happy 
	santa will be plotted within the jupyter terminal using the if function. Should it be lower than 50%, a 
	late santa will be displayed. 




Authors: 
Pascale Tobler 
Michel Voutat
Calvin Limat