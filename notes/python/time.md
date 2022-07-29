# Time & Datetime

- unix timestamp to datetime:
  - `datetime_obj = datetime.fromtimestamp(unix_ts)`
- datetime to unix timestamp:
  - `unix_ts = datetime_obj.timestamp()`
- Format a datetime object:
  - `datetime_obj.strftime("%Y-%m-%d-%H-%M-%S")`