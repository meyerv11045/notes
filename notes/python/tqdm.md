# tqdm

- `from tqdm import tqdm`

## nested loops that look good

- `position=0` means its the first loop we see
- `leave=False` removes old progress bar once done

``` python
for i in tqdm(range(10), desc="outer", position=0):
  for j in tqdm(range(i), desc="inner", position=1, leave=False):
  	pass
```

## display file being processed

- `set_description` updates the description of the progress bar for each iteration

``` python
pbar = tqdm(glob.glob("logs/*.txt"))
for file in pbar:
    pbar.set_description(file)
		# process file
```



