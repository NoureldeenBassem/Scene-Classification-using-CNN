# LinkedIn post

I taught a model to look at a photo and say what kind of place it is. 🏞️

**The problem in plain words:** imagine a stock photo website. Photographers upload thousands of
landscape photos, and someone on the team has to open every single one and tag it: is this a forest?
a beach? a street? The uploads arrive faster than the team can tag them, so the backlog just grows.

**What I built:** a model that sorts a photo into one of six categories, buildings, forest, glacier,
mountain, sea or street. It gets 93% of them right on 3,000 photos it had never seen before, and I put
it online as a small web app where you can drop in your own photo and watch it decide.

**The part I found interesting:** the mistakes are not random at all. Out of 210 wrong answers, 114 of
them are the model confusing a glacier with a mountain. That is more than half of every mistake it
makes, sitting on one single pair.

And honestly, it is a fair mistake. A glacier photo is a snowy slope under a sky, and so is a mountain
photo. What actually separates them is the texture of the ice, and that is the first detail to
disappear when a photo is shrunk down to a size the model can read.

Then I opened the ten mistakes it was most confident about, and six of them were photos labelled
"glacier" with no ice visible anywhere, just green valleys and treelines. The model said mountain. I
would have said mountain. The label was simply wrong.

That was the most useful hour of the whole project, and it is the part you cannot get from a metric.
Some of what looked like model error was the dataset disagreeing with itself.

So instead of chasing a perfect score, I made the model say how confident it is. If I only let it tag
the photos it is sure about, it handles 92% of the uploads at 96% accuracy and passes the rest to a
human. The backlog clears, and the team only opens the genuinely hard photos.

That felt like the real lesson here: knowing where a model is weak is worth more than squeezing out
another point of accuracy.

**Under the hood:** transfer learning on MobileNetV2 in TensorFlow/Keras, trained in two stages
(classifier head first, then fine-tuning the last block, which took it from 91.3% to 93.0%), evaluated
on a held out test set with per class metrics and a confusion matrix, and deployed with Streamlit.

Code 👉 https://github.com/NoureldeenBassem/Scene-Classification-using-CNN
Try it 👉 https://scene-classification-using-cnn-2f5pzdhy2it8yqsbfdwchl.streamlit.app/

Feedback is very welcome, especially if you have worked with classes that overlap this much.

#MachineLearning #DeepLearning #ComputerVision #TensorFlow #Keras #Streamlit #DataScience #CNN
