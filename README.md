# Lit2Vec


(In progress, will be updating over the next week)

Using the Cbow version of the Word2Vec algorithm on Goodreads data, vectors were trained to represent books. 

This repository includes the Google Colab notebooks used to clean the original goodreads data, train the book vectors, and analyze the vectors. 

These notebooks requires the 'ratings.csv' and the 'books.csv' files which are described here

http://fastml.com/goodbooks-10k-a-new-dataset-for-book-recommendations/

and can be found here

https://github.com/zygmuntz/goodbooks-10k

These notebooks are set up to download these files from your Google Drive, and will ask permission to access your Google Drive. So if you would like to use these notebooks as is, download the files from the link above, and upload them to your Google Drive. 

The following images are from a single 2D TNSE plot of the resulting book embeddings. This particular TNSE plotted 3000 books (out of 10,000 book vectors that were trained)

This section contains fantasty/high fantasy written within the last 30-40 years. 

![alt text](Images/Book2VecSample1.JPG)

The secton in the middle has mostly comic books with sci books sourrounding it. Near the bottom is Neil Gaiman's graphic novel series Sandman. 

![alt text](Images/Book2VecSample2.JPG)

The books at the top is a Neil Gaiman's section. I'm not familiar with the other books but they seem to have an element of Neil Gaiman's style of paranormal/magic/sci-fi with a humorous style. 

![alt text](Images/Book2VecSample4.JPG)

This section has space-focused sci-fi. There's a small section of Chuck Palahniuk books to the right. 

![alt text](Images/Book2VecSample3.JPG)

Pre-20th century classics which seem to be grouped by time-period and author. 

![alt text](Images/Book2VecSample5.JPG)

The top right is having a Stephan King party and the bottom left side is having a Michael Crichton party. Perhaps they're grouped together because their books have a thrilling / horror quality. The Dark Tower books which have more of a fantasy quality are placed on the opposite side of Michael Crichton books. 

![alt text](Images/Book2VecSample6.JPG)

Classic childrens' books. The majority of the ones on the bottom left are picture books. Roald Dahl has his own section on the top right. Paddington and Winnie the Pooh seem to enjoy each other's company. Actually, the bottom sourrounding section has mostly animal main characters. 

![alt text](Images/Book2VecSample7.JPG)

Top right has some classic plays. To the bottom left of that, there seems to be writings that tend to be cited as having significant cultural influence (Utopia, The Communist Manifesto, The Republic, The Prince, The Art of War). Further left are more classics. At the left there's a section for Kurt Vonnegut books. At the bottom there are many early to mid 20th century classics. On the right there's a section of books by Charlotte Brontë and Jane Austen.

![alt text](Images/Book2VecSample8.JPG)

Lots of classic non-picture childrens books on the left side. Lord of the Rings and CS Lewis books on the right. 

![alt text](Images/Book2VecSample9.JPG)

This section has modern (written in the 90's to current) childrens books series. A Series of Unfortunate Events. Harry Potter, Artemis Fowl, Alex Rider, Inkworld, Inheritance Cycle, etc. 

![alt text](Images/Book2VecSample10.JPG)

These books all seem to have informational themes. This section has the most fascinating trends to me. I still haven't fully interpreted these trends but here are the ones I noticed so far. 

The top right seem to be focused on relationship informaion, and below that are books focused on financial, career,  and organizational success (Think and Grow Rich, The 7 Habits of Highly Effective People, etc).  Elon Musk's biography is in that section, which seems to be a favorite of Silicon Valley tech start-up people. The the books on the middle right are productivity themed, (The 4-hour workweek, Flow: The Psycology of Optimal Experience ). 

The books in the middle have more narrative elements: Walter Issacson books, Michael Lewis books, Deliverying Happyness. To the right of that are books about startups. The bottom left has books on food and plant life. 

The middle right is focused on art-based informational books. 

![alt text](Images/Book2VecSample11.JPG)

This section continues the informational trend above, themes more focused on history. 

![alt text](Images/Book2VecSample13.JPG)

This picture continues the historical trend above. The right side tends to have historical ficion books. The middle is focused on American history. 

![alt text](Images/Book2VecSample15.JPG)

This section is focused on comedy, particularly by those working in television industry.  

![alt text](Images/Book2VecSample12.JPG)

A young adult section, the right side is focused on dystopia and paranormal elements, the left side is more realist. 

![alt text](Images/Book2VecSample14.JPG)

These section tends to have books with female main characters. 

![alt text](Images/Book2VecSample16.JPG)

Full map of the 3000 vector TNSE. You'll have to zoom in real close to make out the text. It might be easier to download the picture. 

I'll make more for the other 7000 vectors but Google Colab seems to be only able to handle 3000-3500 vectors, even on GPU mode (GPU mode doesn't seem to make a difference though), so I'll probably have to make 2 or 3 more maps. 

