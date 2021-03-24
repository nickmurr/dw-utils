# Init

1. To bind your project with this submodule:
   
    ```shell
    git submodule add https://github.com/nickmurr/dw-utils
    ```

2. To clone project with submodule:

   *   ```shell
          git submodule init
          git submodule update
       ```
      
   or

   *  
      ```shell
       git clone --recursive "your repo"
      ```
3. To fetch all updates:

   ```shell
      git submodule foreach git pull origin main 
   ```
   where `main` = branch
