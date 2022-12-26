# nsetools (National Stock Exchange)

### Introduction

It is a Library that works without any setup requirement, used for collecting/extracting real-time data from National Stock Exchange (India).

### Installation and Upgrade

```python
>>> pip install nsetools    # to install nsetools

>>> pip install nsetools --upgrade   # to upgrade existing nsetools
```

### Usage with examples

In this section, we will see usage and cover all APIs that nsetools offers.

```python
>>> from nsetools import Nse
>>> nse = Nse()
>>> nse
```

```python
# a quotation is an agreed fixed price in nse
>>> a = nse.get_quote('infy')     # infy is stock code for INFOSYS
>>> a

Output:-
'css_status_desc': 'Listed',
 'dayHigh': 1509.0,
 'basePrice': 1497.1,
 'securityVar': 10.6,
 'pricebandlower': 1347.4,
 'sellQuantity5': 115.0,
 'sellQuantity4': 89.0,
 'sellQuantity3': 1.0,
 'cm_adj_high_dt': '17-JAN-22',
 'sellQuantity2': 1475.0,
 'dayLow': 1496.35,
 'sellQuantity1': 1.0,
 'quantityTraded': None,
 'pChange': 0.39,
 'totalTradedValue': 42159.7,
 'deliveryToTradedQuantity': None,
 'totalBuyQuantity': 284483.0,
 'averagePrice': 1503.51,
 'indexVar': None,
 'cm_ffm': 548050.21,
 'purpose': 'INTERIM DIVIDEND - RS 16.50 PER SHARE',
 'buyPrice2': 1502.75,
 'secDate': None,
 'buyPrice1': 1502.9,
 'high52': 1953.9,
 'previousClose': 1497.1,
 'ndEndDate': None,
 'low52': 1355.0,
 'buyPrice4': 1502.6,
 'buyPrice3': 1502.65,
 'recordDate': '28-OCT-22',
 'deliveryQuantity': None,
 'buyPrice5': 1502.55,
 'priceBand': 'No Band',
 'extremeLossMargin': 3.5,
 'cm_adj_low_dt': '26-SEP-22',
 'varMargin': 10.6,
 'sellPrice1': 1502.95,
 'sellPrice2': 1503.0,
 'totalTradedVolume': 2804085.0,
 'sellPrice3': 1503.35,
 'sellPrice4': 1503.4,
 'sellPrice5': 1503.55,
 'change': 5.9,
 'surv_indicator': None,
 'ndStartDate': None,
 'buyQuantity4': 83.0,
 'isExDateFlag': False,
 'buyQuantity3': 16.0,
 'buyQuantity2': 69.0,
 'buyQuantity1': 98.0,
 'series': 'EQ',
 'faceValue': 5.0,
 'buyQuantity5': 87.0,
 'closePrice': 0.0,
 'open': 1500.5,
 'isinCode': 'INE009A01021',
 'lastPrice': 1503.0}
```

```python
>>> nse.is_valid_code('infy')
Output:- True
 
>>> nse.is_valid_code('INFY')
Output:- True

# it means we can write stock code as uppercase or lowercase 
```

```python
# stock index, is a statistical measure that reflects changes taking place in the market
>>> list1 = nse.get_index_list() # to get whole list of index
>>> list1

Output:-
['NIFTY 50 Pre Open',
 'NIFTY 50',
 'NIFTY NEXT 50',
 'NIFTY100 LIQ 15',
 'NIFTY BANK',
 'INDIA VIX',
 'NIFTY 100',
 'NIFTY 500',
 'NIFTY MIDCAP 100',
 'NIFTY MIDCAP 50',
 'NIFTY INFRA',
 'NIFTY REALTY',
 'NIFTY ENERGY',
 'NIFTY FMCG',
 'NIFTY MNC',
 'NIFTY PHARMA',
 'NIFTY PSE',
 'NIFTY PSU BANK',
 'NIFTY SERV SECTOR',
 'NIFTY IT',
 'NIFTY SMLCAP 100',
 'NIFTY 200',
 'NIFTY AUTO',
 'NIFTY MEDIA',
 'NIFTY METAL',
 'NIFTY DIV OPPS 50',
 'NIFTY COMMODITIES',
 'NIFTY CONSUMPTION',
 'NIFTY CPSE',
 'NIFTY FIN SERVICE',
 'NIFTY GROWSECT 15',
 'NIFTY50 VALUE 20',
 'NIFTY50 TR 2X LEV',
 'NIFTY50 PR 2X LEV',
 'NIFTY50 TR 1X INV',
 'NIFTY50 PR 1X INV',
 'NIFTY ALPHA 50',
 'NIFTY50 EQL WGT',
 'NIFTY100 EQL WGT',
 'NIFTY100 LOWVOL30',
 'NIFTY MID LIQ 15',
 'NIFTY PVT BANK',
 'NIFTY100 QUALTY30',
 'NIFTY GS 8 13YR',
 'NIFTY GS 10YR',
 'NIFTY GS 10YR CLN',
 'NIFTY GS 4 8YR',
 'NIFTY GS 11 15YR',
 'NIFTY GS 15YRPLUS',
 'NIFTY GS COMPSITE',
 'NIFTY MIDCAP 150',
 'NIFTY SMLCAP 50',
 'NIFTY SMLCAP 250',
 'NIFTY MIDSML 400',
 'NIFTY200 QUALTY30']
```

