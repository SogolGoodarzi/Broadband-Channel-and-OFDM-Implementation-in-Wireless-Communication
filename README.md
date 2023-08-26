# Broadband-Channel-and-OFDM-Implementation-in-Wireless-Communication
<p align="justify"> Suppose, the channel is frequency selective or in other words broadband. Therefore, the received signal at moment k in the discrete domain (after sampling) is as follows: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/7cd2b8b6-b0ac-4878-9429-9c7b05f002ac)

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/3c59a08f-c2b3-4a28-9256-21052b97f2b4)

Let 𝐿 be the total number of channel taps. In this case, relation (1) is simplified as the following relation:

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/980a017b-5d15-45b7-b0bf-1d74969405cd)

<p align="justify"> Suppose channel bandwidth W = 20MHz, channel coherence time $T_c$ = 5ms and channel delay spread equals to $T_d = 10\micro s$ . We want to send a message of length $N=10^8$ bits in this channel to the receiver. Design an OFDM system to send this message. Let $n_c$ be the number of subcarriers, cp is the length of the cyclic prefix. Message bits randomly (are produced with probability $1/2$ to be zero and with probability $1/2$ to be 1). Assume the modulation is BPSK. Assume that the taps of the channel vary little during a time interval of length $T_c$ and assume constant for simplicity. </p>

### The number of taps of the channel (L):
<p align="justify">  The bandwidth of the channel is 20MHz. Also, the extent of channel delay, i.e. the time it takes for the effect of each input in the channel to disappear, is $10\micro s$ . According to these explanations, the number of taps will be obtained as follows: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/5e012568-f038-4de7-9043-8af99df216f7)

### The length of the circular prefix (cp):
The length of cp that we apply to make the signal alternate and circular convolution to be converted to linear convolution, is obtained from the following relationship:

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/0c989d8b-dc53-4af4-9d96-2bd1c5157d3c)

<p align="justify"> To determine the number of subcarriers in OFDM blocks, we have two upper and lower limits. To determine the upper limit of this parameter, it should be noted that the OFDM channel must remain constant during block transmission. Or in other words, it is Time Invariant. According to the definition that we had for the channel coherence time (it is the period of time after which the channel will change if it passes, or at least the time in which the frequency response of the channel will be independent of its current frequency response), the upper limit of $n_c$ will be obtained as follows: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/623eb5d8-1a98-4200-9b1f-4c64d7ba4ab7)

<p align="justify"> The more the number of subcarriers is taken from this value, the more variable the channel will be with time. On the other hand, if the value of $n_c$ is considered too small, then the sending rate will decrease. So, the number of subcarriers must be more than the number of cp, as a result. </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/8cd16c99-37da-4da6-8d58-279394daa9e1)

To get the number of OFDM blocks, we must divide the number of generated bits by the number of subcarriers. In this case we will have:

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/8a99b703-cd02-43eb-826f-224f0ea370c2)

The block diagram of the OFDM system receiver and transmitter when we use waterfilling in the transmitter will be as follows.

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/d0703e16-945e-41a0-a1cf-adac78ccc286)

#### Waterfilling:
<p align="justify"> The explanation of this block is given in the case of a problem, but in general, it can be said that by using this block, we can fix the low or high value of $H_k$ of the channel. According to the definition we had for this block in the lesson, it is actually similar to filling a water container and its name is also derived from this concept. That is, if we have the frequency response of the channel i.e. H, then if the coefficients that this block multiplies in its input are taken as the opposite of the frequency response of the channel ( $1/H_{k}$ ), then the channel effect will later be targeted in the receiver and the output signals will be detected. So, the ultimate goal of this block is to target the channel effect and eliminate the effects of high or low $H_k$ on the channel output. </p>

#### IFFT:
<p align="justify"> As it was said in the course material, the process of reaching the IFFFT block in the transmitter was that we intended to mount the input signal on the carrier signals and send it. Using the written mathematical relations, we saw that we finally reached the concept of IFFT. As a result, it can be said that the general purpose of placing this block in the transmitter is to place the message signal on the subcarriers and send them. </p>

