# Open Sourcing the Origin Stories: The ml5.js Model and Data Provenance Project

Because machine learning algorithms automatically learn to complete tasks, it might be easy to forget that they are human-designed software imbued with the values of their creators. I researched the origins of ml5.js’ pre-trained models and the data they were trained on to help the ml5.js community learn more about the models for their projects. This article describes the research process, my findings, and how you can contribute to this ongoing work.

---

## Introduction
ml5.js (ml5) is an open source JavaScript code library that introduces machine learning (ML) to students, artists, and creative coders in friendly, approachable ways. ML, a type of artificial intelligence, refers to algorithms that find patterns in data, such as in a dataset of numbers, text, images, or even live video capture. Without being explicitly programmed, a ML algorithm learns parameters to represent or model those patterns, and the result is a trained model that uses those parameters to perform a specific task.

For example, Google’s [PoseNet](https://learn.ml5js.org/#/reference/posenet) model was trained on images of people to estimate key points on the human body. This is valuable for real-time motion capture of performers, who traditionally might wear bodysuits donned with sensors or markers and tracked with specialized, expensive hardware and software systems. Using PoseNet, which is free, the only equipment needed is a computer-connected camera pointed at a person or group of people. This opens up new avenues for experimentation and expression to a wider audience of creators as explored in [this collaboration](https://experiments.withgoogle.com/billtjonesai) between legendary choreographer and dancer, Bill T. Jones, and Google Creative Lab. 

ML models are created and shared by academic, corporate, and government researchers, as well as by students, artists, designers, and hobbyists. Pre-trained models, such as those available from ml5, result from numerous choices, including what training data to gather and how to architect the algorithms for specific use cases, and as such, a ML model will always favor some results over others. The Mozilla Foundation’s white paper, [Creating Trustworthy AI](https://foundation.mozilla.org/en/insights/trustworthy-ai-whitepaper/) (Ricks et al 2020), explains:

>Every dataset comes with its own set of biases, and it is impossible to build a fully unbiased AI system. Humans are biased, and every part of the research, collection, structuring, and labeling of data is shaped by human decisions. Bias is the result not just of unbalanced training data, sampling, and data availability, but it is also the product of systemic and methodological choices teams make when they are designing an AI system.

Bias is especially critical if a ML model discriminates against people, and examples have been well-documented from many different kinds of platforms, from [facial recognition](https://www.nytimes.com/2018/02/09/technology/facial-recognition-race-artificial-intelligence.html) to [language models](https://www.nytimes.com/2019/11/11/technology/artificial-intelligence-bias.html).

Efforts are being made to define AI principles to prevent harmful bias. These include recommendations to design ethical systems that are transparent in how they work, that produce fair and undiscriminating outcomes, and for which their designers can be held accountable. The Berkman Klein Center for Internet & Society at Harvard University surveyed public and private sector organizations and compiled a comprehensive list in [Principled Artificial Intelligence: Mapping Consensus in Ethical and Rights-based Approaches to Principles for AI](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3518482) (Fjeld et al 2020). The ml5 community also values these goals, and the beta version of the library was [announced in 2018](https://medium.com/ml5js/ml5-friendly-open-source-machine-learning-library-for-the-web-e802b5da3b2) with the “priority to be clear and transparent with where [each] model is sourced from, what data was used to train the model, and what data might be missing.” Since its start, ml5 contributors have created or ported many pre-trained models, including PoseNet, from different sources, but at the time of the official launch, background information for models and their training datasets varied in scope across the library.

In 2020 I started digging into their origins to fill in the gaps. For this project, sponsored in part by the [Clinic for Open Source Arts (COSA)](https://www.du.edu/ahss/opensourcearts/) at the University of Denver and the [Interactive Telecommunications Program (ITP)](https://tisch.nyu.edu/itp) at New York University, I developed a framework to research where the models and training datasets came from, who created them and how, and for what purposes. The results, published on [ml5’s models’ reference pages](https://learn.ml5js.org/#/reference/index), are intended to help ml5 users better understand how the models operate, including what bias might be expressed, as they evaluate them for their projects. 

Drawing from data ethics strategies in Catherine D'Ignazio and Lauren F. Klein’s [Data Feminism](https://mitpress.mit.edu/books/data-feminism), I aim to be transparent about my assumptions in my research process, including my methods and framing choices. I acknowledge that pulling these origin stories together is neither an objective process, nor should it be the work of one person. Comments and corrections that critically engage these contributions are welcome!

## Research Approach
The first step was to decide what information to collect about each model and its training data. A number of initiatives propose extensive frameworks for documentation. A few examples include [Model Cards for Model Reporting](https://arxiv.org/abs/1810.03993) (Mitchell et al 2018), [Datasheets for Datasets](https://arxiv.org/abs/1803.09010#) (Gebru et al 2018), and [The Partnership on AI’s ABOUT ML (Annotation and Benchmarking on Understanding and Transparency of Machine Learning Lifecycles)](https://www.partnershiponai.org/about-ml/) (started in 2019). The recommendations are considerably detailed and offer useful starting points, but since the ml5 website provides quickstart steps to learn ML, I worried that too much background information might overwhelm users.

Keeping in mind ml5’s beginner-friendly education goals, I developed a scaled-back approach inspired by the work of data scientist and statistician, [Heather Krause](https://twitter.com/datassist), who urges data journalists to write [data biographies](https://idatassist.com/data-biographies-how-to-get-to-know-your-data/) to answer the where, who, how, and why questions of data sources and collection methods. These echo the general categories of the above-mentioned frameworks, and informed by all of them, I crafted the following templates:

### Model Biography
- Description - **What** does this model do?
- Developer and Year - **Who** developed it and **when**?
- Purpose and Intended Users - **Why** was it developed and **for whom**?
- Hosted Location - **Where** does ml5.js retrieve the model files from?
- ml5 Contributor and Year - **Who** ported it to ml5 and when?
- References - What **sources** were consulted for this information?

### Data Biography
- Description - **What** are the data?
- Source - **Where** did it come from?
- Collector and Year - **Who** collected it and **when**?
- Collection Method - **How** was the data collected?
- Purpose and Intended Users - **Why** was the dataset developed and **for whom**?
- References - What **sources** were consulted for this information?

In keeping with the project’s goal of transparency, I included space for references, especially for those who wish to follow up and contribute in the future. Also, since ml5 aims to make complex topics approachable to novice practitioners, the technical mathematical equations of machine learning algorithms and their evaluation metrics (i.e. how each model was developed) were left out. However the curious can often find this information in the research papers linked in the models’ reference sections.

I looked for answers to the biography questions in several places, starting with the ml5 code repository. Every model was ported to the library from another location, and by reading the codebase history, I verified import dates and the names of contributors. Since ml5 is an open source project, multiple people might have developed a particular model to integrate it into the library with varying degrees of involvement, and I opted to credit those who made the initial contributions. For some models I found mentions and links to the original code repositories, but beyond the ml5 repository, I searched the Internet to track down information. My research was also informed by my personal knowledge of ml5’s development at New York University’s Interactive Telecommunications Program (ITP) at the Tisch School of the Arts, where I was a graduate student and research resident and where I am now currently teaching.

## Findings
During my research in 2020, I worked with sixteen different ML methods in the ml5 library, ranging from sound classification to human pose detection and from image style transfer to text generation. Some methods offered multiple pre-trained models. Some models were trained on the same datasets and some on multiple datasets, while others required users to supply their own data. In those cases, ml5 provided sample data to get started. In total, I researched the origins of twenty-five models and fourteen datasets. I answered all of the biography questions for fifteen models and partially completed the remaining ten with what I could dig up. Of the datasets, I fully-answered seven of the biographies but found limited answers for the additional eight.

Creators for both models and datasets were either from higher education institutions (38%), commercial entities (42%), individuals for whom I could not find any affiliation (18%), or completely unknown. Collaborations between academic and commercial researchers accounted for 16% of all cited creators, and the most frequently mentioned corporation was Google at 36%. It’s important to note here that ml5’s initial development was supported by a Google education grant (see [Shiffman et al 2018](https://medium.com/ml5js/ml5-friendly-open-source-machine-learning-library-for-the-web-e802b5da3b2) and also the [ml5 About page](https://ml5js.org/about/)).

In addition to organizational context, the documentation varied in the type and amount of content (what was there, including source citations), detail (the specificity of the information), and terminology (labels identifying key components). Some information I could not locate; in some cases because it was proprietary and not available.

An example of a well-documented model is SpeechCommands18w, which is the default option for using ml5’s [SoundClassifier](https://learn.ml5js.org/#/reference/sound-classifier) method. (The biographies are located at the end of its [ml5 reference page](https://learn.ml5js.org/#/reference/sound-classifier?id=model-and-data-provenance).) It was developed by Google’s Tensorflow.js team as part of the company’s open source ML platform for application developers. The model recognizes a limited vocabulary of simple English words (such as "yes", "no", "on", "off", "stop", and "go") and was trained on a dataset of individual word recordings. The audio files were crowdsourced from volunteer contributors to Google’s Open Speech Recording project with the intention of creating an open source speech dataset for more people to train their own speech recognition models. A [paper](https://arxiv.org/abs/1804.03209) written about the dataset further describes why English was selected as the language of collection, why specific words were chosen, how the collection process was managed, and how the recordings were processed and evaluated. All of this information, including the dataset itself, was readily available from a couple of Google websites.

[Provenance](https://learn.ml5js.org/#/reference/face-api?id=model-and-data-provenance) for the [Face-Api](https://learn.ml5js.org/#/reference/face-api) training datasets, however, was tricky to track down. Face-Api provides several pre-trained model options for different tasks, such as detecting and recognizing faces in images and videos. In contrast to Google’s SpeechCommands18w, these models were developed by an individual, [Vincent Mühler](https://medium.com/@muehler.v), affiliation unknown, for the JavaScript community to run facial detection models in web and mobile applications. Each model was trained on a dataset from different sources as mentioned in [documentation](https://github.com/justadudewhohacks/face-api.js#models-face-detection) by Mühler. Some models were trained on datasets for which I could not determine who collected the images, their collection methods, sources, overall composition, nor the originally-intended uses. Other datasets were trained on images generally described as retrieved from the Internet by university research teams using web crawlers and search engines.

Without this information it's hard to predict how models trained on these datasets express bias. For example, the Oxford University authors of the freely available [VGG-Face Dataset](https://www.robots.ox.ac.uk/~vgg/data/vgg_face/), which was used in part to train Face-Api’s FaceRecognitionModel, notes a word of caution: 

>We note that the distribution of identities in the VGG-Face dataset may not be representative of the global human population. Please be careful of unintended societal, gender, racial and other biases when training or deploying models trained on this data. 

Even if images were publicly available on the internet does not necessarily mean that they were collected under free distribution use licenses. (The VGG-Face creators note that their images are covered under the Creative Commons Attribution-NonCommercial 4.0 International license but are not directly available because they are subject to copyright.) Nor should we assume that those pictured granted permission for their likenesses to be collected for facial recognition technology. It is worth mentioning that VGG-Face research was funded by the United States Government’s Intelligence Advanced Research Projects Activity (IARPA) from the Office of the Director of National Intelligence (ODNI), which raises questions of intended use cases beyond providing this as a resource for academic research communities. (If you have information about the datasets used to train the models for Face-Api, please submit your contribution to the [Face-API reference page](https://learn.ml5js.org/#/reference/face-api). The steps are linked below.)

## Next Steps and How to Contribute
This research is just the start of telling these stories. My results were added to ml5’s website in the fall of 2020, but as I write this in 2021, it is possible that some provenance information is now out of date and reference links are broken. Maintaining these biographies requires monitoring and updating, as well as ensuring that new models are added to the library with provenance information.

For some models, we might never know the contents of the original dataset(s), the specifics of the algorithm design, nor how those engender bias. Sometimes the biography trails extended farther back than I reported. Some models were ported to ml5 from sources that were in turn ported from other places and so on. How far back to document without overwhelming the user with information was a recurring question. Some questions I might not have thought to ask in the first place.

Clearly there are many lingering questions, and so another goal of this project is to raise awareness about the uneven landscape of ML documentation in both its availability and transparency. Without documentation standards, how can all users of ML tools, from the novice to the experienced, identify and measure how model and data biases impact their projects?

For all these reasons, this documentation is ongoing work in progress, just like the rest of the library. The ml5 open source project welcomes participation from a diverse community of creators and learners with multiple perspectives. The library is available for all visitors to submit inquiries, changes, and additions, and now these biographies are part of the public conversation, too.

If you’d like to participate in this research, the instructions for contributing to the ml5 project are available on its Github repository at *[How to Contribute](https://github.com/ml5js/ml5-library/blob/main/CONTRIBUTING.md)*. If you’re new to working with the library or on Github and you’re not sure where to start, just click “Issues” at the top of the page and then, “New Issue,” to ask for help. As mentioned in the documentation for contributors, the “goal is to make ml5 as open and supportive as possible for those who want to be involved.” Hope to see you there!

---

[Ellen Nickles](https://ellen.town/) is an adjunct professor at New York University’s interactive media programs, [ITP/IMA/Low Res](https://tisch.nyu.edu/itp), at the Tisch School of the Arts.

Many thanks to [Carrie Sijia Wang](https://carriesijiawang.com) and [Alden Rivendale Jones](http://alden.website/) for editing this article.

