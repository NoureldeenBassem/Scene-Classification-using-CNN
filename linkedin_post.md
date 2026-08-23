# LinkedIn post

I taught a model to look at a photo and say what kind of place it is. 🏞️

**The problem I set out to solve:** picture a stock photography platform. Photographers upload
landscape and travel photos, and buyers search that library by scene type, they want a forest, a
mountain, a street. That search only works if every photo carries the right tag, and right now a human
opens and tags every single upload by hand. The backlog of untagged photos grows faster than the
review team can clear it. So photographers wait to get their work live, and buyers search a library
that is missing a chunk of its stock.

**What I built:** a model that looks at an uploaded photo and sorts it into one of six scene
categories on its own, buildings, forest, glacier, mountain, sea or street. It gets 93% of them right
on 3,000 photos it had never seen before, and I put it online as a small web app where you can drop in
your own photo and watch it decide.

**The part I found interesting:** the mistakes are not random at all. Out of 210 wrong answers, 114 of
them are the model confusing a glacier with a mountain. More than half of every mistake it makes,
sitting on one single pair.

And honestly, it is a fair mistake. A glacier photo is a snowy slope under a sky, and so is a mountain
photo. What actually separates them is the texture of the ice, and that is the first detail to
disappear when a photo is shrunk down to a size the model can read.

Then I opened the ten mistakes it was most confident about, and six of them were photos labelled
"glacier" with no ice visible anywhere, just green valleys and treelines. The model said mountain. I
would have said mountain. The label was simply wrong. Some of what looked like model error was the
dataset disagreeing with itself, and that is the part you cannot get from a metric.

**So I did not chase a perfect score.** I made the model report how confident it is instead. If it
only tags the photos it is sure about, it handles 92% of the uploads at 96% accuracy and passes the
rest on. That is the whole point: the backlog clears automatically, photographers get live faster, and
the review team spends its time only on the photos the model is genuinely unsure about, which are the
ones a human was actually needed for.

Knowing where a model is weak turned out to be worth more than squeezing out another point of accuracy.

**Under the hood:** transfer learning on MobileNetV2 in TensorFlow/Keras, trained in two stages
(classifier head first, then fine-tuning the last block, which took it from 91.3% to 93.0%), evaluated
on a held out test set with per class metrics and a confusion matrix, and deployed with Streamlit.

Code 👉 https://github.com/NoureldeenBassem/Scene-Classification-using-CNN
Try it 👉 https://scene-classification-using-cnn-2f5pzdhy2it8yqsbfdwchl.streamlit.app/

Feedback is very welcome, especially if you have worked with classes that overlap this much.

#MachineLearning #DeepLearning #ComputerVision #TensorFlow #Keras #Streamlit #DataScience #CNN
