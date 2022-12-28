## Reproducible Research

- [YT](https://www.youtube.com/watch?v=se7LNICECqI&list=PL20S5EeApOSuFC7PhHtCWtCsqpNKXM64Q&index=5)

1. Use config files

    - yaml tends to be best b/c you can add comments inline
    - separate one for each experiment (copy from a template)
    - hydra for loading config file

2. Effective checkpointing

    - Save as often as your resources permit
    - save model checkpoint for prev epoch and one for best performing epoch
    - can load from a prev checkpoint now if it fails at some point during training
    - should write the code for saving/loading this stuff once, test it well, and never rewrite it again

3. Logging

    - use services like tensorboard (most common) or wandb (more interactive)

4. Set the seed for all randomization sources

    - Don't optimize the seed
    - Report an average of different seeds for model variance
    - watch out for weirdness with the GPU

    ```python
    def set_seed(seed):
      random.seed(seed)
      np.random.seed(seed)
      torch.manual_seed(seed)
      if torch.cuda.is_available():
        torch.cuda.manual_seed(seed)
        torch.cuda.manual_seed_all(seed)
        torch.backends.cudnn.deterministic = True
        torch.backends.cudnn.benchmark = False
      os.environ["PYTHONHASHSEED"] = str(seed)
    ```

5. Version your code

    - commit early and often w/ descriptive messages
    - tag versions of project to separate major decisions
    - separate branch for proof of concepts

6. Track your data too

    - git is easiest but not always feasible for large file sizes
    - backup data occasionally to cloud service
    - compute md5 of data directory and save in config file (which is added to git)
        - compare md5 hash of config file to actual directory being read during experiment

    ``` python
    def md5_update_from_dir(directory: Path, hash):
      assert directory.is_dir()
      for path in sorted(directory.iterdir(), key=lambda p: str(p).lower()):
      	hash.update(path.name.encode())
        if path.is_file():
          with open(path, "rb") as f:
            for chunk in iter(lambda: f.read(4096), b""):
            	hash.update(chunk)
        elif path.is_dir():
          hash = md5_update_from_dir(path, hash)
     	return hash
    
    def md5_dir(directory):
      return md5_update_from_dir(directory, hashlib.md5()).hexdigest()
    ```

    - if releasing a dataset, add a data sheet (readme for the dataset)

7. Maintain notebooks

    - folder just for jupyter notebooks
    - separate notebooks for data analysis, results analysis, plot generation, table generation

8. Report results with error bars

    - once pipeline is done, run experiment with multiple seeds and report the variance in the results
        - or could run with multiple datasets if possible
    - have seed in the config file for reproducible runs
    - pick arbitrary seeds (don't grid search for best ones)
    - plot with error bars and add confidence intervals in the table 

9. Manage dependencies

    - collect all dependecnesi for final release for easy reproduction of the env
    - `pip freeze > requirements.txt`
    - Docker or Singularity (more common for HPC) container is the ideal

10. Open source your research

    - squash all commits in public main branch to a single commit before making repo public 
    - ensure all api keys or secrets are removed from the code
    - format for readability
    - document code
    - Readme should have:
        - dependencies, training scripts, eval scripts, pre-trained models, and results
    - nice to have a contributing guide and blog post

11. Test and validate setup on another machine 

    - test loading and inference of your model
    - this is where any final hardcoding bugs will show themselves