# Logging

- `basicConfig` can only be called once (configures root logger)
  - `logging.basicConfig(filename='app.log', filemode='w', format='%(name)s - %(levelname)s - %(message)s')`
- Msg formatting: 
  - example msg: `root - INFO - this is a logged msg`
  - default formating: `ERROR:root:This is an error message`
  - [All attributes that can be used in a format](https://docs.python.org/3/library/logging.html#logrecord-attributes)
  - useful format: `%(asctime)s - %(module)s - %(funcName)s - %(lineno)d - %(levelname)s - %(message)s` 
  - Can also include process id or process name same as with thread id and thread name to increase visibility into concurrent programs

## Logs from External Packages

- Assuming they use python logging package
- Will default to whatever level is set by root
- Can do more specific things with the logs from external packages like below:

```python
# for azure.identity pkg
logger = logging.getLogger('azure.identity')
logger.setLevel(logging.DEBUG)
handler = logging.FileHandler(filename=f'test.log')
# or for logging to a stream: handler = logging.StreamHandler(stream=sys.stdout)
logger.addHandler(handler)
```

