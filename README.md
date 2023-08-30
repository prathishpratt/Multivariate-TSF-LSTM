Series Forecasting with LSTM

### Includes a benchmarking of MacBook's M1 CPU vs. GPU 


@author: Prathish Murugan

- dataset: https://finance.yahoo.com/quote/GE/history/

<pre>
  From GE's historical price, we take a sliding window of 14 days and 5 features to predict the 
  next day's opening price.

  We have used LSTM as it is important to preserve the sequence in this use case. 
  
  So the input shape will be (x, 14, 5). That is for every row, we will have a (14,5) matrix as input.
  
  Also, Standard Scaling has been used for the 5 columns and then inverse transformed back 
  after the prediction.
</pre>
![Prediction of one day](https://github.com/prathishpratt/Multivariate-TSF-LSTM/assets/64516584/7ea8b9df-9e19-40fc-8285-28da941f8314)
<pre>
  We can only predict one day after the data, since it is multivariate, if we need to 
  predict the next following days we need to predict all the 5 inputs.
  
</pre>


### Benchmarking

## Benchmarking
#### CPU
<pre>
- CPU | Batch size = 16   | loss: 0.0103 - val_loss: 5.1876e-04 | Time Taken to fit = 25s 
- CPU | Batch size = 512  | loss: 0.0089 - val_loss: 5.1310e-04 | Time Taken to fit = 9s
- CPU | Batch size = 1024 | loss: 0.0090 - val_loss: 4.9307e-04 | Time Taken to fit = 8s
- CPU | Batch size = 4096 | loss: 0.0558 - val_loss: 0.0046     | Time Taken to fit = 2s
</pre>
**In CPU even though batch = 4096 was quicker, it has more loss than 1024, which is the most optimal.**

#### M1 GPU
<pre>
- GPU | Batch size = 16   | loss: 6.1139e-04 - val_loss: 0.0021 | Time Taken to fit = 1 min 22s 
- GPU | Batch size = 512  | loss: 0.0134 - val_loss: 0.0022     | Time Taken to fit = 4s
- GPU | Batch size = 1024 | loss: 0.0157 - val_loss: 0.0042     | Time Taken to fit = 4s
- GPU | Batch size = 4096 | loss: 0.0313 - val_loss: 0.0064     | Time Taken to fit = 3s
</pre>
**Same in GPU as CPU, even though batch = 4096 was quicker, it has more loss than 1024, which is the most optimal.**

<img width="1137" alt="M1 performance" src="https://github.com/prathishpratt/Multivariate-TSF-LSTM/assets/64516584/66219077-3c5c-47f8-bf53-1a18126229a9">

