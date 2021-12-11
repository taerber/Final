# Final Project:
Stress Detector: Emergent Model



Tara Erberich
Department of Psychology, University of Southern California
Psyc 450: Neural Network Models Of Social and Cognitive Processes
Professor Stephen Read
December 10, 2021







Abstract
This paper will explore the detection of stress through the workings of a simple feedforward network to replicate similar studies done using CNN models and sensor data. The importance of this model is to examine if emotional question data is a viable option for future stress detection research. The model will be given two different sets of answer data from a question survey taken by 15 subjects under 5 conditions: base, stress, meditation 1, meditation 2, and fun. These inputs are fed into a 1x24 input and unilaterally connected to a 4x6 hidden layer and then bilaterally connected to the 1x3 output. The input layer represents the 24 answers and the 1x3 output represents the 3 detections: neutral, stress, and fun. The model is also tested with similar survey data but the input layer is transformed to a 1x6 in accordance to the number of questions answered. The results show that with learning both datasets are able to correctly classify the output about 80% of the time, but when the learning is removed the model only classifyis the data correctly 50% of the time. This suggests a more advanced model with error-driven learning could better classify the output results and would allow for reliable stress detection with emotional written responses.   

Background
The inspiration of this model came from a study called “Stress detection using deep neural networks” which explores how stress could be detectable through physiological readings (Li, R., & Liu, Z. , 2020). Within this paper the model will focus on emotional answers to survey questions to see how viable this type of data is for stress detection. This type of detection is extremely important because chronic stress leads to many other health issues. An APA reports that around 80% of US adults have serious stress issues (APA: US Adults, 2020). Now more than ever, after experiencing a worldwide pandemic, the need for effective, simple, and reliable methods for stress detection to help future medical research and technology developments has become critical. Stress is caused when fear or anxiety is sensed and the amygdala is activated which in turn activates the hypothalamic-pituitary-adrenocortical (HPA) axis (Cadwell, 2018). The system then overworks and increases cortisol hormones within the body which then increases blood flow and heart rate. Stress can lead to serious health risks like asthma attacks, problems with heart and blood vessels, off-balanced HPA axis, among other serious health conditions (APA: Stress effects on the body, 2018). These hormonal changes should not occur on a daily basis, which is why this stress detection model is proposed. 
	The network was adapted from the original study so it could be modeled correctly in Emergent. The original study used a 1D CNN and a multilayer perceptron neural network, but this could not be modeled in Emergent. The study also used sensor data from wrist and chest reading within their models, but in this model the questionnaire data is tested. Instead, the model below is simplified to 3 layers: input, hidden, and output, because of the lack of volume in the data set and this is a simple classification method. This model is supposed to show that detection from emotional responses could be used for future detection. This is to promote larger stress studies because of how easy it is to conduct question surveys and this will allow for more research behind stress in larger quantities.  

Methods
Data:
The data was obtained from a study that tested 15 participants under 5 different conditions. This data set is called WESAD: Multimodal Dataset for Wearable Stress and Affect Detection, and contains results of individuals chest and wrist monitors and questionnaire results. For this model, only the questionnaire data will be used and all other data will be ignored. The PANA survey data and STAI survey data will both be tested within the model. This will compare how different lengths of answer data will affect the model. Each subject had to fill out questions under 5 different conditions: Base, Stress, Meditation 1, Fun, Meditation 2 and all responses were answers based on a scale. Each row in the WESDA.tsv file and WESD2.tsv file are the answers of an individual under a specific condition. To normalize the data, so the inputs would be between 0-1, the formula (x-min)/(max-min) was applied to each different question. The low volume of data may affect the results of the model and therefore limit the research.
Structure:
The structure of this stress detector simulator is a 3 layer network with an input layer, a hidden layer, and an output layer. For the PANAs questions, the input layer is a 1x24, since each subject answered 24 questions, and the output layer is a 1x3. For the STAI data, the input layer was modified to a 1x6 layer since only 6 questions were answered for this data set. The output is the same 1x3 layer since subjects were tested under the same 5 conditions. Each unit within the output layer represents stressed, neutral, or fun and each input has an output with a 1 in a specific unit spot. From the data, the base, meditation 1, and meditation 2 conditions were labeled as base for the output, the stress condition was labeled as stress output, and the fun condition was labeled as fun output.

Figure 1
Note: Input and Output Formatting

	Above in figure 1, it can be seen that the base output is the activated middle unit, stress is the activated left unit, and fun is the activated right unit. The output will be set at Target for training and the connection layers are unilaterally feedforward between the input and hidden layer. The hidden and output layers are bi-directionally connected and both connections are full projection. While the model is set at Target, both datasets will be tested at the models base function and then further altered depending on the results. Once the training phase is over, the output will be set to compare to shut off error-driven learning and both data files will be tested again to see how well the model performs without any learning. 

Results
PANA Data:
The first run of this model was to see how well the base structure performed. This produced a good sense of what may be harder for the model to distinguish. Below in Figure 2 is an example of a step trial for the meditation 2 condition and it can be observed which inputs activate more. These inputs are more active because these are the inputs that were scored higher on the survey scale and were normalized closer to 1. The output of this trial is the neutral condition, which means the training classified it correctly.

