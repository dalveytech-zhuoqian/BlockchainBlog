数据
```js
[{'stock_id': 1023266, 'weight': 0.96, 'segment_name': 'ETF', 'segment_id': 8685442, 'stock_name': '银华日利ETF', 'stock_symbol': 'SH511880', 'segment_color': '#e84e24', 'proactive': False, 'volume': 0.06202537, 'textname': 'undefined(SH511880)', 'url': '/S/SH511880'}, {'stock_id': 1001892, 'weight': 99.04, 'segment_name': '商贸零售', 'segment_id': 14196553, 'stock_name': '人人乐', 'stock_symbol': 'SZ002336', 'segment_color': '#0055aa', 'proactive': False, 'volume': 39.30171686, 'textname': 'undefined(SZ002336)', 'url': '/S/SZ002336'}]
```
代码
```python
hlds = hlds.strip()
hlds = eval(hlds)
hlds = json.dumps(hlds)
hlds = json.loads(hlds)
for item in hlds:
    if int(item['weight']) > 40:
      pass
```
