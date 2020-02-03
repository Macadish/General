# Anaconda
* [Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
    * Create the environment from the environment.yml file:
        ```
        conda env create -f environment.yml
        ```
    * Activate environment
        ```
        conda activate markdown_env
        ```
    * Create environment.yml
        ```
        conda env export > environment.yml
        ```
