import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import yfinance as yf #pip install yfinance
%matplotlib inline

ticker_list = ['AMZN', 'TSLA'] #add the name of brand
period = '100d' #decide how long days of stock data are imported

len_ticker = len(ticker_list)
hist_list = []

plt.figure(figsize = (10, 50))
plt.subplots_adjust(wspace = 0.3, hspace = 0.3)  

for i in ticker_list:
    temp_list = yf.Ticker(i).history(period=period)
    
    MACD = pd.DataFrame()
    MACD['Close'] = temp_list['Close']
    MACD['EMA_12'] = temp_list['Close'].ewm(span = 12).mean()
    MACD['EMA_26'] = temp_list['Close'].ewm(span = 26).mean()
    MACD['MACD'] = MACD['EMA_12'] - MACD['EMA_26']
    MACD['SIGNAL'] = MACD['MACD'].ewm(span = 9).mean()
   
    plt.subplot(len_ticker * 2, 2, 1 + 2 * ticker_list.index(i))
    plt.plot(MACD['Close'], label = 'stock', color = 'k') #left figure shows 'Close' values
    plt.title('Stock chart of ' + i)
    plt.legend(loc = 'best')

    plt.subplot(len_ticker * 2, 2, 2 + 2 * ticker_list.index(i))
    plt.plot(MACD['MACD'], label = 'MACD', color = 'r')
    plt.plot(MACD['SIGNAL'], label = 'SIGNAL', color = 'g') #right figure shows MACD and SIGNAL
    plt.title('MACD and SIGNAL of ' + i)
    plt.legend(loc = 'best')
    plt.grid(True)
