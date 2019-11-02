# Autonomous Driving

__1. Your 100,000 labeled images are taken using the front-facing camera of your car. This is also the distribution of data you care most about doing well on. You think you might be able to get a much larger dataset off the internet, that could be helpful for training even if the distribution of internet data is not the same.__

__You are just getting started on this project. What is the first thing you do? Assume each of the steps below would take about an equal amount of time (a few days).__

- Spend a few days training a basic model and see what mistakes it makes

> (i) _Start with the basic model and try to undertand the problem in hand with the mistakes your simple model is making._
>
> (ii) _As discussed in lecture, applied ML is a highly iterative process. If you train a basic model and carry out error analysis (see what mistakes it makes) it will help point you in more promising directions._ 

__2. Your goal is to detect road signs (stop sign, pedestrian crossing sign, construction ahead sign) and traffic signals (red and green lights) in images. The goal is to recognize which of these objects appear in each image. You plan to use a deep neural network with ReLU units in the hidden layers.__

__For the output layer, a softmax activation would be a good choice for the output layer because this is a multi-task learning problem. True/False?__

- False 

> (i) _We are asking our neural network to perform many tasks at once, so we need a binary classifier for each of those tasks._
> 
> (ii) _Softmax would be a good choice if one and only one of the possibilities (stop sign, speed bump, pedestrian crossing, green light and red light) was present in each image._

__3. You are carrying out error analysis and counting up what errors the algorithm makes. Which of these datasets do you think you should manually go through and carefully examine, one image at a time?__

- 500 images on which the algorithm made mistakes

> (i) _We need to manually analyze the mistakes our model is making, refer to the lecture for more details._
> 
> (ii) _Focus on images that the algorithm got wrong. Also, 500 is enough to give you a good initial sense of the error statistics. There’s probably no need to look at 10,000, which will take a long time._

__4. After working on the data for several weeks, your team ends up with the following data:__

> - 100,000 labeled images taken using the front-facing camera of your car.
> - 900,000 labeled images of roads downloaded from the internet.
> - Each image’s labels precisely indicate the presence of any specific road signs and traffic signals or combinations of them. For example, $\bm{y^{(i)} = \begin{bmatrix} 1 \\ 0 \\ 0 \\ 1 \\ 0 \end{bmatrix}}$ means the image contains a stop sign and a red traffic light.

__Because this is a multi-task learning problem, you need to have all your $\bm{y^{(i)}}$ vectors fully labeled. If one example is equal to
$\bm{\begin{bmatrix} 0 \\ ? \\ 1 \\ 1 \\ ? \end{bmatrix}}$ then the learning algorithm will not be able to use that example. True/False?__

- False

> (i) _The learning algorithm only analyzes the elements of the vectors which are labelled since it is calculating the loss for each element separately (and then adding them up)._
> 
> (ii) _As seen in the lecture on multi-task learning, you can compute the cost such that it is not influenced by the fact that some entries haven’t been labeled._

__5. The distribution of data you care about contains images from your car’s front-facing camera; which comes from a different distribution than the images you were able to find and download off the internet. How should you split the dataset into train/dev/test sets?__

- Choose the training set to be the 900,000 images from the internet along with 80,000 images from your car's front-facing camera. The 20,000 remaining images will be split equally in dev and test sets.

(_Yes. As seen in lecture, it is important that your dev and test set have the closest possible distribution to “real”-data. It is also important for the training set to contain enough “real”-data to avoid having a data-mismatch problem_)

__6. Assume you’ve finally chosen the following split between of the data:__

| Dataset: | Contains: | Error of the algorithm: |
| :---: | :---: | :---: |
| __Training__ | __940,000 images randomly picked from (900,000 internet images + 60,000 car’s front-facing camera images)__ | __8.8%__ | 
| __Training-Dev__ | __20,000 images randomly picked from (900,000 internet images + 60,000 car’s front-facing camera images)__ | __9.1%__ |
| __Dev__ | __20,000 images from your car’s front-facing camera__ | __14.3%__ |
| __Test__ | __20,000 images from the car’s front-facing camera__ | __14.8%__ |

__You also know that human-level error on the road sign and traffic signals classification task is around 0.5%. Which of the following are True? (Check all that apply).__

- You have a large data-mismatch problem because your model does a lot better on the training-dev set than on the dev set
- You have a large avoidable-bias problem because your training error is quite a bit higher than the human-level error 

__7. Based on table from the previous question, a friend thinks that the training data distribution is much easier than the dev/test distribution. What do you think?__

- There's insufficient information to tell.

> (i) _We don't know how the errors on dev/test sets look like if we had trained the model on them._
>
> (ii) _The algorithm does better on the distribution of data it trained on. But you don’t know if it’s because it trained on that no distribution or if it really is easier. To get a better sense, measure human-level error separately on both distributions._

__8. You decide to focus on the dev set and check by hand what are the errors due to. Here is a table summarizing your discoveries:__

