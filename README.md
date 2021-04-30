# 8225-project
Final project for INF8225 on InfoGAN at Polytechnique Montreal, Winter 2021 semester

# Authors
- Bruno Curzi-Laliberté
- Thomas Rochefort-Beaudoin
- Antoine Martin
- Lucas Aubrun

# Our goal
We set out to reproduce results published by the OpenAI team in their paper:

[InfoGAN: Interpretable Representation Learning by Information Maximizing Generative Adversarial Nets by Xi Chen, Yan Duan, Rein Houthooft, John Schulman, Ilya Sutskever, Pieter Abbeel.](https://arxiv.org/abs/1606.03657)

[OpenAI InfoGAN GitHub](https://github.com/openai/InfoGAN)

# What is an InfoGAN?
InfoGAN consists in a GAN implementation capable of unsupervised disentangled representation learning. When tasked with reproducing images just like a GAN, but also tasked with reproducing its non random part of the latent codes, which can be continuous or categorical, an InfoGAN associates features of the dataset to those codes. This entire process is done by only using the input image, no labeled data, making it a complex but appealing task. If done properly, the end result is a GAN which you can guide to output images that match your criteria based on latent code tuning. Then tuning the random noise part will yield various images of the same type.

# Our results
Solarized dark             |  Solarized Ocean
:-------------------------:|:-------------------------:
<img src="https://user-images.githubusercontent.com/47933584/116708036-51119b00-a99d-11eb-9505-d6b131b4974a.png" width="200" height="200">
  | <img src="https://user-images.githubusercontent.com/47933584/116708036-51119b00-a99d-11eb-9505-d6b131b4974a.png" width="200" height="200">


We were able to reproduce figures from the article with some success with different configurations for the datasets MNIST, SVHN and CELEBA. The GitHub from OpenAI has code that we were not able to execute, even with various dockerhub tensorflow versions and prettytensor versions. It was extremely hard to diagnose our failures and improve with no working example from the original configuration. We believe it has to do with our mutual information loss being improperly calculated, but still we achieve the theoretical maximum of I = 2.3 for C1 on MNIST, making it hard to believe we used the wrong formula. For continuous codes, we were unable to figure out the formula for mutual information maximization. We simply used MSE as an analogy that being able to reproduce the input means somehow to gan stored the information in the image.

# Experiments & help running the notebooks
Our best results were obtained using our own implementation which are in the Jupyter Notebooks InfoGAN_CELEBA, InfoGAN_SVHN and InfoGAN_MNIST. For each notebook, the first cell has all the includes you will need, and the second cell defines the class InfoGAN() which includes all the function needed to build ,train and monitor the InfoGAN. The final cell contains code to do some latent code manipulation. You should be able to see an example of an image that is present in our report. If this does not appear (depending on the .ipynb viewer you are using, some don't show the saved output), refer to the github page of that file and it should display properly.
