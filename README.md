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
<p float="left">
  <img src="https://user-images.githubusercontent.com/47933584/116708036-51119b00-a99d-11eb-9505-d6b131b4974a.png" width="300" />
  <img src="https://user-images.githubusercontent.com/47933584/116709900-258fb000-a99f-11eb-81e2-b18fcf05b8a1.png" width="300" /> 
  <img src="https://user-images.githubusercontent.com/47933584/116709910-288aa080-a99f-11eb-8eb4-5d968a841935.png" width="300" />
</p>

We were able to reproduce figures from the article with some success with different configurations for the datasets MNIST, SVHN and CelebA. We obtained the same result as the article for MNIST, but had great difficulties in training a decent generator on the datasets SVHN and CelebA. We ran into some major reproductibility issues: The GitHub from OpenAI has code that we were not able to execute, even with various dockerhub tensorflow versions and prettytensor versions. It was extremely hard to diagnose our failures and improve with no working example from the original configuration. We believe it has to do with our mutual information loss being improperly calculated, but still we achieve the theoretical maximum of I = 2.3 for C1 on MNIST, making it hard to believe we used the wrong formula. For continuous codes, we were unable to figure out the formula for mutual information maximization. We simply used MSE as an analogy that being able to reproduce the input means somehow to gan stored the information in the image.

# Experiments & help running the notebooks
Our best results were obtained using our own implementation which are in the Jupyter Notebooks InfoGAN_CELEBA, InfoGAN_SVHN and InfoGAN_MNIST. For each notebook, the first cell has all the includes you will need, and the second cell defines the class InfoGAN() which includes all the function needed to build ,train and monitor the InfoGAN. We use Tensorflow Datasets to load automatically the MNIST and SVHN datasets, but the package does not work for CELEBA. You will need to manually download the file *img_align_celeba.zip* from this url: https://drive.google.com/drive/folders/0B7EVK8r0v71pTUZsaXdaSnZBZzg. 
The CelebA notebook expects the file to be in the same directory when loading the dataset. The final cell contains code to do some latent code manipulation. You should be able to see an example of an image that is present in our report. If this does not appear (depending on the .ipynb viewer you are using, some don't show the saved output), refer to the github page of that file and it should display properly.
