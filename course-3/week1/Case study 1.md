# Bird recognition in the city of Peacetopia 

__1. Problem Statement:__
    
__The City Council tells you that they want an algorithm that__

> - Has high accuracy
>
> - Runs quickly and takes only a short time to classify a new image.
> 
> - Can fit in a small amount of memory, so that it can run in a small processor that the city will attach to many different security cameras.

__Having three evaluation metrics makes it harder for you to quickly choose between two different algorithms, and will slow down the speed with which your team can iterate. True/False?__

- True

(_Recalling from the lecture that machine learning is a very iterative process (experimentation with different hyperparameters and testing) so we always prefer to have a single metric for our model performance_)

__2. After further discussions, the city narrows down its criteria to:__

> - "We need an algorithm that can let us know a bird is flying over Peacetopia as accurately as possible."
>
> - "We want the trained model to take no more than 10sec to classify a new image.”
>
> - “We want the model to fit in 10MB of memory.”

__Which of the models would you choose?__

- | Test Accuracy | Runtime | Memory Size |
  | :---: | :---: | :---: |
  | 98 % | 9 sec | 9 MB |

__3. Based on the city’s requests, which of the following would you say is true?__

- Accuracy is an optimizing metric; running time and memory size are satisficing metrics.

(_Maximizing accuracy while subject to the conditions on the runtime and memory size._)

__4. Before implementing your algorithm, you need to split your data into train/dev/test sets. Which of these do you think is the best choice?__

- | Train | Dev | Test |
  | :---: | :---: | :---: |
  | 9,500,000 | 250,000 | 250,000 |

__5. Is the following statement true or false?__

__"You should not add the citizens' data to the training set, because if the training distribution is different from the dev and test sets, then this will not allow the model to perform well on the test set."__

- False 

(_Training data can have a different distribution than the dev/test set._)

__6. One member of the City Council knows a little about machine learning, and thinks you should add the 1,000,000 citizens’ data images to the test set. You object because:__

- This would cause the dev and test set distributions to become different. This is a bad idea because you are not aiming where you want to hit.
- The test set no longer reflects the distribution of data (security cameras) you most care about.

__7. You train a system, and its errors are as follows (error = 100% - Accuracy):__
| Training set error | 4.0% |
| :---: | :---: | 
| __Dev set error__ | __4.5%__ |

__This suggests that one good avenue for improving performance is to train a bigger network so as to drive down the 4.0% training error. Do you agree?__

- No, because there is insufficient information to tell.

(_We don't know the human level performance, so we can't say anything about the avoidable bias._)

__8. You ask a few people to label the dataset so as to find out what is human-level performance. You find the following levels of accuracy:__

| Bird watching expert #1 | 0.3% error |
| :---: | :---: |
| __Bird watching expert #2__ | __0.5% error__ |
| __Normal person #1 (not a bird watching expert)__ | __1.0% error__ |
| __Normal person #2 (not a bird watching expert)__ | __1.2% error__ |

__If your goal is to have “human-level performance” be a proxy (or estimate) for Bayes error, how would you define “human-level performance”?__

- 0.3% (accuracy of expert #1)

(_This is the lowest error out of four accuracy levels, hence this should be a correct representative of the Bayes error._)

__9. Which of the following statements do you agree with?__

- A learning algorithm's performance can be better than human-level performance but it can never be better than Bayes error.

(_Bayes error is the smallest value of error possible for a learning task, human-level performance is often taken as a proxy for Bayes error but it is usually a bit larger than Bayes error._)

__10. You find that a team of ornithologists debating and discussing an image gets an even better 0.1% performance, so you define that as “human-level performance.” After working further on your algorithm, you end up with the following:__

| Human-level performance |	0.1% |
| :---: | :---: |
| __Training set error__ | __2.0%__ |
| __Dev set error__ | __2.1%__ |

__Based on the evidence you have, which two of the following four options seem the most promising to try? (Check two options.)__

- Try decreasing regularization
- Train a bigger model to do better on the training set

(_It is clearly a problem of avoidable bias: the difference between training set error and human-level performance is bigger than the difference between training set error and dev set error, so need to decrease the bias._)

__11. You also evaluate your model on the test set, and find the following:__

| Human-level performance |	0.1% |
| :---: | :---: |
| __Training set error__ | __2.0%__ |
| __Dev set error__ | __2.1%__ |
| __Test set error__ | __7.0%__ |

__What does this mean? (Check the two best options.)__

- You have overfit to the dev set
- You should try to get a bigger dev set

(_Since dev set and test set are from same distribution, the difference in error between dev set and test set suggests we have overfit the dev set, so need to get a bigger dev set._)

__12. After working on this project for a year, you finally achieve:__

| Human-level performance |	0.10% |
| :---: | :---: |
| __Training set error__ | __0.05%__ |
| __Dev set error__ | __0.05%__ |

__What can you conclude? (Check all that apply.)__

- It is now harder to measure the avoidable bias, thus progress will be slower going forward
- If the test set is big enough for the 0.05% error estimate to be accurate, this implies the Bayes error is <= 0.05

(_The dev set error has surpassed the human-level performance, this means in this case, human-level performance is no longer a correct representative of the Bayes error._)

__13. It turns out Peacetopia has hired one of your competitors to build a system as well. Your system and your competitor both deliver systems with about the same running time and memory size. However, your system has higher accuracy! However, when Peacetopia tries out your and your competitor’s systems, they conclude they actually like your competitor’s system better, because even though you have higher overall accuracy, you have more false negatives (failing to raise an alarm when a bird is in the air). What should you do?__

- Rethink the appropriate metric for this task, and ask your team to tune to the new metric.

(_Accuracy is no longer the appropriate metric, our model seems to have low recall._ )

__14. You’ve handily beaten your competitor, and your system is now deployed in Peacetopia and is protecting the citizens from birds! But over the last few months, a new species of bird has been slowly migrating into the area, so the performance of your system slowly degrades because your data is being tested on a new type of data.__

__You have only 1,000 images of the new species of bird. The city expects a better system from you within the next 3 months. Which of these should you do first?__

- Use the data you have to define a new evaluation metric (using a new dev/test set) taking into account the new species, and use that to drive the further progress for your team.

(_Refer to the lectures for how to split this newly acquired data into train/dev/test sets and then redefine your evaluation metric._)

__15. The City Council thinks that having more Cats in the city would help scare off birds. They are so happy with your work on the Bird detector that they also hire you to build a Cat detector. (Wow Cat detectors are just incredibly useful aren’t they.) Because of years of working on Cat detectors, you have such a huge dataset of 100,000,000 cat images that training on this data takes about two weeks. Which of the statements do you agree with? (Check all that agree.)__

- Needing two weeks to train will limit the speed at which you can iterate
- Buying faster computers could speed up your teams' iteration speed and thus your team's productivity
- If 100,000,000 examples is enough to build a good enough Cat detector,you might be better of training with just 10,000,000 examples to gain a ≈10x improvement in how quickly you can run experiments, even if each model performs a bit worse because it’s trained on less data.