#### FFT:
<p align="justify"> After receiving IFFT in the transmitter, each data of the input signal is mounted on one of the subcarriers. According to the course material, these subcarriers are sinks that are located in such a way that their intersection point with other subcarriers is at zero, and also at the frequency where the peak of one of these sinks occurs, the rest of the sinks have negligible values, as a result, in order to receive Correct data in the frequency domain, we must sample at certain points. Finally, in order to convert the received data from the frequency domain to the time domain, we take FFT and the output signal values ​​in the time domain will be accessible in this way. </p>

#### cp and cp removal:
<p align="justify"> Adding cp, as it was said before, is to alternate the input signal so that when it is taken with the convolution channel, it becomes circular convolution. In this case, if we take the Fourier transform from the circular convolution, it will be converted to multiplication, but the normal convolution will not necessarily be converted to multiplication in the frequency domain. As a result, targeting this block is like this. Also, with a series of new data added at the beginning of the input signal, we will naturally see the outputs corresponding to these data on the receiver side. As a result, to target these extra data, we put the cp removal block so that the length of the output signal is proportional to its corresponding input and the unnecessary extra data is removed from the output signal. </p>

* <p align="justify"> Instead of the Waterfilling method, use the diversity method at the location in the receiver to compensate for fading in the receiver (the power of each subcarrier is $P_{max}/n_c$ ). Suppose we have 10 antennas in the receiver and the distance between these antennas is big enough. Use the MRC method in the receiver and plot the error probability diagram as versus $SNR = P_{max}/(N_0 * n_c)$ . For this section, we must simulate the following block diagram: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/f885e634-fd1f-4b67-badd-3412494d7e13)

<p align="justify"> According to the above block diagram and textbooks, in order to implement MRC, we must pass the x input signal through 10 channel branches with different coefficients. In this case, for every 10 branches, we must finally remove cp and take FFT and finally multiply by $H^{*}$ , which are actually the cophasing coefficients for the MRC block. Finally, to get the same error as before, we compare each bit of the matrix 𝑍 with the input matrix 𝑎, which was the production bits, and get the probability of error. The error probability diagram plotted for this section is as follows: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/c07a271e-549e-4f49-88e1-acceb440c0b5)

* <p align="justify"> Instead of the diversity method in the previous part, use the equalization method in the receiver with the ZF and MMSE criteria. For each of these two criteria, simulate the system and obtain the error probability diagram. </p>

### ZF Equalizer:
<p align="justify"> To implement this block, it is similar to the previous sections, with the difference that when we reach the equalizer block, the $W_k$ coefficients that are multiplied at the input of this block in order to remove the channel effect are equal to $W_k = 1/H_k$ . This coefficient will be multiplied both in the sentence $H.X$ and in the noise $W$ . Finally, we compare the output vector $Z$ with the input vector $a$, similar to the previous cases, and plot the probability of error. </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/e1acc56b-999d-4517-a4ea-d6d4477ce414)

### MMSE Equalizer:
To implement this equalizer, we act similar to ZF, with the difference that the coefficients of this equalizer are obtained from the following equation:

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/f05ffe75-a933-4949-898b-dff82e26eb1a)

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/5b172461-8b4d-4ce9-8c0a-f9e7a83ddcbf)

Finally, the error probability diagrams of these two systems are shown in the figure below:

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/05c5d430-8765-48df-8cfa-1a456a350fbc)

<p align="justify"> As it is clear, the graphs do not differ much, but according to the course material, we expected that at high SNRs such as $\sigma_{n}^2/\sigma_{s}^2$ , due to its high SNR, the SNR will be much lower and we can ignore it, the performance of the two equalizers will be almost the same at these points. In this case we have: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/52dc8edc-3d3f-4b3b-b471-1e9344949623)

<p align="justify"> In the previous part, suppose that the clipping effect occurs in the output of IFFT to the extent of $0.8 max(|X_{k}|)$ . plot the error probability diagram in terms of $SNR = P_{max}/(N_0 * n_c)$ . (Use the MMSE criterion). </p>

<p align="justify"> For this section, after applying the IFFT block on the transmitter side, we perform the clipping operation by determining the output. For this purpose, we set the portions of the output signal of the IFFT block that have a value greater than the specified threshold equal to the same threshold. The continuation of the system process is the same as before and no additional code is needed for these sections. In the following, the graphs of two system states with clipping and without clipping are plotted as follows: </p>

![image](https://github.com/SogolGoodarzi/Broadband-Channel-in-Wireless-Communication/assets/125180530/9809a38b-9fd6-4000-ae68-6d66f3b31a2f)