Figure 2
Note: Step Trial of base model

	The statistics of the trail run are presented below in Figure 3 and these results show how the model performs in one run. The SSE and PctErr results are both around 50% for many of the epochs, showing the model is capable of learning the inputs but there is room for improvement. Figure 4 further outlines how the model is learning over epochs as the PctCorr, purple line, is slowly increasing but still dips as new subject data is introduced. 

Figure 3
Note: Step Epoch Training results

Figure 4
Note: Step Run TstEpcPlot Graph

Now with the base results the model can be altered to find improvement in the PctCor percentage. The first altercation was to see if the model could perform better if the paramSet was set to the Default inhibition and then training and testing the model again. Below in Figure 5 are the results of this model change and it is seen that PctCorr has raised to around 80% correct. This is a substantial improvement from the first performance of the model.  

Figure 5
Note: Step Run TstEpcPlot Graph

Within figure 6, it is also seen that the model is now predicating correctly at about 70-80% which is about a 30% increase from the model with base parameters set. Since the model performs relatively well the output layer will be set to compare to see how the model does without learning by changing target to compare in the code. 

Figure 6
Note: Step Run Results

Once the model was switched to compare, the default model was run and so was the model with parameters set to default inhibition. These tests offered opposite results as before, since the default model was able to perform better without learning. Below in figure 7 and figure 8, are the results of the training epoch plots. The default model in figure 7 correctly identifies the output 50% of the time and the model with default inhibition in figure 8 identifies the output correctly 20% of the time. This is a change from how the model performed under target. Unlike before, the default inhibition did not help the model and that is most likely because its inhibition was not low enough, which is needed for a smaller data set. 

Figure 7

Figure 8

By switching to compare in the code the model struggles more with identifying stress because the network labels stress as fun in the output. This may be a result of similar input patterns coming from stress and fun data. This indicates that the fun condition may need to be removed for more accurate readings or a model with better error detection. Within figure 9, it can be seen how many of the inputs are activated for stress because subjects answered with a higher scale value for most responses. This creates confusion in the output layer leading to labeling the stress condition as fun because both stress and fun have many active inputs. Due to these two conditions causing the model confusion, more data may need to be collected, the fun condition may need to be removed, or learning based models need to be produced. 

Figure 9

STAI Data: 
Similar tests and changes were applied to the second dataset of STAI questions to compare how data differences may affect model performance. Figure 10 shows how the altered model has an input layer of 1x6 to represent each answer. The results within figure 11 show how the model performed under testing with target set and no default inhibition set, this results in better statistics than with the PANA data under these testing conditions. The model gets to around 90% PctCor within a few trials. When the model is set to default inhibition during testing the results are worse than the base network, which is unlike the PANAs data set. This may all be attributed to the smaller amount of questions answered by subjects. Since the base model gave the best results this model was further tested with the coding being switched to compare.

Figure 10

Figure 11

Once the model was switched to compare similar results were seen as with the PANA data. The model performed significantly worse as figure 12 shows the PctCor is around 30%, which is significantly lower than the model using target. As well as, the trial in figure 10 is also incorrect as the first output unit should be activated for stress but instead the fun unit is activated. These similar results from PANA and STAI models set at compare show that the fun condition confuses the model too much without learning present in the model.   

Figure 12

Conclusion
The stress detector model was tested under various conditions and not all proved to be the best methods. The overall trend that worked seemed to be that some sort of learning must be applied to the model for best results that are above 80% correct or else the model gets confused between the fun and stress condition. Without the learning aspect, the active inputs of stress and fun are too similar as these models with output set at compare cannot remember the smaller differences between the two. This indicates the model needs some sort of error-driven learning method to potentially better the testing results between stress and fun conditions. The fun condition could be removed as well, but this is a key element as a stress detector should not be detecting fun emotions as stress. Since both fun and stress increase similar physiological and emotional aspects within the body the distinction between the two is small. The models set at target within the code performed very well at about a rate of 80-90% accuracy. This leads me to believe that further alterations to the model as suggested above will prove to create a reliable model. This could be a huge advancement for future stress detection as a new type of data can be collected, beside just the sensor reading data.  

References
American Psychological Association. (n.d.). APA: U.S. adults report highest stress level 
since early days of the COVID-19 pandemic. American Psychological Association. Retrieved December 10, 2021, from https://www.apa.org/news/press/releases/2021/02/adults-stress-pandemic. 
American Psychological Association. (n.d.). Stress effects on the body. American 
Psychological Association. Retrieved December 10, 2021, from https://www.apa.org/topics/stress/body. 
Caldwell, A. (n.d.). The neuroscience of stress. BrainFacts.org. Retrieved December 10, 
2021, from https://www.brainfacts.org/thinking-sensing-and-behaving/emotions-stress-and-anxiety/2018/the-neuroscience-of-stress-061918. 
Li, R., & Liu, Z. (2020, December 30). Stress detection using Deep Neural Networks - 
BMC Medical Informatics and Decision making. BioMed Central. Retrieved December 10, 2021, from https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/s12911-020-01299-4. 
WESAD: Multimodal dataset for Wearable stress and affect detection. Ubiquitous 
Computing. (n.d.). Retrieved December 10, 2021, from https://ubicomp.eti.uni-siegen.de/home/datasets/icmi18/. 