| Overall dev set error	| 15.3% |
| :---: | :---: |
| __Errors due to incorrectly labeled data__ | __4.1%__ |
| __Errors due to foggy pictures__ | __8.0%__ |
| __Errors due to rain drops stuck on your car’s front-facing camera__ | __2.2%__ |
| __Errors due to other causes__ | __1.0%__ |

__The results from this analysis implies that the team’s highest priority should be to bring more foggy pictures into the training set so as to address the 8.0% of errors in that category. True/False?__

- False because it depends on how easy it is to add foggy data. If foggy data is very hard and costly to collect, it might not be worth the team's effort.

(_Correct feedback:  You should consider the tradeoff between the data accessibility and potential improvement of your model trained on this additional data._)

__9. You can buy a specially designed windshield wiper that help wipe off some of the raindrops on the front-facing camera. Based on the table from the previous question, which of the following statements do you agree with?__

- 2.2% would be a reasonable estimate of the maximum amount this windshield wiper could improve performance.

> (i) _Yes. You will probably not improve performance by more than 2.2% by solving the raindrops problem. If your dataset was infinitely big, 2.2% would be a perfect estimate of the improvement you can achieve by purchasing a specially designed windshield wiper that removes the raindrops._
>
> (ii) _In other words, you will not be able to boost the performance by more than 2.2%. In fact, 2.2% performance boost will happen only when we have infintely big data set (not a small representative of it)._

__10. You decide to use data augmentation to address foggy images. You find 1,000 pictures of fog off the internet, and “add” them to clean images to synthesize foggy days, like this:__

__Which of the following statements do you agree with?__

- So long as the synthesized fog looks realistic to the human eye, you can be confident that the synthesized data is accurately capturing the distribution of the real foggy images (or a subset of it), since human vision is very accurate for the problem you're solving.

(_Yes. If the synthesized images look realistic, then the model will just see them as if you had added useful data to identify road signs and traffic signals in a foggy weather. It will very likely help._)

__11. After working further on the problem, you’ve decided to correct the incorrectly labeled data on the dev set. Which of these statements do you agree with? (Check all that apply).__

- You should also correct the incorrectly labelled data from the test set, so that the dev and test sets continue to come from the same distribution

(_Yes because you want to make sure that your dev and test data come from the same distribution for your algorithm to make your team’s iterative development process is efficient._)

- You do not necessarily need to fix the incorrectly labeled data in the training set, because it's okay for the training set distribution to differ from the dev and the test sets. Note that it is important that the dev and test set have the same distribution.

(_True, deep learning algorithms are quite robust to having slightly different train and dev distributions._)

__12. So far your algorithm only recognizes red and green traffic lights. One of your colleagues in the startup is starting to work on recognizing a yellow traffic light. (Some countries call it an orange light rather than a yellow light; we’ll use the US convention of calling it yellow.) Images containing yellow lights are quite rare, and she doesn’t have enough data to build a good model. She hopes you can help her out using transfer learning.__

__What do you tell your colleague?__

- She should try using weights pre-trained on your dataset, and fine-tuning further with the yellow-light dataset.

> (i) _Yes. You have trained your model on a huge dataset, and she has a small dataset. Although your labels are different, the parameters of your model have been trained to recognize many characteristics of road and traffic images which will be useful for her problem. This is a perfect case for transfer learning, she can start with a model with the same architecture as yours, change what is after the last hidden layer and initialize it with your trained parameters._
>
> (ii) _Both of our models are quite similar since the problem statements are aimed towards the same task, so transfer learning can be a good solution._

__13. Another colleague wants to use microphones placed outside the car to better hear if there’re other vehicles around you. For example, if there is a police vehicle behind you, you would be able to hear their siren. However, they don’t have much to train this audio system. How can you help?__

- Neither transfer learning nor multi-task learning seems promising.

> (i) _Yes. The problem he is trying to solve is quite different from yours. The different dataset structures make it probably impossible to use transfer learning or multi-task learning._
>
> (ii) _In this case, the problem statements are aiming towards tasks which are quite different (vision vs audio)._

__14. To recognize red and green lights, you have been using this approach:__

__(A) Input an image (x) to a neural network and have it directly learn a mapping to make a prediction as to whether there’s a red light and/or green light (y).__

__A teammate proposes a different, two-step approach:__

__(B) In this two-step approach, you would first (i) detect the traffic light in the image (if any), then (ii) determine the color of the illuminated lamp in the traffic light.__

__Between these two, Approach B is more of an end-to-end approach because it has distinct steps for the input end and the output end. True/False?__

- False

(_Approach A is more of an end-to-end learning approach as it maps directly the input (x) to the output (y) whereas approach B is multi-step approach._)

__15. Approach A (in the question above) tends to be more promising than approach B if you have a ________ (fill in the blank).__

- Large training set

(_End-to-end learning approach is viable if we have a lot of data to train on though it has been observed that it works better in practice._)