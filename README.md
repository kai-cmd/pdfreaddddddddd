#part 1


Automatic Identification of Braille Blocks by Neural Network

Using Multi-Channel Pressure Sensor Array

Koichi Kuzume∗

Haruko Masuda

Yudai Murakami

Information Engineering Department, Information Engineering Department,

Department of Human Intelligence

Systems, Graduate School of Life

Sciences and Systems Engineering,

Kyushu Institute of Technology, Japan

National Institute of Technology,

Yuge College, Japan

National Institute of Technology,

Yuge College, Japan

ABSTRACT

Pressure Sensor Array. In 2020 The 3rd International Conference on Com-

putational Intelligence and Intelligent Systems (CIIS 2020), November 13–15,

2020, Tokyo, Japan. ACM, New York, NY, USA, [7](#br7)[ ](#br7)pages. [https://doi.org/10.](https://doi.org/10.1145/3440840.3440858)

[1145/3440840.3440858](https://doi.org/10.1145/3440840.3440858)

In recent years, the number of visually impaired people in Japan

has exceeded 300,000 including those with low vision, and acci-

dental falls on the station platform involving them have not been

eliminated. Persons having acquired visual impairment make up

one third of all cases of blindness in Japan. It is known that they

often cannot walk alone with only a white cane or guide dog. The

main cause of platform accidents was misidentiﬁcation of braille

blocks. Therefore, it was necessary to develop an auxiliary device

for accurately identifying braille blocks that the acquired visually

impaired could also use easily. In this research, we developed an au-

tomatic identiﬁcation system for braille blocks using foot pressure

data acquired by a multi-channel pressure sensor array. First, we

devised a new foot pressure data acquisition device using a multi-

channel pressure sensor array. Our proposed device had excellent

features such as being light weight, low cost, and easy to extend to

multi-channel. Second, in order to accurately identify the braille

blocks, the foot pressure data acquired under various conditions

was learned by neural network, and identiﬁcation performance

evaluated. As a result of the experiment, the braille blocks could

be identiﬁed with a high rate of at least 98% accuracy by neural

network, with a very simple structure of an input layer (16 neurons),

a hidden layer (5 neurons), and an output layer (4 neurons).

1

INTRODUCTION

At present, the number of visually impaired people in Japan is

over 300,000 including those with low vision. Acquired visually

impaired persons make up one third of all blind persons in Japan.

The main causes ofꢀacquired blindness are eye diseases such as

diabetic retinopathy, glaucoma and cataract to which elderly peo-

ple are prone. It is known that they often cannot walk alone with

only a white cane or guide dog. In the future, with the super aging

of society, the number of visually impaired people will increase

more and more [[1](#br6), [2](#br6)]. Accidents involving the visually impaired

are continuously increasing. According to a survey of the statistics

of accidents involving them on station platforms conducted by the

Ministry of Land, Infrastructure, Transport and Tourism between

2010 and 2017 [[3](#br6)], during this period 15 train accidents involving

them occurred, 10 of which were fatal. In addition, the number of

accidents involving visually impaired persons falling to the station

platform reached 605. Many deaths involving them have occurred

since 2017. The main cause of these accidents was the misidentiﬁca-

tion of braille blocks. Visually impaired people walk with the help

of information from braille blocks and a white cane. The following

are believed to be the causes of misidentiﬁcation of braille blocks

and accidents [\[4\].](#br6)

CCS CONCEPTS

• Information systems applications; • Data mining; • Cluster-

ing;

• Mental stress while walking in crowds.

•

Wear and tear of braille blocks or improper installation.

KEYWORDS

visually impaired people, identiﬁcation of braille block, foot pres-

sure sensors, Neural Network

• Since most visually impaired are adventitious disabled, there

are individual diﬀerences in the ability to identify braille

blocks.

ACM Reference Format:

Therefore, in recent years, with the increase of visually impaired

people, varied research and development to support their walking

has been actively undertaken. Existing walking support technolo-

gies include some systems using ultrasonic waves, such as the “Moat

Sensor” and “Sonic Guide” [[5](#br6)–[7](#br6)]. These systems emit ultrasonic

waves to the walking environment to measure the distance between

obstacles and a visually impaired person, and notify the disabled

person with the periphery information. However, these systems

cannot demonstrate suﬃcient performance in places where crowd-

ing is prone to occur, such as in a station yard, because pedestrians

block ultrasonic waves. Other systems using cameras have similar

drawbacks and are less practical [\[8](#br6)]. In addition, novel technology

that embeds an RFID or magnet in the braille blocks and reads the

information using a sensor mounted in a white cane for walking

Koichi Kuzume, Haruko Masuda, and Yudai Murakami. 2020. Automatic

Identiﬁcation of Braille Blocks by Neural Network Using Multi-Channel

∗Corresponding Author: kuzume@info.yuge.ac.jp.

Permission to make digital or hard copies of all or part of this work for personal or

classroom use is granted without fee provided that copies are not made or distributed

for proﬁt or commercial advantage and that copies bear this notice and the full citation

on the ﬁrst page. Copyrights for components of this work owned by others than ACM

must be honored. Abstracting with credit is permitted. To copy otherwise, or republish,

to post on servers or to redistribute to lists, requires prior speciﬁc permission and/or a

fee. Request permissions from permissions@acm.org.

CIIS 2020, November 13–15, 2020, Tokyo, Japan

© 2020 Association for Computing Machinery.

ACM ISBN 978-1-4503-8808-5/20/11...$15.00

<https://doi.org/10.1145/3440840.3440858>

93





CIIS 2020, November 13–15, 2020, Tokyo, Japan

Koichi Kuzume et al.

Figure 1: Structure of the foot pressure sensor array.

Table 2: Structure of neural network and learning condition

category to be identiﬁed

Number of neurons in

input layer

8 or 16

4

Number of neurons in

output layer

Number of hidden layer

Number of neurons in

hidden layer

1

5

Training set

70%

15%

15%

Validation set

Test set

to the entire sole of the foot. This device enables us to identify their

moving state, such as walking, running, standing still and going up

or down stairs. However, since it is impossible to identify the shape

of a road surface, it cannot be used for identifying the type of braille

blocks. Y. Ohashi et.al. tried to classify the braille blocks by template

matching using HoG (Histogram of Oriented Gradients) features on

the measured foot pressure data. 32-ch foot pressure sensors were

used. However, the average classiﬁcation rate was 78.2%, which

was not so high. Moreover, as the classiﬁcation rate depended on

a user’s walking style, it was necessary to prepare a template for

each user in advance [[12](#br7)]. Another attempted to identify using

the maximum lateral pressure value for each step during walking

[[13](#br7)]. In that study, when the center of gravity moved from the heel

to the toe during walking, the identiﬁcation was performed using

machine learning using the maximum value of each channel. That

system used 208-channel foot pressure sensors and was expensive.

The objective of our research was to develop an automatic braille

block identiﬁcation system which acquired visually impaired per-

sons could also use easily without extra large-scale infrastructure

[[14](#br7)]. To realize the proposed system, we devised a 16-ch foot pres-

sure sensor array and applied a Neural Network as a classiﬁer of the

braille blocks to improve the identiﬁcation performance. This paper

is organized as follows: Section 2 is devoted to the design of the

Figure 2: Characteristics of foot pressure versus output volt-

age in case of 8-ch sensor array.

Table 1: Category to be identiﬁed

Category

Category to be identiﬁed

1

2

3

Nothing to step on

Stepping on the ﬂat ﬂoor

Stepping on the

guidance braille blocks

Stepping on the warning

braille blocks

4

support was proposed [[9](#br6)–[11](#br7)]. However, these assistive technologies

have not been widely used because of the necessity of large-scale

infrastructure and high cost.

There are several examples of research using foot pressure in-

formation similar to our research. One is a device to estimate the

walking state based on the magnitude of the foot pressure and pat-

tern of the activated sensors by pressure-sensitive sensors attached

94





Automatic Identification of Braille Blocks by Neural Network Using Multi-Channel Pressure Sensor Array

CIIS 2020, November 13–15, 2020, Tokyo, Japan

Figure 3: Three positions of pressure sensor attachment (toe, center and heel) and CH positions.

foot pressure sensor and describing its characteristics. In Section 3,

we detail experiments with acquisition of foot pressure data and

evaluate the identiﬁcation performance of braille blocks by neural

network. We discuss the experimental result and realization for

practical use by using FPGA chip in Section 4. Section 5 concludes

the paper and mentions future works.

2

FOOT PRESSURE SENSOR ARRAY

2\.1 Design of the foot pressure sensor

The foot pressure sensor used had a pressure-sensitive sheet with

the characteristic that the resistance value changed depending on

pressure applied in the Z-axis direction. The sheet was a conductive

microﬁber non-woven produced by Eeony Corp [[15](#br7)]. The pressure-

sensitive sheets were cut to a size of 10 × 10 mm[2](#br7)[ ](#br7)and fabricated at

an interval of 10 mm to reduce interference between each sensor,

and then the conductive yarn was sewn crosswise on the fore and

back side of the sheets to ﬁx. As a result of the cross point area

at which the conductive yarn crossed, it could form a pressure-

sensitive sensor. By sewing the pressure-sensitive sensors could be

realized. Figure [1(](#br2)a) shows the structure of the pressure-sensitive

sensor cell, and [a](#br2)[ ](#br2)16-channel in a lattice pattern (4 × 4) shown in

Figure [1](#br2)[ ](#br2)(b) could be realized. Figure [1(](#br2)a) shows the structure of

the pr[essur](#br2)e-sensitive sensor cell, [and](#br2)[ ](#br2)a 16-chnnel sensor array

is shown in Figure [1](#br2)[ ](#br2)(b). Foot pressure data was acquired using

an Arduino micro[computer](#br2)[ ](#br2)board equipped with a micro SD card

shield. The pressure sensors could be formed at each intersection

area of the conductive yarn and were controlled by a matrix circuit

using analog switches. The time-division scanning method of all

sensors was used to reduce the number of inputs to an ADC with

10bits. The prototype system could acquire the foot pressure data

for about 3000 steps under the conditions of a sampling frequency

of 150 [Hz] and 16-channel.

Figure 4: Flat ﬂoor, warning and guiding braille blocks,

which we intended to identify in our laboratory.

2\.2 Electronic characteristics of the foot

pressure sensor array

Figure [2](#br2)[ ](#br2)shows the relationship between output voltage and mea-

sured [fo](#br2)ot pressure by an 8-channel sensor array when the user

took one step on a warning block. Each output voltage from the

sensor was calibrated because an oﬀset voltage was generated even

while no pressure was applied.

Figure 5: Calculated result of ROC depending upon attach-

ment position of the sensor array (in the case of heel posi-

ton).

95





CIIS 2020, November 13–15, 2020, Tokyo, Japan

Koichi Kuzume et al.

Table 3: Evaluation result of the identiﬁcation performance depending on sampling frequency

Attaching position

Heel

Category

Sensitivity [%]

Precision [%]

Overallꢀperformanceꢀ[%]

1

2

3

4

1

2

3

4

1

2

3

4

99\.5

96\.1

94\.7

91\.4

98\.8

87\.3

79\.1

81\.5

98\.5

86\.3

77\.8

61\.3

100

96\.8

94\.8

91\.4

100

91\.3

91\.7

63\.8

100

94\.4

91\.0

88\.0

Center

Toe

94\.3

79\.1

45\.3

3

EXPERIMENT AND EVALUATION

array gotten by the confusion matrix. The position with the highest

identiﬁcation performance was the heel.

3\.1 Identiﬁcation performance of braille

blocks by neural network

3\.2.2 Sampling frequency. We compared the identiﬁcation perfor-

mance when the sampling frequencies for acquiring foot pressure

data were 50 [Hz] and 150 [Hz] (see Table [4).](#br5)[ ](#br5)The overall identiﬁca-

tion rate at 50 [Hz] was 92.4%, and 94.4% [at](#br5)[ ](#br5)150[Hz] respectively.

The higher the sampling frequency, the higher the identiﬁcation

performance was. There was no signiﬁcant diﬀerence in overall

identiﬁcation performance between the two cases. However, the

identiﬁcation performance of warning blocks degraded at 50[Hz].

The identiﬁcation performance of machine learning using neural

network was evaluated by ROC (Receiver Operating Characteris-

tics) and confusion matrix. The neural network tool we used in this

research was Deep Learning Toolbox operated on MATLAB ver.

R19b.

3\.2 Data acquisition conditions for machine

learning

3\.2.3 Number of sensor ccannels. Table [5](#br5)[ ](#br5)shows the evaluation

results of the identiﬁcation performance [in](#br5)[ ](#br5)the case of 8 and 16-

channel. The overall identiﬁcation performance was 94.4% for 8-

channel, and 97.1% for 16-channel. The identiﬁcation performance

was improved as the number of channels increased. Since the

amount of hardware of our system was proportional to the number

of channels and it required more time to infer the classiﬁcation of

braille blocks, we needed to ﬁx the appropriate number of channels

without degradation of performance.

In order to realize the mobile device which was embedded in our

system, it was necessary to minimize the amount of hardware for

inferring the type of braille blocks in real time. Then, the identiﬁca-

tion performance was evaluated under the diﬀerent data acquisition

conditions such as attachment position of the sensor array, sampling

frequency, the number of sensor channels and optimal structure of

neural network.

3\.2.1 Braille block identification performance depending on atacch

ment position of tce foot pressure sensor array. First, the diﬀerence

in identiﬁcation performance depended on the position where the

sensor array was attached. As shown in Figure [3,](#br3)[ ](#br3)a foot pressure

sensor array with 8-channel was attached at [the](#br3)[ ](#br3)following three

positions: toe, center and heel. Foot pressure at each position was

then measured. Foot pressure data was measured when stepping on

mock braille blocks paved on the ﬂoor in the laboratory. It included

300 steps for each of the three states of stepping on a ﬂat ﬂoor, the

guidance block and the warning block (See Table [1](#br2)[ ](#br2)and Figure [4).](#br3)

Measurements were taken at each of the three p[ositions](#br2)[ ](#br2)[with](#br3)[ ](#br3)[a](#br3)

sampling frequency of 150[Hz]. After learning with the obtained

foot pressure data by neural network under the conditions shown

in Table [2,](#br2)[ ](#br2)an experiment for identifying the type of braille blocks

was p[erforme](#br2)d. Figure [5](#br3)[ ](#br3)shows the ROC in the case of attaching

the sensor array to the [he](#br3)el. The AUC (Area under the curve) was

larger than 0.8. Table [3](#br4)[ ](#br4)shows the evaluation result of the identi-

ﬁcation accuracy dep[ending](#br4)[ ](#br4)on attachment position of the sensor

3\.2.4 Optimal structure of neural network. To realize a mobile de-

vice embedded with the ability for identiﬁcation of braille blocks, it

was necessary to reduce the amount of hardware as much as possi-

ble. We examined how the identiﬁcation performance depended on

the structure of the neural network. Setting the number of input

layers, hidden layers and output layers to only one layer, the num-

ber of neurons in the hidden layer was varied from 1 to 10. The

identiﬁcation performance was then evaluated. Figure [6](#br5)[ ](#br5)shows the

identiﬁcation accuracy was saturated with over 5 [neurons.](#br5)

3\.2.5 Field test. We walked on the braille blocks paved around the

train station to evaluate the identiﬁcation performance of braille

blocks. Figure [7](#br6)[ ](#br6)shows a picture of an experiment in the ﬁeld and

the result ofꢀ[the](#br6)[ ](#br6)confusion matrix. It was 97.1% for inside experi-

ments and 98.8% for ﬁeld experiments and a deterioration of the

identiﬁcation performance was not observed (see Table [6).](#br5)

96





Automatic Identification of Braille Blocks by Neural Network Using Multi-Channel Pressure Sensor Array

CIIS 2020, November 13–15, 2020, Tokyo, Japan

Table 4: Valuation result of the identiﬁcation performance depending on sampling frequency

Sampling Frequency [Hz]

50

Category

Sensitivity [%]

Precision [%]

Overallꢀperformanceꢀ[%]

1

2

3

4

1

2

3

4

98\.3

93\.3

89\.0

89\.4

99\.5

96\.1

94\.7

92\.2

100\.0

96\.7

92\.0

79\.4

100\.0

96\.8

94\.8

91\.4

92\.4

150

94\.4

Table 5: Evaluation result of the identiﬁcation performance in case of 8 and 16-channel

Number of channels

8ch

Category

Sensitivity [%]

Precision [%]

Overallꢀperformanceꢀ[%]

1

2

3

4

1

2

3

4

99\.5

96\.1

94\.7

91\.4

99\.7

98\.8

96\.5

96\.2

100\.0

96\.8

94\.8

91\.4

100\.0

99\.1

96\.9

95\.6

94\.4

16ch

97\.1

Table 6: Evaluation result of the identiﬁcation performance in the ﬁeld.

Predicted class of braille blocks

Real class

of braille

blocks

Accuracy 98.8 [%]

1

1508

0

2

56

3

73

4

16

Sensitivity [%]

1

91\.2

98\.6

99\.0

99\.2

2

8408

66

84

37

3

0

22680

99

98\.9

175

17595

98\.8

4

0

100

38

98\.1

Precisionꢀ[%]

4

DISCUSSION

In general, a recurrent neural network has been used for machine

learning of time-series data. However, in our system, high identiﬁ-

cation performance could be realized with a very simple structure

that used only the correlation between foot-pressure data of each

channel for machine learning. The ﬁnal goal of our research is to

develop the braille blocks identiﬁcation system by neural network

using the multi-channel pressure sensor array shown in Figure [8.](#br6)

This system consists of the following four functions: Foot pr[es-](#br6)

sure data acquisition, machine learning of acquired data by cloud

computer, download of the learned-weighted coeﬃcients from the

cloud to an inference chip and the notiﬁcation of the information to

support walking for visually impaired persons. The inference chip

will be realized using an FPGA (Field Programmable Gate Array)

or a microcomputer. As the inference chip contains an input layer

with 16 input channels and a hidden-layer with ﬁve neurons and

an output-layer with four outputs, it can be constructed by 100

multipliers. The inference operation can be processed in parallel

Figure 6: Characteristic of identiﬁcation performance de-

pending on the number of neurons in a hidden layer.

97





CIIS 2020, November 13–15, 2020, Tokyo, Japan

Koichi Kuzume et al.

Figure 7: Picture of experiment in the ﬁeld.

for higher identiﬁcation of braille blocks. We then estimated the

amount of hardware to realize our system. The number of multi-

pliers contained in the inference chip was estimated at about 100.

Therefore, it is expected to execute identiﬁcation processing for

braille blocks in real time. In the future, we will construct the com-

plete system for visually impaired persons by an FPGA and cloud

technology. We will then evaluate performance and usability with

the help of the visually impaired, including those with acquired

blindness.

ACKNOWLEDGMENTS

This work was supported by JSPS KAKENHI Grant Number

19K12886.

Figure 8: Working support system for disabled persons us-

ing a multi-channel pressure sensor array.

REFERENCES

[1] J. Fujisaku, R. Koda and K. Nakazato. 2014. Research on psychological diﬃculties

on using a white cane by people with visual impairment, Bulletin of Tokyo

University and Graduate School of Social Welfare, 105-114.

using an FPGA chip. As a result, the proposed system could pro-

vide eﬀective information for the visually impaired to assist with

walking in real time.

[2] K. Tsubota, T. Awa, K. Suruga 2017. Divergence on the use of white cane among

adventitiously blinded persons: focusing on the signiﬁcant other in their life

courses. Transactions of JASVET. vol.33, No.1,1-10.

5

CONCLUSION AND FUTURE WORKS

[3] Ministry of Land, Infrastructure. 2014.Transport and Tourism, Japan. [http://www.](http://www.mlit.go.jp/common/001251591.pdf)

[mlit.go.jp/common/001251591.pdf](http://www.mlit.go.jp/common/001251591.pdf).

[4] [M.](http://www.mlit.go.jp/common/001251591.pdf)[ ](http://www.mlit.go.jp/common/001251591.pdf)[Ohkura,](http://www.mlit.go.jp/common/001251591.pdf)[ ](http://www.mlit.go.jp/common/001251591.pdf)[M.](http://www.mlit.go.jp/common/001251591.pdf)[ ](http://www.mlit.go.jp/common/001251591.pdf)[Shimizu,](http://www.mlit.go.jp/common/001251591.pdf)[ ](http://www.mlit.go.jp/common/001251591.pdf)[M.](http://www.mlit.go.jp/common/001251591.pdf)[ ](http://www.mlit.go.jp/common/001251591.pdf)[Tauchi,](http://www.mlit.go.jp/common/001251591.pdf)[ ](http://www.mlit.go.jp/common/001251591.pdf)T. Murakami. Science of orientation and mo-

bility of persons with visually impairment toward safe and reliable independent

travel. 69-77.

[5] [http://www.gdp-](http://www.gdp)[ ](http://www.gdp)search.com.au/minig\_1.htm#IMPORT\_M.

[6] [Larisa](http://www.gdp)[ ](http://www.gdp)[Dunai,](http://www.gdp)[ ](http://www.gdp)[Ismael](http://www.gdp)[ ](http://www.gdp)Lengua, Ignacio Tortajada, Fernando Brusola Simon. 2014

.Obstacle detectors for visually impaired people. in Proc. International Conference

on Optimization of Electrical and Electronic Equipment. IEEE, 809-816.

[7] N. Ortigosa Araque, L. Dunai, G. Peris Fajarnes, V. Santiago Praderas, I. Dunai.

2009\. Sound map generation for a prototype blind mobility system using multiple

sensors. ABLETECH’08 Conference.

[8] N. Tanaka, M. Okudaira. 2009. A study on image processing for action assis-

tance of visually impaired humans using a camera equipped cellular phone.

Technical Report of The Institute of Image Information and Television Engi-

neers,Vol.33,Issue 6, 173-176.,

[9] Mohsin Murad, Abdullah Rahman, Arif Ali Shah, et.al. 2011. An RFID based

navigation and object recognition assistant for visually impaired people”, Proc.

of 7th International Conference on Emerging Technologies, IEEE.

In this research, we proposed the braille block identiﬁcation system

that could support walking for the visually impaired. The proposed

system enabled visually impaired persons to get information on

the type of braille blocks by attaching a pressure sensor array on

their sole and using a neural network as a classiﬁer.

The merit of our system was that it did not require new infras-

tructure and had inexpensive and highly accurate identiﬁcation

capability. Acquired visual impaired persons who do not use a white

cane or guide dog can also utilize it. Under various conditions, such

as attachment position of the sensor array and sampling frequency,

the number of sensor cells and structure of the neural network,

the identiﬁcation performance was evaluated by ROC and confu-

sion matrix. We could derive the best data acquisition condition

98





Automatic Identification of Braille Blocks by Neural Network Using Multi-Channel Pressure Sensor Array

CIIS 2020, November 13–15, 2020, Tokyo, Japan

[10] Hernandez, Vitor Filipea, Paulo Costac, João Barrosoa. 2013. Location based ser-

vices for the blind supported by RFID technology”, 5th International Conference

on Software Development and Technologies for Enhancing Accessibility and

Fighting Info-exclusion, DSAI.

(Information Processing Society of Japan).

[13] H. Horie, T. Mitsuda, S. Kawamura. 2006. An algorithm for estimating walk-

ing types using foot-pressure sensors. Transactions of the Japanese Society for

Medical and Biological Engineering: BME 44(4), 621-627.

[11] Sakmongkon Chumkamon, Peranitti Tuvaphanthaphiphat, Phongsak Keerati-

wintakorn. 2008. A blind navigation system using RFID for indoor environments.

Proc. of 5th International Conference on Electrical Engineering/Electronics, com-

puter, telecommunications and Information Technology,Vol.2.

[14] Y. Murakami, K.Kuzume. 2019. Automatic identiﬁcation of braille blocks by using

machine learning. Proc. the Shikoku-Section Joint Convention of the Institutes

of Electrical and Related Engineers.

[15] [http://eeonyx.com/product_category/emi-stealth/.](http://eeonyx.com/product_category/emi-stealth/)

[12] Y. Ohashi, Y. Enokibori, K. Masei. 2013. Identiﬁcation of the road surface context

using the maximum pressure selection when walking. IPSJ SIG Technical Report

99


#part2


2022 IEEE International Conference on Pervasive Computing and Communications Workshops and other Affiliated

Events (PerCom Workshops): Work in Progress

Inference System for Automatic Identification of

Braille Blocks Using a Pressure Sensor Array

Koichi Kuzume

*Dep. of Information Engineering*

*National Institute of Technology,*

*Yuge college*

Yoshitugu Watanabe

*Advanced Course of Production*

*Engineering*

*National Institute of Technology,*

*Yuge college*

Haruko Masuda

*Dep. of Information Engineering*

*National Institute of Technology,*

*Yuge college*

Tomonari Masuzaki

*Dep. of Information Engineering*

*National Institute of Technology,*

*Yuge college*

Kamijima-cho, Japan

Kamijima-cho, Japan

Kamijima-cho, Japan

kuzume@info.yuge.ac.jp

Kamijima-cho, Japan

haruko@info.yuge.ac.jp

t\_masuzaki@info.yuge.ac.jp

ap20009@yuge.kosen-ac.jp

***Abstract* — Visually impaired people usually use braille blocks**

**as guidance marks when walking outside. Therefore, detecting the**

**braille blocks accurately is very important for them to walk safely.**

**In our previous research we proposed a novel system for**

**recognizing braille blocks, mainly in an outdoor setting, using not**

**only the information from a white cane but also a pressure sensor**

**array to realize the braille block more accurately. Moreover, we**

**showed our system could be constructed using a Neural Network**

**with an extremely simple structure. In this research we developed**

**an inference system for automatic identification of braille blocks**

**based on the previous research results. The system consisted of a**

**16-channel foot pressure sensor array, a microcomputer and a**

**cloud system, which respectively detected the difference in**

**pressure pattern depending upon the type of braille block, made**

**inferences about the kinds of braille blocks and implemented**

**machine learning. We made a prototype system and confirmed**

**that the system could infer the kinds of braille blocks with high**

**accuracy in real-time.**

proposed and reviewed to meet the needs of the visually

impaired [3]. Some systems used a CCD camera [4-6]. Toshiaki

Okamoto et.al. proposed a novel method for detecting braille

block by using a camera and Convolutional Neural Network

(CNN). In their experiment, they confirmed that the test

accuracy was approximately 94%. However, they couldn’t

demonstrate sufficient performance in places prone to crowding,

such station yards, because pedestrians blocked the view ahead.

Other novel technology that involved embedding an RFID or

magnet in braille blocks and reading the information using a

sensor mounted in a white cane for walking support was

proposed [7-9]. In addition, Fukuda et.al. proposed light-

emitting textured paving block by using LED to support the

mobility for the weak eyesight people [10]. This block had

extremely long-life emission by the battery. However, these

assistive technologies were not widely used because of the

necessity of large-scale infrastructure and high cost. There were

several examples of research using foot pressure information.

One was a device to estimate the walking state based on the

magnitude of the foot pressure and pattern of the activated

sensors by pressure-sensitive sensors attached to the entire sole

[11]. This device was to identify the moving states, such as

walking, running, standing. Since it was impossible to identify

the shape of a road surface, it couldn’t be used for identifying

the type of braille blocks. Y. Ohashi et.al. tried to classify the

braille blocks by template matching using the Histogram of

Oriented Gradients features of the measured foot pressure data.

32-ch foot pressure sensors were used [12]. However, the

average classification accuracy was 78.2%, which was not

particularly high.

***Index Terms — inference, braille block, machine learning,***

***identification, pressure sensor array***

I. INTRODUCTION

According to statistics reported by the World Health

Organization, approximately 253 million people in the world are

visually impaired, of which 217 million have slight vision and

36 million are blind [1]. There are more than 300,000 visually

impaired people living in Japan, of which about 60% acquired

visual impairment due to illness or injury [2]. As a result, many

people with acquired visual impairment have progressive eye

diseases in which their visual function gradually declines. It is

said that many people with visual impairments who have just

suffered a disability often find life inconvenient due to difficulty

moving and obtaining information, and tend to stay home. We

show the number of fall accidents on station platforms involving

visually impaired people from 2010 to 2019 in Figure 1 [2]. The

number of fall accidents is declining due to the installation of

platform doors, but fatal accidents still occurred every year.

There are various kinds of causes of fall accidents, and it is said

that the misrecognition of braille blocks is one of the principal

causes. Visually impaired people usually use braille blocks as

guidance marks when walking outside. Therefore detecting the

braille blocks accurately is very important for them to walk

safely. A wide range of walking support technologies have been

Fig. 1 The number of accidents in which visually impaired people fell from the

station platform and fatal accidents.

A9u7th8or-i1ze-6d6lic5e4ns-1ed64us7e-4lim/2ite2d/$to3:1D.a0li0an©Un2i0ve2rs2ityIEoEf TEechnology. Downlo4a6ded on April 01,2023 at 09:58:09 UTC from IEEE Xplore. Restrictions apply.





2022 IEEE International Conference on Pervasive Computing and Communications Workshops and other Affiliated

Events (PerCom Workshops): Work in Progress

In our previous research, we proposed a novel system that,

mainly when the visually impaired person was outside, in case

of recognizing the braille block, not only the information from

the white cane but also the pressure sensor array was used to

realize the braille block more accurately [13]. Our system had a

function to identify the type of braille blocks by machine

learning based on the difference in foot pressure pattern when

the user stepped on the braille block. In our previous research,

we confirmed that our system could be constructed by Neural

Network with an extremely simple structure that had an

identification accuracy of 95% or more by computer simulation

using MATLAB. The objective of our current research was to

develop an inference system for automatic identification of

braille blocks based on the previous research results, which

reduced false recognition and enhanced safety.

was not simple. Therefore, in this research we changed the

conductive thread to metal tape to shorten the

The remainder of this paper is divided into four sections.

Section II describes the outline of our inference system. Section

III presents the experimental method and results. Then we

describe the structure and characteristics of the foot pressure

sensor array and machine learning for braille block

identification. Identification of braille blocks by our inference

system is finally followed by our conclusions in Section IV.

Fig. 2 Schematic diagram of inference system for automatic identification of

braille blocks.

II. OUTLINE OF INFERENCE SYSTEM

*A. Construction of inference system for automatic*

*identification of braille blocks*

A schematic diagram of our system is shown in Figure 1. A 16-

ch pressure sensor array was attached to the sole, and the data

measured by walking on the braille block on flat ground.

Machine learning was executed after sending the collected data

to the cloud. The learned weighting coefficients were

downloaded to the inference chip. The type of braille blocks

was referenced in the chip. When the inference chip detected a

warning block it informed the user by voice or vibration.

Identification targets were of the following four types:

• Nothing to step on.

Fig. 3 Structure of sensor before and after improvements

production time and improve maintainability. A pressure-

sensitive sheet with an area of 10 x 10 mm2 was fabricated in a

lattice pattern (4x4). It was attached with copper metal tape in

between and soldered to the connector. The pressure sensors

could be formed at each intersection area of the conductive

copper tape and controlled by a matrix circuit using analog

switches. The time-division scanning method of all sensors was

used to reduce the number of inputs to an ADC with 10-bits.

The sensor array was protected by covering it with a thin

laminate film. Figure 3 shows the structure of the sensor before

and after the improvement. The pressure-sensitive sheet,

produced by Eeony Corp [14], was a conducting weave that’s

resistance value changed depending on the pressure applied in

the Z-axis.

• Stepping on flat ground.

• Stepping on a warning block.

• Stepping on a guidance block.

The inference chip was realized by a microcomputer, Raspberry

Pi.

*B. Improvement of 16-ch foot pressure sensor array*

The foot pressure sensor array was an important device that

determined the performance of the system. We required the

following conditions for the device:

• Fast response speed (real-time walking support for

III. EXPERIMENTAL METHOD AND RESULTS

users).

• Short time to make.

*A. Characteristics of foot pressure sensor array*

Figure 4 shows the 16-ch pressure sensor array which we made.

Figure 5 shows the relationship between the output voltage and

measured foot pressure by a 16-ch sensor array when the user

took one step on a warning block. Each output voltage from a

sensor cell was calibrated because an offset voltage was

generated even while no pressure was applied. Figure 6 shows

the pressure patterns of a foot pressure sensor array when the

user stepped on a flat floor, guiding braille block and warning

block respectively. Each pattern was dependent upon the type

• Inexpensive.

• High identification rate and low deviation in sensitivity.

• Easy maintenance (easy replacement of sensor in case of

failure).

In the previous research, we made a 16-ch pressure-sensitive

sensor array using a conductive thread and a pressure-sensitive

sheet, but making it took too much time and its maintenance

47

Authorized licensed use limited to: Dalian University of Technology. Downloaded on April 01,2023 at 09:58:09 UTC from IEEE Xplore. Restrictions apply.





2022 IEEE International Conference on Pervasive Computing and Communications Workshops and other Affiliated

Events (PerCom Workshops): Work in Progress

of braille block on which the user stepped. Then we learned the

difference in patterns by Neural Network.

*B. Machine learning for identifying braille blocks*

We used Raspberry Pi 4 as the inference chip and Python as the

development language for inference processing. A Neural

Network toolbox running on MATLAB was used for machine

learning. We display the learning conditions of the Neural

Network in Table I. The inference time for identification of the

braille blocks was 80 msec. The foot pressure data for inference

was normalized (Mini-Max Normalization). Figure 7 shows the

evaluation results of the identification performance by

MATLAB. The overall identification performance was 96.7%

or more.

Fig. 5 Characteristics of 16ch foot pressure versus voltage

*C. Identification of braille blocks by inference chip*

The weighting coefficients calculated by MATLAB were

written to the inference chip. Figure 8(a) and (b) show an

example of the experimental results of inference performance

while stepping on the warning braille block using the newly

developed pressure-sensitive sensor array mounted under a

leather shoe. The figures show that during the step transition

period there existed some erroneous inference, marked “\*” in

the graph. This was because the chip inferred the user stepped

on the guiding block even though stepping on the warning

braille block. To reduce such errors during the step transition

period, we adopted majority decision processing using the

results of 5 inferences. Figure 8 (b) shows that the errors

occurring during the transition period of the step change could

be reduced. Table 2 shows the evaluation results of inference

performance. The experiments were made under the following

conditions: The user stepped on a flat floor, guiding block and

warning block 500 times respectively and performance was

evaluated by counting the number of correct or incorrect

inferences.

Flat floor

Guidance

Warning

Fig.6 Pressure pattern depending on braille blocks

TABLE I.

STRUCTURE OF NN

AND LEARNING CONDITION

Number of neurons in input layer

16

8

Number of neurons in hidden layer

Number of neurons in output layer

Number of hidden layers

Training set

Structure of NN

4

1

70%

15%

15%

3000

80msec

Center

Validation set

Learning

conditions

Test set

Number of learning data

Inference time

Shoe attachment position

Raspberry Pi 4

IV.

CONCLUSIONS AND FUTURE WORKS

In this study, we developed an inference system for visually impaired

people to identify braille blocks. Our system consisted of three parts,

a foot pressure sensor, a microcomputer to acquire the pressure data,

and a cloud system for machine learning. First, we made a foot

pressure sensor array with high identification accuracy, low cost and

speed and ease of manufacture. We changed the structure of the sensor

Fig. 4 16-ch pressure sensor array and connect with Raspberry Pi 4

48

Authorized licensed use limited to: Dalian University of Technology. Downloaded on April 01,2023 at 09:58:09 UTC from IEEE Xplore. Restrictions apply.





2022 IEEE International Conference on Pervasive Computing and Communications Workshops and other Affiliated

Events (PerCom Workshops): Work in Progress

array from our previous research and devised a new method to shorten

make time by replacing the sensor part with copper tape. We evaluated

inference performance, confirming that our sensor array had an

identification performance of 97% or more. The newly developed

sensor was then attached to the back of leather shoes and the foot

pressure data measured to be learned and sent to a cloud system.

However, some inference errors occurred in the so-called transient

periods at the moment when the step was taken off and reached the

floor. We proposed a method, through majority decision processing, to

reduce such errors and confirmed that the errors could be greatly

reduced through its application. As a future task, we plan to execute

the following things mentioned below;

•

•

Improve the lifetime of the foot pressure sensor

Enable to execute both learning and inference processes in a

chip, not use the cloud.

•

Repeat experiments for practical use with the cooperation of

visually impaired people.

ACKNOWLEDGMENT

This work was supported by JSPS KAKENHI Grant Number

19K12886.

REFERENCES

[1] R.R.A.Bourne et.al., “Magnitude, temporal trends, and projection of the

global prevalence of blindness and distance and near vision impairment:

A systematic review and meta-analysis,” Lancet Global Health, vol.5,

no.9, pp. e888-e897. Sep. 2017.

[2] Ministry of Land, Infrastructure, Transport and Tourism, Japan.

http://www.mlit.go.jp/common/001251591.pdf.

[3] Md. Milon Islam et.al., “Developing walking assistants for visually

impaired people: A review,” IEEE Sensors J. vol.19, no.8, pp2568-2576,

April 15, 2019.

Fig.7 Evaluation of identification performance by MATLAB

[4] T.Okamoto et.al., “Braille block recognition using convolutional neural

network and guide for visually impaired people.” Pro. of the 29th

International Symposium on Industrial Electronics (ISIE) ,IEEE, 2020.

[5] J. Fujisaku, R. Koda and K. Nakazato, “Research on psychological

difﬁculties on using a white cane by people with visual impairment,”

*Bulletin of Tokyo University and Graduate School of Social Welfare*, pp.

105-114, 2014.

[6] N. Tanaka, M. Okudaira. 2009. A study on image processing for action

assistance of visually impaired humans using a camera equipped cellular

phone.

[7] Mohsin Murad, Abdullah Rahman, Arif Ali Shah, et.al, “An RFID based

navigation and object recognition assistant for visually impaired people”,

Proc. of 7th International Conference on Emerging Technologies, IEEE,

2011\.

[8] Sakmongkon Chumkamon, Peranitti Tuvaphanthaphiphat, Phongsak

Keeratiwintakorn, “A blind navigation system using RFID for indoor

environments, Proc. of 5th International Conference on Electrical

Engineering/Electronics, computer, telecommunications and Information

Technology, Vol. 2, 2008.

[9] K. Tsubota, T. Awa, K. Suruga, “Divergence on the use of white cane

among adventitiously blinded persons: focusing on the significant other

in their life courses,” Transactions of JASVET. vol. 33, No. 1, pp. 1-10,

2017\.

Fig.8 Experimental evaluation of identification performance

TABLE II.

INFERENCE PERFORMANCE BY MICROCOMPUTER CHIP

[10] Hiromi Fukuda et.al., “A study on the visibility of the light emitting

braille block”, International Conference on Human Centered Design, the

Lecture Notes in Computer Science book series (LNCS, volume 6776),

pp 295-303, 2011.

Nothing

to step

Warning

block

Guiding

block

MATLAB

Simulation

Flat floor

Nothing

to step

100%

0%

0%

92%

3%

0%

3%

0%

2%

98\.0%

98/6%

98\.4%

96\.7%

[11] H. Horie, T. Mitsuda, S. Kawamura, “An algorithm for estimating

walking types using foot-pressure sensors”, Transactions of the Japanese

Society for Medical and Biological Engineering: BME 44(4), pp. 621-627,

2006\.

[12] Y. Ohashi, Y. Enokibori, K. Masei, “Identification of the road surface

context using the maximum pressure selection when walking”, IPSJ SIG

Technical Report (Information Processing Society of Japan), 2013.

Flat floor

Warning

block

0%

94%

3%

3%

Guiding

block

0%

4%

95%

[13] K. Kuzume, et.al., “Automatic Identification of Braille Blocks by Neural

Network Using Multi-Channel Pressure Sensor Array”, The 3rd

International Conference on Computational Intelligence and Intelligent

Systems, pp. 93–99, November 2020.

Machine learning was performed by Neural Network on a cloud

system. The learned weight coefficients were written to

microcomputer, Raspberry Pi 4, to realize an inference chip. We

evaluated the identification performance of our inference chip and

confirmed that our system had high identification accuracy in real-time.

a

[14] http://eeonyx.com/product\_category/emi-stealth/.

49

Authorized licensed use limited to: Dalian University of Technology. Downloaded on April 01,2023 at 09:58:09 UTC from IEEE Xplore. Restrictions apply.

