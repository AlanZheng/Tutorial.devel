#### Repository
https://github.com/AlanZheng/Tutorial.devel

#### What Will I Learn?
- How to recompile vim from source code to enable a feature, such as enable python3
- How to configure the vdebug for vim.
- How to configure xdebug and work together with vdebug.

#### Requirements
State the requirements the user needs in order to follow this tutorial.

- vim source code: https://github.com/vim/vim
- vdebug source code: https://github.com/vim-vdebug/vdebug
- php
- xdebug

#### Difficulty
- Intermediate

#### Tutorial Contents
1. To verify if your vim enable python3 by run: **vim --version**, it will output below information, if you see **+python3**, that means your vim enabled python3, if you see **-python3**, that means you need recompile vim from source code to enable python3. I verified vim the distribution of CentOS e17, it doesn't enable python3. So I recompiled the vim to enable python3.

   ![1539689296454](https://github.com/AlanZheng/Tutorial.devel/blob/master/vim_version.png)

2. Get the vim source code from : https://github.com/vim/vim by below command:

   ```
   git clone https://github.com/vim/vim.git
   ```

   Then changing the directory into vim source code, to run ./configure --enable-python3interp, after that you can compile vim by make command. When make done, your new vim should in src directory, so changing the directory into src, and run ./vim --version to check if python3 enabled. If compiling successfully, I believe the ourput will be **+python3** as above screenshot picture.

3. Get the vdebug source code from https://github.com/vim-vdebug/vdebug.git by below command:
    ```
    git clone https://github.com/vim-vdebug/vdebug.git`
    ```
    Then copy/move its content in your ~/.vim/ directory. You should call :helptags ~/.vim/doc in vim to generate the necessary help tags, after that, to run :help vdebug in vim, if you see something like below, that means your vdebug worked well with vim.

    ![1539691265468](https://github.com/AlanZheng/Tutorial.devel/blob/master/vdebug_doc.png)

4. Add below code into your ~/.vimrc 
    ```
    let g:vdebug_options = {}
    let g:vdebug_options["port"] = 7000
    ```

5. Configure your xdebug, you should add below code into your php.ini:
    ```
    xdebug.remote_enable=1
    xdebug.remote_host=127.0.0.1
    xdebug.remote_port=7000
    xdebug.remote_log="/tmp/xdebug.log"
    ```
    NOTE: the xdebug's port must same with vdebug's as above.

    To create a file phpinfo.php, and put below code:
    ```
    <?php phpinfo(); ?>
    ```
    Then to verify if xdebug configure worked well:
    ```
    php phpinfo.php | grep xdebug
    ```

6. Open a php file by vim, then press F10 to set a break point to cursor line, then press F5 to let vdebug waiting for connection as below.

    ![1539692284118](https://github.com/AlanZheng/Tutorial.devel/blob/master/vdebug_break.png)

7. After that to access this php from browser(firefox/chrome), the  xdebug should work now, and you will able to see debug status in the vim.

    ![1539696328484](https://github.com/AlanZheng/Tutorial.devel/blob/master/vdebug_debug.png)

    If there is anything won't work for your case, please contact me freely.

#### Proof of Work Done
https://github.com/AlanZheng/Tutorial.devel