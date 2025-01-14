---
title: "Lecture 9: Deep generative models"
slides: true
---
<nav class="menu">
    <ul>
        <li class="home"><a href="/">Home</a></li>
        <li class="name">Lecture 9: Deep generative models</li>
                <li><a href="#video-000">Generator networks</a></li>
                <li><a href="#video-024">Generative adversarial networks</a></li>
                <li><a href="#video-045">Autoencoders</a></li>
                <li><a href="#video-067">Variational autoencoders</a></li>
        <li class="pdf"><a href="https://mlvu.github.io/lectures/51.Deep%20Learning2.annotated.pdf">PDF</a></li>
    </ul>
</nav>

<article class="slides">


       <section class="video" id="video-000">
           <a class="slide-link" href="https://mlvu.github.io/lecture09#video-0">link here</a>
           <iframe
                src="https://www.youtube.com/embed/jAxUolSXGtg?modestbranding=1&showinfo=0&rel=0"
                title="YouTube video player"
                frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
           </iframe>

       </section>



       <section id="slide-001">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-001" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0001.svg" class="slide-image" />

            <figcaption>
            <p    >In this lecture, we’ll look at generative modeling, The business of training probability models that are too complex to give us an explicit density function over our feature space, but that do allow us to sample points. If we train them well, we get points that look like those in our dataset.<br></p><p    >These kinds of methods are often combined with neural nets to produce very complex, high-dimensional objects, for instance images.<br></p><p    ><lnbr></lnbr></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-002">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-002" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0002.png" class="slide-image" />

            <figcaption>
            <p    >Here is the example, we gave in the first lecture. A deep neural network from which we can sample highly realistic images of human faces.<br></p><p    ><br></p><p    >source: <a href="https://arxiv.org/abs/1812.04948"><strong class="blue">A Style-Based Generator Architecture for Generative Adversarial Networks</strong></a>, Karras et al.<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-003">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-003" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0003.svg" class="slide-image" />

            <figcaption>
            <p    >In the rest of the lecture, we will use the following visual shorthand. The diagram on the left represents <strong>any kind of neural network</strong>. We don’t care about the precise architecture, whether it has one or a hundred hidden layers and whether it uses fully connected layers or convolutions, we just care about the shape of the input and the output.<br></p><p    >The image on the right represents a <strong>multivariate normal distribution</strong>. Think of this as a contour line for the density function. We’ve drawn it in a 2D space, but we’ll use it as a representation for MVNs in higher dimensional spaces as well. If the MVN is nonstandard, we’ll draw it as an ellipse somewhere else in space.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-004" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-004" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0004anim0.svg" data-images="51.DeepLearning2.key-stage-0004anim0.svg,51.DeepLearning2.key-stage-0004anim1.svg" class="slide-image" />

            <figcaption>
            <p    >A plain neural network is purely <strong>deterministic</strong>. It translates an input to an output and does the same thing every time with no randomness. How do we turn this into a probability distribution?<br></p><p    >The first option is to take the output and to interpret it as the parameters of a probability distribution. We simply run the neural network for some input, let it produce some numbers as an output, and then interpret those as the parameters to a probability distribution. This distribution then defines a probability on a separate space. The network plus the probability distribution define a probability distribution <strong>conditional on the network input</strong>.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-005">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-005" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0005.svg" class="slide-image" />

            <figcaption>
            <p    >If this sounds abstract, note that it is something we've been doing already since the early lectures. For instance: to do binary classification, we defined a neural network with one sigmoid activated output node. We took that output value as the probability that the class was the positive one, but we could also say we're parametrizing a Bernoulli distribution with this value, and the Bernoulli distribution defines probabilities over the space containing the two outcomes "Class=<span class="blue">pos</span>" and "Class=<span class="orange red">neg</span>".<br></p><p    >If we do this with a multiclass problem and a softmax output, we are parametrizing a <strong>multinomial distribution</strong>.<br></p><aside    >Note that linear regression is just a special case of this with a very simple (one layer) neural net.</aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-006" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-006" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0006anim0.svg" data-images="51.DeepLearning2.key-stage-0006anim0.svg,51.DeepLearning2.key-stage-0006anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Another example is regression, either linear or with a neural network.<br></p><p    >Here we simply produce a target prediction for x. However, what we saw in the previous lecture is that if we interpret this as t<strong>he mean of a normal distribution</strong> on y, then maximizing the likelihood of this distribution is equivalent to the least squares loss function.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-007">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-007" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0007.svg" class="slide-image" />

            <figcaption>
            <p    >If we build a probability distribution  parametrized by a neural network in this way, training it is pretty straightforward. We can easily compute the log-likelihood over our whole data, which then becomes a loss function. With backpropagation and gradient descent, we can train the parameters of the neural network to maximize the likelihood of the data under the model<br></p><p    >For many distributions, this leads to loss functions that we've seen already.<br></p><p    >The loss function for a normal output distribution with a <span class="orange">mean</span><em class="orange"> </em><em>and</em> <span class="blue">variance</span>, is a modification of the squared error. We can set the<span class="blue"> variance</span> larger to reduce the impact of the squared errors, but we pay a penalty of the logarithm of <span>sigma</span>. If we know we are going to get the output value for instance i exactly right, then we will get almost no squared error and we can set the variance very small, paying little penalty. If we we’re less sure, then we expect a sizable squared error and we should increase the variance to reduce the impact a little. This way, we get a neural network that tells us not just what its best guess is, but also how sure it is about that guess.<br></p><aside    >Neural networks are very poor at estimating how sure they should be, so take this with a grain of salt, but in principle, the machinery is there for the network to provide an indication of certainty.</aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-008" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-008" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0008anim0.svg" data-images="51.DeepLearning2.key-stage-0008anim0.svg,51.DeepLearning2.key-stage-0008anim1.svg,51.DeepLearning2.key-stage-0008anim2.svg,51.DeepLearning2.key-stage-0008anim3.svg" class="slide-image" />

            <figcaption>
            <p    >For a solution that applies to high-dimensional outputs like images, we can use the outputs to parametrize a<em> multivariate</em> normal distribution. Here we'll parametrize both the mean and the covariance matrix.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-009">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-009" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0009.svg" class="slide-image" />

            <figcaption>
            <p    >If we provide both the  the mean and the variance of an output distribution, it looks like this (for an n-dimensional output space). We simply split the output layer in two parts, and interpret one part as the <span>mean</span> and the other as the<span> covariance matrix</span>.<br></p><p    >Since representing a full covariance matrix would grow very big for high-dimensional outputs, we usually assume that the covariance matrix is <strong>diagonal </strong>(all off-diagonal values are zero). That way the representation of the <span>covariance</span> requires as many arguments as the representations of the<span class="orange"> mean</span>, and we can simply split the output vector into two halves.<br></p><p    >Equivalently, we can think of the output distribution as putting an independent 1D Gaussian on each dimension, with a mean and variance provided for each.<br></p><p    >For the mean, we can use a linear activation, since it can have any value, including negative values. However, the values of the covariance matrix need to be positive. To achieve this, we often exponentiate them. We’ll call this an <strong>exponential activation</strong>. An alternative option is the <strong>softplus</strong> function ln(1 + e<sup>x</sup>), which grows less explosively.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-010">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-010" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0010.svg" class="slide-image" />

            <figcaption>
            <p    >Here’s what that looks like when we generate an image. The output distribution gives us a <span class="orange">mean</span> value for every channel of every pixel (a 3-tensor) and a corresponding <span class="blue">variance</span> for every mean. If we look at what that tells us about the red value of the pixel at coordinate (8, 7) we see that we get a univariate Gaussian with a particular mean and a variance. The mean tells us the network’s best guess for that value, and the variance tells us how <em>certain </em>the network is about this output. </p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-011" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-011" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0011anim0.svg" data-images="51.DeepLearning2.key-stage-0011anim0.svg,51.DeepLearning2.key-stage-0011anim1.svg,51.DeepLearning2.key-stage-0011anim2.svg" class="slide-image" />

            <figcaption>
            <p    >If we want to go all out, we can even make our neural network output the parameters of a Gaussian mixture model. This is called a <strong>mixture density network</strong>.<br></p><p    >All we need to do, is make sure that we have one output node for every parameter required, and apply different activations to the different kinds of parameters. The <span class="orange">means</span> get a linear activation and the <span class="blue">covariances </span>get an exponential activation as before. The component weights need to sum to one, so we need to give them a softmax activation (over just these three output values).<br></p><p    >If we want to train with maximum likelihood, we encounter this sum-inside-a-logarithm function again, which is difficult to deal with. But this time, it’s not such a headache. As we noted in the last lecture we can work out the gradient for this loss, it’s just a very ugly function. Since we are using backpropagation anyway, that needn’t worry us here. All we need to work out are the local derivatives or backward functions for functions like the logarithm and the sum, and those are usually provided by systems like Pytorch and Keras anyway.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-012" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-012" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0012anim0.svg" data-images="51.DeepLearning2.key-stage-0012anim0.svg,51.DeepLearning2.key-stage-0012anim1.svg" class="slide-image" />

            <figcaption>
            <p    >The mixture density network may seem like overkill, but it’s actually very useful in regression problems where multiple answers may be valid.<br></p><p    >Consider the problem of<strong> inverse kinematics</strong> in robotics. We have a robot arm with two joints, and we know where in space we want the hand of the arm to be. What angles should we set the two joints to? This is a great application for machine learning: it’s a relatively simple, smooth function. It’s easy to generate examples, and explicit solutions are a pain to write, and not robust to noise in the control of the robot. So we can solve it with a neural net. <br></p><p    >The inputs are the two coordinates where we want the hand to be (x<sub>1</sub>, x<sub>2</sub>), and the outputs are the two angles we should set the joints to (θ<sub>1</sub>, θ<sub>2</sub>). The problem we run into, is that for every input, <strong>there are two solutions</strong>. One with the elbow up, and one with the elbow down. A normal neural network trained with an MSE loss would not pick one or the other, but it would <em>average between the two</em>. <br></p><p    >A mixture density network with two components can fix this problem. For each input, it can simply put its components on the two valid solutions.<br></p><p    >image source: Mixture Density Networks, Christopher Bishop, 1994  <br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-013" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-013" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0013anim0.svg" data-images="51.DeepLearning2.key-stage-0013anim0.svg,51.DeepLearning2.key-stage-0013anim1.svg,51.DeepLearning2.key-stage-0013anim2.svg,51.DeepLearning2.key-stage-0013anim3.svg,51.DeepLearning2.key-stage-0013anim4.svg,51.DeepLearning2.key-stage-0013anim5.svg,51.DeepLearning2.key-stage-0013anim6.svg" class="slide-image" />

            <figcaption>
            <p    >The problem with the robot arm is that the task is uniquely determined in one direction—every configuration of the robot arms leads to a unique point in space for the hand—but not when we try to reason backward from the hand to the configuration of the joints. <br></p><p    >Here is a 2D version with that problem. Given x, we can predict t unambiguously. But, if we flip the problem and try to predict x given t, then at values like x=0.5, there are multiple predictions with high density. A network with a single Gaussian head (i.e. what we are implicitly doing when we are using least squares loss), will try to fit its Gaussian over both clusters of the data. This puts the mean, which is our ultimate prediction, <em>between</em> these two clusters, in a region where there is no data at all.<br></p><aside    >We can give the neural network control over the variance of this distribution as well, but all that achieves is that the variance grows to cover both groups of points. The mean stays in the same place.<br></aside><p    >By contrast, the mixture density network can output a distribution with two peaks. This allows it to cover the two groups of points in the output, and so solve the problem in a much more useful way.<br></p><p    >The general problem in the middle picture is called <strong>mode collapse</strong>: we have a problem with multiple acceptable answers, and instead of picking one of the answers at random, the neural network averages over all of them and produces a terrible answer.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-014" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-014" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0014anim0.svg" data-images="51.DeepLearning2.key-stage-0014anim0.svg,51.DeepLearning2.key-stage-0014anim1.svg" class="slide-image" />

            <figcaption>
            <p    >If our data is spread out in space in a complex, clustered pattern, and we  fit a simple unimodal distribution to it (that is, a distribution with one peak) then the result is a distribution that puts all the probability mass on the average of our points, but very <em>little</em> probability mass where the points actually are.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-015">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-015" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0015.png" class="slide-image" />

            <figcaption>
            <p    >Mixture density networks go some way towards letting us capture more complex distributions in our neural networks, but when we want to capture something as complex and rich as the distribution on images representing human faces, they’re still insufficient. <br></p><p    >A mixture model with k components gives us k modes. So in the space of images, we can pick k images to give high probability and the rest is just a simple Gaussian shape around those k points. The distribution on human faces has infinitely many modes (all possible human faces) that should all be about equally likely. To achieve a distribution this complex, we need to use the power of the neural net, not just to choose a finite set of modes, but to control the whole shape of the probability function. <br></p><p    >Letting the neural network pick the parameters of a distribution with a simple shape is only ever going to produce a distribution with a simple shape. We need to change our approach.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-016" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-016" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0016anim0.svg" data-images="51.DeepLearning2.key-stage-0016anim0.svg,51.DeepLearning2.key-stage-0016anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Here’s a more powerful idea: we put the probability distribution at the<em> start</em> of the network instead of at the end of it. We sample a point from some straightforward distribution, usually a standard normal distribution, and we feed that point to a neural net. The result of these two steps is a random point, so we’ve defined another probability distribution. We call this construction a <strong>generator network</strong>.<br></p><aside    >Compare this to how we defined parametrized multivariate normals in the previous lecture: we started with a standard normal distribution, and we applied a linear transformation. This is the same thing, but we’ve replaced the linear transformation by a nonlinear one.<br></aside><p    >If we ignore the value of the input, we are now sampling from an unconditional distribution on <strong>x</strong>.<br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-017">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-017" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0017.svg" class="slide-image" />

            <figcaption>
            <p    >To see what kind of distributions we might get when we do this, let’s try a little experiment. <br></p><p    >We wire up a random network as shown: a two-node input layer, followed by 12, 100-node fully-connected hidden layers with ReLU activations., and a final transformation back to two points. We <em>don’t train</em> the network. We just use Glorot initialisation to pick the parameters, and then  sample some points. Since the output is 2D, we can easily scatter-plot it.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-018">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-018" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0018.png" class="slide-image" />

            <figcaption>
            <p    >Here’s a plot of 100k points sampled in this way. Clearly, we’ve defined a highly complex distribution. Instead of having a finite set of single points as modes, we get strands of high probability in space, and sheets of lower, but nonzero probability. Remember, this network hasn’t been trained, so it’s not representing anything meaningful, but it shows that the distributions we can represent in this way is a highly complex family.<br></p><aside    >Note that the variance has shrunk, and the mean has drifted away from (0, 0); apparently our weight initialisation is not quite perfect.<br></aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-019">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-019" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0019.svg" class="slide-image" />

            <figcaption>
            <p    >We can also use this trick to generate images. A normal convolutional net starts with a low-channel, high resolution image, and slowly decreases the resolution by maxpooling, while increasing the number of channels. Here, we reverse the process. We shape our input into a low resolution image with a large number of channels. We slowly increase the resolution by upsampling layers, and decrease the number of channels.<br></p><p    >We can use regular convolution layers, or <strong>deconvolutions</strong>, which are a kind of upside-down convolution. Both approaches give us effective generator networks for images.<br></p><p    >We see, that even without training, we have produced a distribution on images that is very complex and non-uniform.<br></p><aside    >I’ve enhanced the contrast and saturation in these images to make the colors stand out a little more.</aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-020" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-020" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0020anim0.svg" data-images="51.DeepLearning2.key-stage-0020anim0.svg,51.DeepLearning2.key-stage-0020anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Of course, we can also use both options: we sample the input from a standard MVN, interpret the output as another MVN, and then sample from that.<br></p><p    >In these kinds of generator networks, the input is often called <strong>z</strong>, and the space of inputs is often called the<strong> latent space</strong>. As we will see later, this maps perfectly onto the hidden variable models of the previous lecture.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-021">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-021" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0021.svg" class="slide-image" />

            <figcaption>
            <p    >So the big question is, <strong>how do we train a generator network?</strong> Given some data, how do we set the weights of the network so that the sampled outputs start to look like the examples we have in our data?<br></p><p    >We’ll start with something that doesn’t work, to help us understand why the problem is difficult. Here is a naive approach: we simply sample a random point <strong class="blue">x</strong> (e.g. a picture) from the data, and sample a point <strong class="green">y</strong> from the model and train on how close they are. <br></p><aside    >The <span class="orange red">loss </span>could be any distance function between two tensors. The mean-squared error over the elements is a simple approach. If the elements are values between 0 and 1 (like in images), the binary cross-entropy makes sense too. For images the absolute value of the error (also called L1 loss) is also popular.</aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-022" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-022" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0022anim0.svg" data-images="51.DeepLearning2.key-stage-0022anim0.svg,51.DeepLearning2.key-stage-0022anim1.svg,51.DeepLearning2.key-stage-0022anim2.svg,51.DeepLearning2.key-stage-0022anim3.svg" class="slide-image" />

            <figcaption>
            <p    >If we implement this naive approach, we do not get a good probability distribution. Instead, we get <strong>mode collapse</strong>. <br></p><p    >Here is a schematic example of what's happening: the <span class="blue">blue points </span>represent the modes (likely points) of the data. The <span class="green">green point</span> is generated by the model. It’s close to one of the<span class="blue"> blue points</span>, so the model should be rewarded, but it’s also far away from almost all of the other points. During training, there’s no guarantee that we will pair it up with the correct point, and we are likely to compute the<span class="orange red"> loss</span> to a completely different point.<br></p><p    >On average the model is punished for generating such points much more often than it is rewarded. The model that generates only the open point in the middle gets a smaller loss (and less variance). Under backpropagation, neural networks tend to converge to a distribution that generates only <span class="green">the open point</span> over and over again.<br></p><p    >In other words, the many different modes (areas of high probability) of the data distribution end up being averaged (“collapsing”) into a single point.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-023">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-023" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0023.svg" class="slide-image" />

            <figcaption>
            <p    >Even though we have a probability distribution that is able to represent highly complex, multi-modal outputs, if we train it like this, we still end up producing a <strong>unimodal</strong> output centered on the mean of our data. If the dataset contains human faces, we get a fuzzy average of all faces, not a sample with individual details.<br></p><p    >How do we get the the network to<em> imagine details</em>, instead of averaging over all possibilities?</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-024">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-024" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0024.svg" class="slide-image" />

            <figcaption>
            <p    >There are two main approaches: GANs and variational autoencoders. We'll give a quick overview of the basic principle of GANs in the next part, and then a more detailed treatment of autoencoders and variational autoencoders in the last two parts.<br></p><p    ></p>
            </figcaption>
       </section>




       <section class="video" id="video-024">
           <a class="slide-link" href="https://mlvu.github.io/lecture09#video-24">link here</a>
           <iframe
                src="https://www.youtube.com/embed/eaWxDebDDo8?modestbranding=1&showinfo=0&rel=0"
                title="YouTube video player"
                frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
           </iframe>

       </section>



       <section id="slide-025">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-025" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0025.svg" class="slide-image" />

            <figcaption>
            <p    >In the last video, we defined <strong>generator networks</strong>, and we saw that they represent a very rich family of probability distributions. We also saw, that training them can be a tricky business.<br></p><p    >In this video we’ll look one way of training such networks: the method of <strong>generative adversarial networks (GANs)</strong>.<br></p><p    ><lnbr></lnbr></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-026" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-026" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0026anim0.svg" data-images="51.DeepLearning2.key-stage-0026anim0.svg,51.DeepLearning2.key-stage-0026anim1.svg,51.DeepLearning2.key-stage-0026anim2.png,51.DeepLearning2.key-stage-0026anim3.png,51.DeepLearning2.key-stage-0026anim4.png" class="slide-image" />

            <figcaption>
            <p    >GANs  originated just after Convolutional networks were breaking new ground, showing spectacular, sometimes super-human, performance in image labeling. The suggestion arose that perhaps convolutional networks were doing more or less the same as what humans do when they look at something.<br></p><p    >To verify this, researchers decided to start investigating  what kind of inputs would make a trained convolutional network give a certain output. This is easy to do, you just compute the gradient <em>with respect to the input of the network</em>, and train the input to maximise the activation of a particular label, while keeping the parameters of the network fixed. <br></p><aside    >This is similar to the feature visualizing approach we saw before, but you do it on the output nodes instead of the hidden nodes. <br></aside><p    >You would expect that if you start with a random image, and follow the gradient to maximize the activation of the output node corresponding to the label “bus”, you’d get a picture of a bus. Or at least something that looks a little bit like a bus. What you actually get is something that is indistinguishable from the noise you started with. Only the very tiniest of changes is require to make the network see a bus.<br></p><p    >These are called <strong>adversarial examples</strong>. Instances that are specifically crafted to trip up a given model.<br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-027">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-027" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0027.svg" class="slide-image" />

            <figcaption>
            <p    >The researchers also  found that if they started the search not at a random image, but at an image of another class, all that was needed to turn it into another class (according to the network) was a very small distortion. So small, that to us the image looks unchanged. In short, a tiny change to the image is enough to make a convolutional neural net think that a picture of a bus is a picture of an ostrich.<br></p><p    >Adversarial examples are an active area of research (both how to generate them and make models more robust against them).<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-028">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-028" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0028.svg" class="slide-image" />

            <figcaption>
            <p    >Even manipulating objects in the physical world can have this effect. A stop sign can be made to look like a different traffic sign by the simple addition of some stickers. Clearly, this has some worrying implications for the development of self-driving cars.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-029">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-029" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0029.svg" class="slide-image" />

            <figcaption>
            <p    >Pretty soon, this bad news was turned into good news by realising that if you can generate adversarial examples <em>automatically</em>, you can also add them to the dataset <em>as negatives</em> and retrain your network to make it more robust. You can simply tell your network that these things are not stop signs. Then, once your network is robust to the original adversarial examples, you can generate some new adversarial examples, and start the whole thing over again.<br></p><p    >We can think of this as a kind of iterated 2 player game (or an arms race). The <strong>discriminator</strong> (our classifier) tries to get good enough to tell fake data from real data and the <strong>generator</strong> (the algorithm that generates the adversarial examples) tries to get good enough to fool the discriminator.<br></p><p    >This is the basic idea of the <strong>generative adversarial network</strong>.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-030">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-030" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0030.png" class="slide-image" />

            <figcaption>
            <p    >We’ll look at four different examples of GANs. We’ll call the basic approach the “vanilla GAN”</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-031">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-031" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0031.svg" class="slide-image" />

            <figcaption>
            <p    >Generating adversarial examples by gradient descent is possible, but it’s much nicer if both our generator and our discriminator are separate neural networks. This will lead to a much cleaner approach for training GANs.<br></p><p    >We will draw the two components like this. The <strong class="orange red">generator </strong>takes an input sampled from a standard MVN and produces an image. This is a generator network as described in the previous video. We don't give it an output distribution (i.e. we're using option 2 from the previous part).<br></p><p    >The<strong class="orange red"> discriminator</strong> takes an image and classifies it as <span class="blue">Positive</span> (a real image of the target class) or <span class="orange red">Negative</span> (a fake image sampled from the generator). <br></p><p    >If we have other images that are not of the target class, we can add those to the negative examples as well, but often, the <span class="blue">positive</span> class is just our dataset (like a collection of human faces), and the <span class="orange red">negative</span> class is just the fake images created by the generator.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-032" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-032" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0032anim0.svg" data-images="51.DeepLearning2.key-stage-0032anim0.svg,51.DeepLearning2.key-stage-0032anim1.svg" class="slide-image" />

            <figcaption>
            <p    >To train the discriminator, we feed it examples from the<span class="blue"> positive</span> class, and train it to classify these as<span class="blue"> Pos</span>. <br></p><p    >We also sample images from the generator (whose weights we keep fixed) and train the discriminator to recognize these as negative. At first, these will just be random noise, but there’s little harm in telling our network that such images are not busses (or whatever our positive class is).<br></p><p    >Note that since the generator is a neural network, we don’t need to collect a dataset of fake images which we then feed to the discriminator. We can just stick the discriminator on top of the generator, <em>making a single computation graph</em>, and train it by gradient descent to classify the result as negative. We just need to make sure to freeze the weights of the generator, so that gradient descent only updates the discriminator.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-033">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-033" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0033.svg" class="slide-image" />

            <figcaption>
            <p    >Then, to train the generator, we freeze the discriminator and train the weights of the generator to produce images that cause the discriminator to label them as <strong class="blue">Positive</strong>. <br></p><p    >This step may take a little time to wrap your head around. If it helps, think of the whole disciminator as a very complicated loss function. Whatever the generator produces, the more likely the discriminator is to call it positive, the lower the loss.<br></p><p    >We don’t need to wait for either step to converge. We can just train a the discriminator for one batch (i.e. one step of gradient descent) and then train the generator for one batch, and so on. <br></p><p    >And this is what we’ll call the <strong>vanilla GAN</strong>.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-034" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-034" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0034anim0.png" data-images="51.DeepLearning2.key-stage-0034anim0.png,51.DeepLearning2.key-stage-0034anim1.png" class="slide-image" />

            <figcaption>
            <p    >Sometimes we want to train the network to map an input to an output, but to generate the output probabilistically. For instance, when we train a network to color in a black-and-white photograph of a flower, it could choose many colors for the flower. We want to avoid mode collapse here: instead of averaging over all possible colors, giving us a brown or gray flower, we want it to pick one color, from all the possibilities. <br></p><p    >A <strong>conditional GAN</strong> lets us train generator networks that can do this.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-035">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-035" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0035.svg" class="slide-image" />

            <figcaption>
            <p    >In a conditional GAN, the generator is a function with an image input, which it maps it to an image output. However, it uses randomness to imagine specific details in the output. <br></p><p    >In this example, it imagines the photograph corresponding to a line drawing of a shoe. Running this generator twice would result in different shoes that are both “correct” instantiations of the input line drawing.<br></p><p    >source: <a href="https://phillipi.github.io/pix2pix/"><strong class="blue">Image-to-Image Translation with Conditional Adversarial Networks </strong></a>(2016), Phillip Isola Jun-Yan Zhu et al.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-036">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-036" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0036.svg" class="slide-image" />

            <figcaption>
            <p    >To train a conditional GAN, we give the discriminator <strong>pairs of inputs and outputs</strong>. If these come from the generator, they should be classified as fake (negative) and if they come from the data, they should be classified as real (positive).<br></p><p    >The generator is trained in two ways. <br></p><p     class="list-item">We freeze the weights of the discriminator, as before, and train the generator to produce thins that the discriminator will think are <span class="green">real</span>. <br></p><p     class="list-item">We feed it and input from the data, and backpropagate on the corresponding output (using L1 loss).<br></p><aside    >There are many more details you need to be aware of to train a model like this well, but for now we will just focus on the high-level picture.</aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-037">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-037" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0037.png" class="slide-image" />

            <figcaption>
            <p    >The conditional GAN works really well, but only if we have an example of a specific output that corresponds to a specific input. For some tasks, we don’t have paired images. We only have unmatched bags of images in two domains. For instance, we know that a picture of a horse can be turned into a picture of that horse as a zebra (a skilled painter could easily do this), but we don't have a lot of paired images of horses and corresponding zebras. All we have is a large number of horse images and a large number of zebra images.<br></p><p    >If we randomly match one zebra image to a horse image, and train a conditional GAN on this, all we get is mode collapse.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-038">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-038" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0038.png" class="slide-image" />

            <figcaption>
            <p    >CycleGANs solve this problem using two tricks. <br></p><p    >First, we train generators to perform the transformation in both directions. We train both a horse-to-zebra generator and a zebra-to-horse generator. Then each horse in our dataset is transformed into a zebra <strong>and back again</strong>.This gives us a fake zebra picture, which we can use to train a zebra discriminator, together with the real zebra pictures. We do the same thing the other way around: we transform the zebras to fake horses and back again, and use the fake horses together with the real horses to train a horse discriminator.<br></p><p    >Second, we add a <strong>cycle consistency loss</strong>. When we transform a horse to a zebra and back again, we should end up with the same horse again. The more different the final horse picture is from the original, the more we punish the generator networks. <br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-039">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-039" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0039.svg" class="slide-image" />

            <figcaption>
            <p    ><br></p><p    >Here is the whole process in a diagram.<br></p><p    >One way to think of this is as the generators practicing steganography: hiding a secret message inside another innocent message. The generators are trying to hide a picture of a horse inside a picture of a zebra. The cycle consistency loss ensures that all the information of the horse picture is in the zebra picture and the horse picture can be fully decoded from the zebra picture. The discriminator's job is to tell which of the zebra pictures it sees have a horse hiding in it. <br></p><p    >If we have a strong discriminator and the generator can still fool it, then we get very realistic zebra pictures with horses hidden inside. Since the obvious way to make this transformation is to transform the horse into the zebra in the way we would do it, this is the transformation that the network learns.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-040">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-040" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0040.png" class="slide-image" />

            <figcaption>
            <p    >The CycleGAN works surprisingly well. Here’s how it maps photographs to impressionist paintings and vice versa.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-041">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-041" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0041.svg" class="slide-image" />

            <figcaption>
            <p    >It doesn’t always work perfectly, though.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-042">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-042" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0042.png" class="slide-image" />

            <figcaption>
            <p    >Finally, let’s take a look at the <strong>StyleGAN</strong>, the network that generated the faces we first saw in the introduction. This is basically a Vanilla GAN, with most of the special tricks in the way the generator is constructed. It uses too many tricks to discuss here in detail, so we’ll just focus on one aspect: the idea that the latent vector is fed to the network at each stage of its forward pass.<br></p><p    >Since an image generator starts with a coarse (low resolution), high level description of an image, and slowly fills in the details, feeding it the latent vector at every layer (transformed by an affine transformation to fit it to the shape of the data at that stage), allows it to use different parts of the latent vector to describe different aspects of the image (the authors call these “styles”).<br></p><p    >The network also receives separate extra random noise per layer, that allows it to make random choices. Without this, all randomness would have to come from the latent vector.<br></p><p    ><br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-043" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-043" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0043anim0.png" data-images="51.DeepLearning2.key-stage-0043anim0.png,51.DeepLearning2.key-stage-0043anim1.png,51.DeepLearning2.key-stage-0043anim2.png,51.DeepLearning2.key-stage-0043anim3.png" class="slide-image" />

            <figcaption>
            <p    >To see how this works, we can try to manipulate the network, by changing the latent vector to another for some of the layers. In this example all images on the margins are people that are generated for a particular single latent vector.<br></p><p    >We then re-generate the image for <span class="orange red">the destination,</span> except that for a few layers (at the bottom, middle or top), we use<span class="blue"> the source</span> latent vector instead.  <br></p><p    >As we see, overriding the bottom layers changes things like gender, age and hair length, but not ethnicity. For the middle layer, the age is largely taken from the destination image, but the ethnicity is now override by the source. Finally for the top layers, only surface details are changed.<br></p><p    >This kind of manipulation was done during training as well, to ensure that it would lead to faces that fool the discriminator.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-044">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-044" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0044.svg" class="slide-image" />

            <figcaption>
            <p    >Let’s look at the other side of the network: the noise inputs. <br></p><p    >If we keep all the<span> latent</span> and <span>noise</span> inputs the same except for the very last noise input, we can see what the noise achieves: the man’s hair is equally messy in each generated example, but exactly in what way it’s messy changes per sample. The network uses the noise to determine the precise orientation of the individual “hairs”.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-045">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-045" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0045.svg" class="slide-image" />

            <figcaption>
            <p    >We’ve given you a high level overview of GANs, which will hopefully give you an intuitive grasp of how they work. However, GANs are notoriously difficult to train, and many other tricks are required to get them to work. Here are some phrases you should Google if you decide to try implementing your own GAN.<br></p><p    >In the next video, we’ll look at a completely different approach to training generator networks: autoencoders.</p><p    ></p>
            </figcaption>
       </section>




       <section class="video" id="video-045">
           <a class="slide-link" href="https://mlvu.github.io/lecture09#video-45">link here</a>
           <iframe
                src="https://www.youtube.com/embed/t6GxDo1fSt0?modestbranding=1&showinfo=0&rel=0"
                title="YouTube video player"
                frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
           </iframe>

       </section>



       <section id="slide-046">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-046" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0046.svg" class="slide-image" />

            <figcaption>
            <p    >In this part, we'll start to lay the groundwork for<strong> Variational Autoencoders</strong>. This starts with a completely different abstract task: dimensionality reduction. We'll see that given a dimensionality reduction model, we can often turn it into a generative model with a few hacks. In the next part, we will then develop this type of model in a more grounded and theoretical way.<br></p><p    ><lnbr></lnbr></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-047">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-047" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0047.svg" class="slide-image" />

            <figcaption>
            <p    >Before we turn to autoencoders, let's first look at what we can do once we've trained a generator network. We’ll look at four use cases.<br></p><p    >The first, of course is that we can generate data that looks like it came from the same distribution as ours.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-048" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-048" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0048anim0.png" data-images="51.DeepLearning2.key-stage-0048anim0.png,51.DeepLearning2.key-stage-0048anim1.png" class="slide-image" />

            <figcaption>
            <p    >Another thing we can do is <strong>interpolation</strong>.<br></p><p    >If we take two points in the input space, and draw a line between them, we can pick evenly spaced points on that line and decode them. If the generator is good, this should give us a smooth transition from one point to the other, and each point should result in a convincing example of our output domain.<br></p><p    >Remember that in some contexts, we refer to the input of a generator network as its <strong>latent space</strong>.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-049">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-049" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0049.png" class="slide-image" />

            <figcaption>
            <p    >We can also draw an<strong> interpolation grid</strong>; we just map the corners of a square lattice of equally spaced points to four points in our input space, and run all points through the generator network.<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-050">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-050" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0050.svg" class="slide-image" />

            <figcaption>
            <p    >If the latent space is high dimensional, most of the probability of the standard MVN is near the edges of the radius-1 hypersphere (not in the centre as it is in 1, 2 and 3-dimensional MVNs). <br></p><aside    >High-dimensional MVNs look <a href="https://www.inference.vc/high-dimensional-gaussian-distributions-are-soap-bubble/"><strong class="blue">more like a soap bubble</strong></a> than the dense pointcloud we’re used to seeing in low-dimensional visualizations.<br></aside><p    >For that reason, we get better results if we interpolate along an arcinstead of along a straight line. This is called <strong>spherical linear interpolation</strong>.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-051">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-051" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0051.svg" class="slide-image" />

            <figcaption>
            <p    >What if we want to interpolate between points in our dataset? It’s possible to do this with a GAN trained generator, but to make this work, we first have to <em>find</em> our data points in the input spoace. Remember, during training the discriminator is the only network that gets to see the actual data. We never explicitly map the data to the latent space.<br></p><p    >We can tack a mapping from data to latent space onto the network after training (as was done for these images), but we can also learn such a mapping directly. As it happens, this can help us to train the generator in a much more direct way.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-052" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-052" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0052anim0.svg" data-images="51.DeepLearning2.key-stage-0052anim0.svg,51.DeepLearning2.key-stage-0052anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Note that such a mapping would also give us a <strong>dimensionality reduction</strong>. We can see the latent space representation of the data as a reduced dimensionality representation of the input.<br></p><p    >We’ll focus on the perspective of dimensionality reduction for the rest of this video, to set up basic autoencoders. We can get a generator network out of these, but it’s a bit of an afterthought. In the next video, we’ll see how to train generator networks with a data-to-latent-space mapping in a more principled way.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-053">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-053" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0053.svg" class="slide-image" />

            <figcaption>
            <p    >Here’s what a simple <strong>autoencoder</strong> looks like. It’s is a particular type of neural network, shaped like an hourglass. Its job is just to make the output as close to the input as possible, but somewhere in the network there is <span class="blue">a small layer</span> that functions as a bottleneck. <br></p><p    >After the network is trained, this small layer becomes a compressed low-dimensional representation of the input.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-054" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-054" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0054anim0.svg" data-images="51.DeepLearning2.key-stage-0054anim0.svg,51.DeepLearning2.key-stage-0054anim1.svg,51.DeepLearning2.key-stage-0054anim2.svg" class="slide-image" />

            <figcaption>
            <p    >Here’s the picture in detail. We call the bottom half of the network the <strong class="orange red">encoder</strong> and the top half the <strong class="green">decoder</strong>. We feed the autoencoder an instance from our dataset, and all it has to do is reproduce that instance in its output. We can use any loss that compares the output to the original input, and produces a lower loss, the more similar they are. Then, we just brackpropagate the loss and train by gradient descent.<br></p><aside    >Least-squares loss, absolute error loss and binary cross-entropy are popular choices<br></aside><p    >We call the  blue layer the<span class="blue"> </span><strong class="blue">latent representation</strong> of the input. If we train an autoencoder with just two nodes on the latent representation, we can plot what latent representation each input is assigned. If the autoencoder works well, we expect to see similar images clustered together (for instance smiling people vs frowning people, men vs women, etc).<br></p><aside    >In a 2D space, we can’t cluster too many attributes together, but in higher dimensions it’s easier.  To quote <a href="http://jeffclune.com/courses/media/courses/2016-Fall-AI/lectures/L24-AI-2016.pdf"><strong class="blue">Geoff Hinton</strong></a>: “If there was a 30 dimensional supermarket, [the anchovies] could be close to the pizza toppings and close to the sardines.”</aside><aside    ></aside>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-055">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-055" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0055.svg" class="slide-image" />

            <figcaption>
            <p    >To show what this looks like, we've set up a relatively simple autoencoder consisting of convolutions in the encoder and deconvolutions in the decoder. We train it on a low-res version of the <a href="https://github.com/NVlabs/ffhq-dataset"><strong class="blue">FFHQ dataset</strong></a> of human faces. We give the latent space 256 dimensions.<br></p><aside    >For the PCA lecture we used black and white data to make the task easier. Since we have a more powerful model, we can use more varied full-color data. The StyleGAN was trained on the full-resolution version of this data.<br></aside><p    >Here are the reconstructions on a very simple network, with MSE loss on the output after 5 full passes over the data. </p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-056">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-056" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0056.svg" class="slide-image" />

            <figcaption>
            <p    ></p>
            </figcaption>
       </section>





       <section id="slide-057">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-057" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0057.svg" class="slide-image" />

            <figcaption>
            <p    ></p>
            </figcaption>
       </section>





       <section id="slide-058">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-058" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0058.svg" class="slide-image" />

            <figcaption>
            <p    >After 300 epochs, the autoencoder has pretty much converged. Here are the reconstructions next to the original data. Considering that we've reduced each image to just 256 numbers, it's not too bad.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-059" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-059" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0059anim0.svg" data-images="51.DeepLearning2.key-stage-0059anim0.svg,51.DeepLearning2.key-stage-0059anim1.svg,51.DeepLearning2.key-stage-0059anim2.svg" class="slide-image" />

            <figcaption>
            <p    >One thing we can now do is to study the latent space based on the examples that we have. For instance, we can see whether smiling and non-smiling people end up in distinct parts of the latent space.<br></p><p    >We just label a small amount of instances as<span class="orange"> smiling</span> and <span class="blue">nonsmiling</span> (just 20 each in this case). If we're lucky, these form distinct clusters in our latent space. If we compute the means of these clusters, we can draw a vector between them. We can think of this as a “smiling” vector. The further we push people along this line, the more the decoded point will smile.<br></p><p    >This is one big benefit of autoencoders: we can train them on unlabeled data (which is cheap) and then use only a <em>very</em> small number of labeled examples to “annotate” the latent space. In other words, autoencoders are a great way to do <strong>semi-supervised learning</strong>.<br></p><aside    >Compare this to what we did in our previous dimensionality reduction method of principal component analysis. There, we found that dimensions in the reduced space corresponded to high-level semantic concepts like gender and expression. Here, the latent space is a little more "entangled", but we can usually still find distinct directions for high-level concepts (they are just not aligned with the axes).</aside><aside    ></aside>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-060">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-060" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0060.svg" class="slide-image" />

            <figcaption>
            <p    >Once we've worked out what the smiling vector is, we can manipulate photographs to make people smile. We just encode their picture into the latent space, add the smiling vector (times some small scalar to control the effect), and decode the manipulated latent representation. If the autoencoder understands "smiling" well enough, the result will be the same picture but manipulated so that the person will smile.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-061">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-061" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0061.svg" class="slide-image" />

            <figcaption>
            <p    >Here is what that looks like for our (simple) example model. In the middle we have the decoding of the original data, and to the right we see what happens if we add an increasingly large multiple of the smiling vector.<br></p><p    >To the right we subtract the smiling vector, which makes the person frown.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-062" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-062" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0062anim0.svg" data-images="51.DeepLearning2.key-stage-0062anim0.svg,51.DeepLearning2.key-stage-0062anim1.svg" class="slide-image" />

            <figcaption>
            <p    >With a bit more powerful model, and some face detection, we can see what some famously moody celebrities might look like if they smiled.<br></p><p    >source: <a href="https://blogs.nvidia.com/blog/2016/12/23/ai-flips-kanye-wests-frown-upside-down/"><strong class="blue">https://blogs.nvidia.com/blog/2016/12/23/ai-flips-kanye-wests-frown-upside-down/</strong></a><br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-063">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-063" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0063.svg" class="slide-image" />

            <figcaption>
            <p    >What we get out of an autoencoder, depends on which part of the model we focus on.<br></p><p    >If we keep the <span class="orange red">encoder</span> and the <span class="green">decoder</span>, we get a network that can help us manipulate data in this way.<br></p><p    >If we keep just the <span class="green">encoder</span>, we get a powerful dimensionality reduction method. We can use the latent space representation as the features for a model that does not scale well to too many features (like a non-naive Bayesian classifier).<br></p><p    >But this lecture was about generator networks. How do we get a generator out of a trained autoencoder? It turns out we can do this by keeping just the <span class="green">decoder</span>.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-064">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-064" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0064.svg" class="slide-image" />

            <figcaption>
            <p    >We don’t know beforehand where the data will end up in latent space, but after training we can just check. We encode the training data, fit a distribution to this point cloud in our latent space, and then just use this distribution as the input to our <span class="green">decoder</span> to create a generator network.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-065">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-065" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0065.svg" class="slide-image" />

            <figcaption>
            <p    >This is the point cloud of the <span class="blue">latent representations</span> in our example. We plot the first two of the 256 dimensions, resulting in the blue point cloud.<br></p><p    >To these points we, we fit an MVN (in 256 dimensions), and we sample 400 new points from it, the<span class="orange red"> red</span> dots.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-066">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-066" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0066.svg" class="slide-image" />

            <figcaption>
            <p    >If we feed these points to the decoder, this is what we get. It's not quite up these with the style gan results, but clearly, the model can generate some non-existant people.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-067">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-067" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0067.svg" class="slide-image" />

            <figcaption>
            <p    >This has given us a generator, but we have little control over what the latent space looks like. We just have to hope that it looks enough like a normal distribution that our MVN makes a good fit. In the GAN, we have perfect control over what our distribution on the latent space looks like; we can freely set it to anything. However, there, we have to fit a mapping from data to latent space after the fact.<br></p><p    >We’ve also seen that this interpolation works well, but it’s not something we’ve specifically trained the network to do. In the GAN, we should expect all latent space points to decode to something that fools the decoder, but in the autoencoder, there is nothing that stops the points <em>in between</em> the data points from decoding to garbage.<br></p><p    >Moreover, neither the GAN nor the autoencoder is a very principled way of optimizing. Is there a way to train for <strong>maximum likelihood</strong> directly?<br></p><p    >The answer to all of these questions is the<strong> variational autoencoder</strong>, which we’ll discuss in the next video.<br></p><p    ></p>
            </figcaption>
       </section>




       <section class="video" id="video-067">
           <a class="slide-link" href="https://mlvu.github.io/lecture09#video-67">link here</a>
           <iframe
                src="https://www.youtube.com/embed/inUJd7f931g?modestbranding=1&showinfo=0&rel=0"
                title="YouTube video player"
                frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
           </iframe>

       </section>



       <section id="slide-068">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-068" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0068.svg" class="slide-image" />

            <figcaption>
            <p    ><lnbr></lnbr></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-069">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-069" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0069.svg" class="slide-image" />

            <figcaption>
            <p    >The variational autoencoder is a more principled way to train a generator network using the principles of an autoencoder. This requires a little more math, but we get a few benefits in return.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-070">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-070" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0070.svg" class="slide-image" />

            <figcaption>
            <p    >We’ll start with the maximum log-likelihood objective. We want to choose our parameters θ (the weights of the neural network) to maximise the log likelihood of the data. We will write this objective step by step until we end up with an autoencoder.<br></p><aside    >We're specifically using the natural logarithm here because it will simplify things a little down the road.</aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-071">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-071" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0071.svg" class="slide-image" />

            <figcaption>
            <p    >The first insight is that we can view our generator as a hidden variable model. We have a hidden variable <strong>z</strong>, which is standard normally distributed and then fed to a neural network to produce a variable <strong>x</strong>, which we observe. <br></p><p    >The network computes the conditional distribution of <strong>x</strong> given <strong>z</strong>.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-072" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-072" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0072anim0.svg" data-images="51.DeepLearning2.key-stage-0072anim0.svg,51.DeepLearning2.key-stage-0072anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Here we see how the hidden variable problem causes our mode collapse. If we knew which <strong>z</strong> was supposed to produce which <strong>x</strong>, we could feed that z to the network compute the loss between the output and x and optimize by backpropagation and gradient descent.<br></p><p    >The problem, as in the previous lecture, is that we don’t have the complete data. We don’t know the values of <strong>z</strong>, only the values of <strong>x</strong>. There, we introduced a distribution q to approximate the "completion" of the data. We'll do that here as well: we'll introduce a probability distribution that tells us, for a given instance x, which latent representations are most likely.<br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-073">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-073" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0073.svg" class="slide-image" />

            <figcaption>
            <p    >Before we define q, let's think what it needs to approximate. We want a distribution on the latent space, conditional on some instance <strong>x </strong>(for instance an image).</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-074">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-074" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0074.svg" class="slide-image" />

            <figcaption>
            <p    >In the EM algorithm, we defined q as a big table of numbers (the responsibilities). Because we were approximating a categorical distribution, we could just set the parameters of q(z|x) explicitly for every x. Here, we want to <em>generalize</em> more: we will train a neural network to learn a function that maps a given instance <strong>x</strong> to a distribution on the latent space. If the network works well the correct latent representation (the one that decodes to <strong>x</strong> if we feed it to the generator) will get a high probability density under the distribution produced by this network.<br></p><p    >This is the network we’ll use. It consumes <strong>x</strong> and it produces a normal distribution on <strong>z</strong>. It has its own parameters, phi, which are not related to the parameters theta of p.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-075">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-075" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0075.svg" class="slide-image" />

            <figcaption>
            <p    >In the EM algorithm, for a given choice of parameters θ for <span class="green">p</span>(<strong>x</strong>|<strong>z</strong>, θ), we could easily work out the reverse distribution on <strong>z</strong>, conditioned on <strong>x</strong>. This gave us a target that <span class="orange red">q </span>should approximate.<br></p><p    >Here, things aren’t so easy. To work out <span class="green">p</span>(z|x, θ) we would need to<strong> invert</strong> the neural network: work out for a particular output <strong>x</strong>, which input values z are likely to have caused that output.<br></p><p    >This is not impossible to do (we saw something similar in at the start of the lecture), but its a costly and imprecise business. Just like we did with the GANs, it’s best to introduce a network that will learn the inversion for us. For this reason, we won't follow the EM logic of alternating approximation. Instead, we'll figure out a way to train <span class="green">p</span> and <span class="orange red">q</span> <strong>together</strong>. We’ll try to update the parameters of <span class="green">p</span> to fit the data, and try we’ll update the parameters of <span class="green">q</span> to keep it a good approximation to the inversion of <span class="green">p</span>.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-076" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-076" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0076anim0.svg" data-images="51.DeepLearning2.key-stage-0076anim0.svg,51.DeepLearning2.key-stage-0076anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Since the parameters of our model are the neural network weights, we’ll simplify our notation like this. <br></p><p    >This emphasizes that even though these are probabilities, the conditional probabilities shown here are the only ones that we can efficiently compute. We can’t reverse the conditional, or marginalize anything out. The price we pay for using the power of neural networks is that we are stuck with these functions and have build an algorithm on just these.<br></p><p    >With one exception. We do know the marginal distribution on <strong>z</strong>, since that is what we defined as the distribution on the input of our generator neural net: it’s a simple standard normal MVN.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-077">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-077" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0078.svg" class="slide-image" />

            <figcaption>
            <p    >Putting everything together, this is our model. If we feed <strong class="orange red">q</strong><sub class="orange red">v</sub> an instance from our data <strong>x</strong>, we get a normal distribution on the latent space. If we sample a point <strong>z</strong> from this distribution, and feed it to <strong class="green">p</strong><sub class="green">w </sub>we get a distribution on <strong>x</strong>. If the networks are both well trained, this should give us a good reconstruction of <strong>x</strong>.<br></p><p    >The neural network <strong class="green">p</strong><sub class="green">w</sub> is our probability distribution conditional on the latent vector. <strong class="orange red">q</strong><sub class="orange red">v</sub> is our approximation of the conditional distribution on <strong>z</strong>.<br></p><aside    >We are beginning to see the autoencoder emerge. Note that this is relatively incidental. We are just trying to train the generator network, and all we've done is introduce <span class="orange red">q</span> as an approximation to the inverse of <span class="green">p</span>. At no point did we set out to build a dimensionality reduction method.<br></aside><aside    ></aside>
            </figcaption>
       </section>





       <section id="slide-078">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-078" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0079.svg" class="slide-image" />

            <figcaption>
            <p    >We can now apply the decomposition we proved in the last lecture. We look at the marginal distribution on x, and break it up into two terms using <span class="orange red">q</span>.<br></p><p    >Before, we had a discrete hidden variable, and now we have a continuous one, but the proof still works (since we wrote everything in terms of expectations).<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-079" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-079" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0080anim0.svg" data-images="51.DeepLearning2.key-stage-0080anim0.svg,51.DeepLearning2.key-stage-0080anim1.svg,51.DeepLearning2.key-stage-0080anim2.svg,51.DeepLearning2.key-stage-0080anim3.svg" class="slide-image" />

            <figcaption>
            <p    >Here is the decomposition, rewritten in our new notation.<br></p><p    >In the EM algorithm, we used this to set up an alternating optimization algorithm: first optimizing one term and then the other. To do that here, we’d need to minimize the KL divergence between <span class="orange red">q</span> and the inverse of <span class="green">p</span>. This is possible, but expensive. As we said before, the inverse of <span class="green">p</span> is hard to compute.<br></p><p    >Instead, we’ll follow a cheaper track: we'll maximize a lower bound to the value we actually want to maximize.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-080" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-080" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0081anim0.svg" data-images="51.DeepLearning2.key-stage-0081anim0.svg,51.DeepLearning2.key-stage-0081anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Because we cannot invert <span class="green">p</span><sub class="green">w</sub>, we cannot easily compute the KL term (let alone optimise <span class="orange red">q</span><sub class="orange red">v</sub><span class="orange red"> </span>to minimise it). <br></p><p    >Instead, we focus entirely on the L term. Since it’s a lowerbound on the quantity we’re trying to maximize, anything that increases L will help our model. The better we maximise L, the better our model will do.<br></p><aside    >Note that this is only a lowerbound because we know that the KL term cannot be negative. If the KL divergence could be negative, the L term could be larger or smaller than the log-likelihood.<br></aside><p    ><br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-081" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-081" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0082anim0.svg" data-images="51.DeepLearning2.key-stage-0082anim0.svg,51.DeepLearning2.key-stage-0082anim1.svg,51.DeepLearning2.key-stage-0082anim2.svg" class="slide-image" />

            <figcaption>
            <p    >Here’s a visualisation of how a lower bound objective works. We’re interested in finding the highest point of the <span class="blue">blue line </span>(the maximum likelihood solution), but that’s difficult to compute. Instead, we maximise the <span class="orange">orange line </span>(the evidence lower bound). Because it’s guaranteed to be below the blue line everywhere, we may expect to be finding a high value for the blue line as well. To some extent, pushing up the orange line, pushes up the  blue line as well.<br></p><p    >How well we do on the blue line depends a lot on how <em>tight</em> the lower bound is. The distance between the lower bound and the log likelihood is expressed by the KL divergence between <span class="green">p</span><sub class="green">w</sub><span class="green">(z|x)</span> and<span class="orange red"> q</span><sub class="orange red">v</sub><span class="orange red">(z|x)</span>. That is, because we cannot easily compute <span class="green">p</span><sub class="green">w</sub><span class="green">(z|x)</span>, we introduced an approximation<span class="orange red"> q</span><sub class="orange red">v</sub><span class="orange red">(z|x)</span> . The better this approximation, the lower the KL divergence, and the tighter the lower bound.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-082" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-082" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0083anim0.svg" data-images="51.DeepLearning2.key-stage-0083anim0.svg,51.DeepLearning2.key-stage-0083anim1.svg,51.DeepLearning2.key-stage-0083anim2.svg,51.DeepLearning2.key-stage-0083anim3.svg,51.DeepLearning2.key-stage-0083anim4.svg,51.DeepLearning2.key-stage-0083anim5.svg,51.DeepLearning2.key-stage-0083anim6.svg" class="slide-image" />

            <figcaption>
            <p    >Right now, we can’t use L as a loss function directly, since  it contains functions like <span class="green">p</span>(x,z) that are not easily computed and because it’s an expectation. We’ll rewrite it step by step until it’s a loss function that can de directly used, heaply and easily in a deep learning system.<br></p><p    >Since we want to implement a loss function, we will <em>minimize </em>the negative of the L function. We now need to work out what that means for our neural net.<br></p><p    >All three probability functions we are left with are ones we can easily compute: <span class="orange red">q</span>(z|x) is given by the encoder network, <span class="green">p</span>(x|z) is given by the decoder network, and <span class="green">p</span>(z) was chosen when we defined (back in part 1) how the generator works, if we marginalize out x, the distribution on z is a standard multivariate normal.<br></p><aside    >Since we now take the expectation over a continuous distribution, all sums become integrals and (inside all expectations and inside the KL divergence). By keeping everything written as expectations, we ensure that we don’t have to deal with integrals.</aside><aside    ></aside>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-083" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-083" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0084anim0.svg" data-images="51.DeepLearning2.key-stage-0084anim0.svg,51.DeepLearning2.key-stage-0084anim1.svg" class="slide-image" />

            <figcaption>
            <p    >Let's see if this is a loss function we can implement in a system like pytorch.<br></p><p    >The KL term is just the KL divergence between the MVN that the encoder produces for x and the standard normal MVN. This <a href="https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence#Multivariate_normal_distributions"><strong class="blue">works out</strong></a> as a relatively simple differentiable function of <span class="orange">mu</span> and <span class="blue">sigma</span>, so we can use it directly in a loss function.<br></p><aside    >Remember that <span class="blue">θ</span><sub>z</sub> is usually restricted to a diagonal matrix, so the network just outputs a vector of the same size as <span class="orange">μ</span><sub>z</sub>, which we take to be the diagonal of the covariance matrix.</aside><aside    ></aside>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-084" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-084" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0085anim0.svg" data-images="51.DeepLearning2.key-stage-0085anim0.svg,51.DeepLearning2.key-stage-0085anim1.svg" class="slide-image" />

            <figcaption>
            <p    >The second part of our loss function requires a little more work. It’s an <strong>expectation</strong> for which we don’t have a closed form expression. Instead, we can <em>approximate</em> it by taking some samples, and averaging them. To keep things simple, we just take a single sample (we’ll be computing the network lots of times during training, so overall, we’ll be taking lots of samples).</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-085">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-085" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0086.svg" class="slide-image" />

            <figcaption>
            <p    >We almost have a fully differentiable model. Unfortunately, we still have a <strong>sampling step</strong> in the middle (and sampling is not a differentiable operation).<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-086">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-086" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0087.svg" class="slide-image" />

            <figcaption>
            <p    >We can get get rid of it by remembering the algorithm for sampling from a given MVN. We sample from the standard MVN, and <em>transform</em> the sample using the parameters of the required MVN.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-087">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-087" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0088.svg" class="slide-image" />

            <figcaption>
            <p    >Since we have, by construction, a diagonal covariance matrix, the sampling algorithm is particularly simple. We just sample a vector from a standard normal distribution, element-wise multiply it by the <span class="blue">vector of standard deviations of the target distribution</span>, and add <span class="orange">the mean of the target distribution</span>.<br></p><p    >Looking at this algorithm we can see two things. First, the sampling part doesn't depend on the parameters produced by <span class="orange red">q</span>. We can do all the random bits before we know what parameters <span class="orange red">q</span> has produced for us. Second, the rest of the algorithm is a simple, differentiable and affine operation. <br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-088">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-088" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0089.svg" class="slide-image" />

            <figcaption>
            <p    >This means that we can basically work the sampling algorithm <em>into the architecture of the network</em>. We provide the network with an<span class="orange"> </span><strong class="orange">extra input</strong>: a sample from the standard MVN. <br></p><aside    >Note that this requires the network to produce standard deviations instead of variances. So long as the outputs are positive, we can just interpret them as standard deviations, and assume that the network will learn to produce standard deviations instead of variances.<br></aside><p    >Why does this help us? We’re still sampling, but we’ve moved the random sampling out of the way of the backpropagation. The gradient can now propagate down to the weights of the <span class="orange red">q </span>function, and the actual randomness is treated as an<em> input</em>, rather than a computation.<br></p><p    >And with that, we have a fully differentiable loss function that we can put into a system like Keras or pytorch to train our autoencoder.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-089">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-089" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0090.svg" class="slide-image" />

            <figcaption>
            <p    >The two terms of the loss function are usually called <span class="orange red">KL loss</span> and <span class="green">reconstruction loss</span>. <br></p><p    >The <span class="green">reconstruction loss</span> maximises the probability of the current instances. This is basically the same loss we used for the regular autoencoder: we want the output of the decoder to look like the input.<br></p><p    >The<span class="orange red"> KL loss </span>ensures that the latent distributions are clustered around the origin, with variance 1. Over the whole dataset, it ensures that the latent distribution looks like a standard normal distribution.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-090">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-090" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0091.svg" class="slide-image" />

            <figcaption>
            <p    >The formulation of the VAE has three forces acting on the latent space. The reconstruction loss pulls the latent distribution as much as possible towards a single point that gives the best reconstruction. Meanwhile, the KL loss, pulls the latent distribution (for all points) towards the standard normal distribution, acting as a <strong>regularizer</strong>. Finally, the sampling step ensures that not just a single point returns a good reconstruction, but a whole <em>neighbourhood</em> of points does. The effect can be summarized as follows:<br></p><p    >The <strong class="green">reconstruction loss </strong>ensures that there are points in the latent space that decode to the data.<br></p><p    >The<strong> </strong><strong class="orange red">KL loss</strong> ensures that all these points together are laid out like a standard normal distribution.<br></p><p    >The<strong> sampling step </strong>ensure that points in between these also decode to points that resemble the data.<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-091" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-091" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0092anim0.svg" data-images="51.DeepLearning2.key-stage-0092anim0.svg,51.DeepLearning2.key-stage-0092anim1.svg,51.DeepLearning2.key-stage-0092anim2.svg,51.DeepLearning2.key-stage-0092anim3.svg" class="slide-image" />

            <figcaption>
            <p    >To define an autoencoder, we need to choose the output distribution of our decoder, which will determine the precise form of the reconstruction loss. In these slides, we've used a normal distribution, but for images, that's not usually the best choice. <br></p><p    >We can get slightly better results with a Laplace distribution, but convergence will still be slow. <br></p><p    >Better results are achieved with the binary cross entropy. This doesn't correspond to a proper distribution on continuous valued image tensors, but it's often used anyway because of the fact convergence. To fix this problem, you can use something called <a href="https://en.wikipedia.org/wiki/Continuous_Bernoulli_distribution"><strong class="blue">a continuous Bernoulli distribution</strong></a>, which will give you fast convergence and a theoretically correct VAE.</p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-092">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-092" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0093.svg" class="slide-image" />

            <figcaption>
            <p    >Here are some reconstructions for the regular autoencoder and for the VAE. They perform pretty similarly. There are slight differences if you look closely, but it's hard to tell which is better.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-093">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-093" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0094.svg" class="slide-image" />

            <figcaption>
            <p    >However, if we generate data by providing the generator with a random input, the difference becomes more pronounces. Here we see that the VAE is more likely to generate complete, and coherent faces (although both models still struggle with the background).</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-094">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-094" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0095.svg" class="slide-image" />

            <figcaption>
            <p    >For completeness, here is the smiling vector, applied to the VAE model.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-095">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-095" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0096.png" class="slide-image" />

            <figcaption>
            <p    >Here are some examples from a more elaborate VAE.<br></p><p    >source: Deep Feature Consistent Variational Autoencoder by Xianxu Hou, Linlin Shen, Ke Sun, Guoping Qiu<br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-096" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-096" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0097anim0.svg" data-images="51.DeepLearning2.key-stage-0097anim0.svg,51.DeepLearning2.key-stage-0097anim1.svg" class="slide-image" />

            <figcaption>
            <p    >![An animated example of latent space interpolation in the DCVAE](https://houxianxu.github.io/assets/dfcvae/combined.gif)<br></p><p    >source: <a href="https://houxianxu.github.io/assets/project/dfcvae"><strong class="blue">https://houxianxu.github.io/assets/project/dfcvae</strong></a></p><p    ><a href="https://houxianxu.github.io/assets/project/dfcvae"><strong class="blue"></strong></a></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-097">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-097" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0098.svg" class="slide-image" />

            <figcaption>
            <p    >Here is what the algorithm looks like in Pytorch. Load the 5th worksheet to give it a try.<br></p><p    ><a href="https://github.com/mlvu/worksheets/blob/master/Worksheet%205%2C%20Pytorch.ipynb"><strong class="blue">https://github.com/mlvu/worksheets/blob/master/Worksheet%205%2C%20Pytorch.ipynb</strong></a><br></p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-098">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-098" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0099.svg" class="slide-image" />

            <figcaption>
            <p    >In this worksheet, the VAE is trained on MNIST data, with a 2D latent space. Here is the original data, plotted by their latent coordinates. The colors represent the classes, to which the VAE did not have access.<br></p><p    >If you run the worksheet, you’ll end up with this picture (or one similar to it).</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-099" class="anim">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-099" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0100anim0.svg" data-images="51.DeepLearning2.key-stage-0100anim0.svg,51.DeepLearning2.key-stage-0100anim1.svg" class="slide-image" />

            <figcaption>
            <p    >While the added value of the VAE is a bit difficult to detect in our example, in other domains it’s more clear. <br></p><p    >Here is an example of interpolation on sentences. First using a regular autoencoder, and then using a VAE. Note that the intermediate sentences for the AE are non-grammatical, but the intermediate sentences for the VAE are all grammatical.<br></p><p    ><br></p><p    >source: Generating Sentences from a Continuous Space by Samuel R. Bowman, Luke Vilnis, Oriol Vinyals, Andrew M. Dai, Rafal Jozefowicz, Samy Bengio<br></p><p    >https://arxiv.org/abs/1511.06349<br></p><p    ></p>
            </figcaption>
            <span class="hint">click image for animation</span>
       </section>





       <section id="slide-100">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-100" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0101.svg" class="slide-image" />

            <figcaption>
            <p    >We see that GANs are in many ways the inverse of autoencoders, in that GANS have the data space as the inside of the network, and VAEs have it as the outside.</p><p    ></p>
            </figcaption>
       </section>





       <section id="slide-101">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-101" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0102.svg" class="slide-image" />

            <figcaption>
            <p    ></p>
            </figcaption>
       </section>





       <section id="slide-102">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-102" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0103.svg" class="slide-image" />

            <figcaption>
            <p    ></p>
            </figcaption>
       </section>





       <section id="slide-103">
            <a class="slide-link" href="https://mlvu.github.io/lecture09#slide-103" title="Link to this slide.">link here</a>
            <img src="51.DeepLearning2.key-stage-0104.svg" class="slide-image" />

            <figcaption>
            <p    ></p>
            </figcaption>
       </section>


</article>
