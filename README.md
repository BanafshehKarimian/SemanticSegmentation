# SemanticSegmentation
The dataset we use is Camvid: <br />
https://s3.amazonaws.com/fast-ai-imagelocal/camvid.tgz<br />
http://mi.eng.cam.ac.uk/research/projects/VideoRec/CamVid/data/LabeledApproved_full.zip<br />
We implement SegNet Base from its paper: https://arxiv.org/abs/1505.07293<br />
The architecture of the SegNet is:<br />
![SegNet arch](https://www.derinogrenme.com/wp-content/uploads/2015/12/segnet.png)<br />
SegNet has 13 encoder (Convoultional layer with kernel 7x7 and stride 1 followed by ReLU and maxpooling downsampling with kernel 2x2 and stride 2)/decoder (Upsampling with saved edge features and Convolutional leyer with kernel 7x7 and stride 1) layers and the output of the last layer is given to a softmax in order to produce a probability of each class for each pixle. The 2x2 maxpooling has the stride of 2, the loss function is cross entropy and SGD with fixed lr of 0.1 and momentum of 0.9 is used to train the network. Unlike Segnet, SegNet base uses only 4 encoder/decoder layers. <br />
Class N1 learns weights of the middle encoder decoder set. Class N2 freezes the learned weights from N1 and trains the third endoer with the second decoder. class N3 freezes the learned weights from N2 and trains the second endoer with the third decoder. Class N4 freezes the learned weights from N3 and trains the first endoer with the last decoder. <br />
The mentioned method, which is used in the paper, is time consuming, so we use NT that trains all 4 encoder/decoder paires at the same time.<br />
results without batch normalization:<br />
![results without batch normalization](https://github.com/BanafshehKarimian/SemanticSegmentation/blob/main/1.png)<br />
results with batch normalization:<br />
![results with batch normalization](https://github.com/BanafshehKarimian/SemanticSegmentation/blob/main/2.png)<br />
