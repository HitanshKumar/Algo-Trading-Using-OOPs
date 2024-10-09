
# 🔸Index Trading With Object Oriented Programing 🔸

OBJECTIVE:

➡️ To create a script that implements a moving average strategy using Object-Oriented Programming (OOP).

➡️ OOP will allow us to backtest any instrument for the moving average strategy without changing the code.

➡️ Any modification, such as changing the moving average window parameter, can be easily tweaked.

✨ For the purpose of this project, we will be using Nifty data and analyzing it with the help of the quantstats library.



## Class Functions📜

Following are the imp code snipits⬇️

1️⃣ This code initiates the class 'backtesting' and show the proper format to call the functions in the class⤵️
```bash
class backtesting:
    def __init__(self, ticker, start, end):
        self.ticker = ticker
        self.start = start
        self.end = end

        self.get_data()
        self.indicators()
        self.positions()
        self.analysis()
```
2️⃣ Computing the positions column⤵️
```bash
  def positions(self):
        self.df['positions'] = np.where(self.df['Close'] > self.df['Close'].shift(1), 1, 0)
        self.df['positions'] = self.df['positions'].shift(1)
        self.df['strategy_returns'] = self.df['positions'] * self.df['simple_returns']
        self.df['simple_returns'] = self.df['simple_returns'] + 1
        self.df['strategy_returns'] = self.df['strategy_returns'] + 1

```
3️⃣ Doing the final analysis using the qantsats library⤵️
```bash
  def analysis(self):
        self.df[['simple_returns', 'strategy_returns']].cumprod().plot(grid=True)
        print('simple returns were:', self.df['simple_returns'].cumprod()[-1] - 1)
        print('strategy returns were:', self.df['strategy_returns'].cumprod()[-1] - 1)
        
        qs.reports.basic(self.df['strategy_returns'])
```

## Conclusion🎯

- Object Oriented Programing and the very idea of using 'Class method' in python is very ideal to code any trading strategy because it makes it much more easier to backtest it on any instrument and any modifications to the code can be made very easily

- This project aimed to demonstrate how to do the same for a very basic strategy such as the moving average