![alt text](Images/Book2Vec0-3000New.jpg)

The following images show examples of the book vectors' similiarity properties. Similiarity was measured via dot product. 

![alt-text-1](Images/sim1.JPG) 

![alt-text-2](Images/sim2.JPG)

![alt text](Images/sim3.JPG) 

![alt text](Images/sim4.JPG)

![alt text](Images/sim5.JPG) 

![alt text](Images/sim6.JPG)

![alt text](Images/sim7.JPG)

The following images show some of the arithmetic properties of the book vectors. Although these properties are not as robust as word vectors' arithmetic properties, I hope to improve these with better hyperparameter optimization and more data. But in the meanwhile, here are some of the more interesting results I found. 

Vampire Classic - Vampire = Classics

![alt text](Images/va1.JPG)

Twilight Graphic Novel - Twilight + Coraline = Coraline Graphic Novel (in top 2 vectors returned)

![alt text](Images/va2.JPG)

Winnie-The-Pooh + Eastern Philosophy =  Pooh Eastern Philosophy

![alt text](Images/va3.JPG)

Romance Classic - Classic = Romance 

![alt text](Images/va4.JPG)

Neil Gaiman Childrens' - Neil Gaiman = Childrens'

![alt text](Images/va5.JPG)

Vampire Romance - Vampire = Romance

![alt text](Images/va6.JPG)

Takeaways (Stuff for other Machine Learning fans)

-Smaller Batch Sizes

Smaller batch sizes (32 and 64) durng training are very important to making sure robust similiarity properties for all book vectors. At higher batch sizes (128, 256, and 512) most of the vectors had decent similiarity properties but there always seemed to be a few books whose vectors did not have decent similiarity properties (based purely on my domain knowledge of the data, aka knowing which books should be most similiar to certain books). 

In the case of Harry Potter books 2-7, from looking directly at the data, I knew that the most similiar books to these should be other Harry Potter books in the series, but this was not the case, even after 100 epoches. However, when I switched to batch size 64, the similiarty properties for Harry Potter books 2-7 improved significantly after only a few epoches. This is demonstracted in the gif below (you probably have to tinker with the notebooks to know what's going on ). 

![alt text](Images/HarryPotterSmallBatch.gif)

https://gfycat.com/InfamousGrippingDeinonychus

https://giant.gfycat.com/InfamousGrippingDeinonychus.webm


I am not 100% sure what this is so, but this is my best guess:

Since the average window size is 112 and varies from 20 to 200 (depending on how many books a user has read), there was high probability that a particular book in a series like Harry Potter would get paired other books instead of Harry Potter. Say that there were 7 books in the series and the user had rated all 7 of them, and this user has also rated 112 other books; the probability of a Harry Potter book being paired with another Harry Potter book as a label for that user is 6/112. In this case, I theorized that maybe higher batch sizes would hinder the optimization more significantly than an application of the word2vec algorithm for a small and constant window size since word2vec is trying to optimize many embeddings at once. 

-Softmax Embeddings for Vector Arithmetic

So far, all the vector arithmetic examples above are cases where I performing the addition and/or subtraction on the book input embeddings, and then performing similiarity on the resulting vector against the softmax embeddings. The results were much more robust than comparing the resulting vector to the input embeddings. 

