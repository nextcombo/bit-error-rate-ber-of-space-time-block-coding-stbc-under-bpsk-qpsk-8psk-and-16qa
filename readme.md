# Bit Error Rate (BER) of Space-Time Block Coding (STBC) under BPSK, QPSK, 8PSK, and 16QAM modulations [with MATLAB code]

clear; \nclc; \nk = 1; %Modulation method 1-BPSK, 2-QPSK, 3-8PSK, 4-16QAM \nnSyms = 2100; % Generate a symbolic number \nnTx = 2; % Number of transmit antennas\nnRx = 1; % Number of receiving antennas % Bitrate Alamouti coding is 1, G3 and G4 are 1/2, H3 and H4 are 3/4, see stbc.m\nnPackage = 100; % Iterations \nSNR_dB = 0:2:20; \nSNR_lin = 10.^(SNR_dB/10); \nMod_style = {'BPSK','QPSK','8PSK','16QAM'}; \nfor SNR_i = 1:length(SNR_dB)\n    fprintf('SNR is %d db.\n',SNR_dB(SNR_i)); \n    for package_count = 1:nPackage\n        Bits = randi([0 1],1,nSyms*k); \n        [Syms Gmap] = modulation(k,Bits); \n        [x Frame] = stbc(Syms,nTx,rate); \n        [Index_de Frame_de] = stbc_de(x,Frame,nTx,nRx,Gmap,SNR_lin,SNR_i,rate); \n        data_de = dec2bin(Index_de-1,k); \n        Bits_de=reshape((double(data_de)-48).',1,[]); \n        nError_s(package_count) = sum(sum(Frame~=Frame_de)); \n        nError_b(package_count) = sum(Bits~=Bits_de); \n    end\n    SER(SNR_i) = sum(nError_s)/(nPackage*nSyms); \n    BER(SNR_i) = sum(nError_b)/(nPackage*nSyms*k); \n    BER_theroy(SNR_i) = get_BER_theroy(k,nTx,nRx,SNR_lin(SNR_i),rate); \n    \nend\nfigure; \nsemilogy(SNR_dB,BER,'*r'); \ntitle([num2str(nTx),' × ',num2str(nRx),', ',Mod_style{k}]); \nhold on; \nsemilogy(SNR_dB,BER_theroy,'bo--'); \nhold on; \nlegend('Simulation Value','Theoretical Value'); \nylabel('BER'); \nxlabel('SNR(dB)'); \ngrid on; \n    \n
MATLAB simulation results

## Images

![Error rate of space-time block coding (STBC) under BPSK, QPSK, 8PSK, and 16QAM modulations [with MATLAB code]](01.jpg)
![Error rate of space-time block coding (STBC) under BPSK, QPSK, 8PSK, and 16QAM modulations [with MATLAB code]](02.jpg)
![Error rate of space-time block coding (STBC) under BPSK, QPSK, 8PSK, and 16QAM modulations [with MATLAB code]](03.jpg)
![Error rate of space-time block coding (STBC) under BPSK, QPSK, 8PSK, and 16QAM modulations [with MATLAB code]](04.jpg)
![Error rate of space-time block coding (STBC) under BPSK, QPSK, 8PSK, and 16QAM modulations [with MATLAB code]](05.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