```python
>>> nif_phrma_quote  = nse.get_index_quote("NIFTY PHARMA") # choose anyone from above list and put in 'get_index_quote' to get its stock quote
>>> nif_phrma_quote

Output:-
{'name': 'NIFTY PHARMA',
 'lastPrice': 12687.15,
 'change': '-97.30',
 'pChange': '-0.76',
 'imgFileName': 'NIFTY_PHARMA_open.png'}
```

```python
>>> All_StockCodes = nse.get_stock_codes()
>>> All_StockCodes

Output:- # here I am showing few output of get_stock_code......
'DHAMPURSUG': 'Dhampur Sugar Mills Limited',
 'DHANBANK': 'Dhanlaxmi Bank Limited',
 'DHANI': 'Dhani Services Limited',
 'DHANUKA': 'Dhanuka Agritech Limited',
 'DHARMAJ': 'Dharmaj Crop Guard Limited',
 'DHARSUGAR': 'Dharani Sugars&Chemicals Limited',
 'DHRUV': 'Dhruv Consultancy Services Limited',
 'DHUNINV': 'Dhunseri Investments Limited',
 'DIAMONDYD': 'Prataap Snacks Limited',
 'DICIND': 'DIC India Limited',
 'DIGISPICE': 'DiGiSPICE Technologies Limited,
..............................
```

```python
>>> advance_dec = nse.get_advances_declines()  #it shows number of rising stocks, falling stocks and unchanged stocks in a given trading day, per index.
>>> advance_dec

Output:- # here I am showing few output of get_advance_declines......
{'indice': 'NIFTY50 VALUE 20',
  'advances': 20.0,
  'declines': 0.0,
  'unchanged': 0.0},
 {'indice': 'NIFTY100 QUALTY30',
  'advances': 27.0,
  'declines': 3.0,
  'unchanged': 0.0},
 {'indice': 'NIFTY PVT BANK',
  'advances': 9.0,
  'declines': 1.0,
  'unchanged': 0.0},
 {'indice': 'NIFTY MID LIQ 15',
  'advances': 14.0,
  'declines': 1.0,
  'unchanged': 0.0},
.............
```

```python
>>> gainers = nse.get_top_gainers() # It shows list of top gaining stocks for the last trading session
>>> gainers

Output:- # here I am showing few output of get_top_gainers......
{'symbol': 'BAJAJFINSV',
  'series': 'EQ',
  'openPrice': 1496.9,
  'highPrice': 1539.95,
  'lowPrice': 1483.15,
  'ltp': 1532.45,
  'previousPrice': 1497.05,
  'netPrice': 2.36,
  'tradedQuantity': 916203.0,
  'turnoverInLakhs': 13866.55,
  'lastCorpAnnouncementDate': '13-Sep-2022',
  'lastCorpAnnouncement': 'Face Value Split (Sub-Division) - From Rs 5/- Per Share To Re 1/- Per Share'},
............................
```

```python
>>> losers = nse.get_top_losers() # It shows list of top losing stocks for the last trading session
>>> losers

Output:- # here I am showing few output of get_top_losers......
{'symbol': 'TATACONSUM',
  'series': 'EQ',
  'openPrice': 779.0,
  'highPrice': 783.7,
  'lowPrice': 773.0,
  'ltp': 775.0,
  'previousPrice': 779.0,
  'netPrice': '-0.51',
  'tradedQuantity': 669092.0,
  'turnoverInLakhs': 5197.77,
  'lastCorpAnnouncementDate': '09-Jun-2022',
  'lastCorpAnnouncement': 'Annual General Meeting/Dividend - Rs  6.05 Per Share'},
...............
```

### Thank You....