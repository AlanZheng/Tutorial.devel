#### Repository
https://github.com/AlanZheng/Tutorial.devel

#### What Will I Learn?
- How to recompile vim from source code to enable a feature, such as enable python3
- How to configure the vdebug for vim.
- How to configure xdebug and work together with vdebug.

#### Requirements
- CentOS e17
- vim source code: https://github.com/vim/vim
- vdebug source code: https://github.com/vim-vdebug/vdebug
- PHP 5.6.38
- xdebug 2.5.5

#### Difficulty
- Intermediate

#### Tutorial Contents
1. Verifying vim information by run: **vim --version** to see its output  is **+python3 ** or **-python3**, plus symbol means this feature enable, otherwise disabled. The default vim distribution disabled python3 on CentOS e17. So we have recompiled the vim from source code to enable it.

   ![vim_version](https://github.com/AlanZheng/Tutorial.devel/raw/master/vim_version.png)

2. Get the vim source code from : https://github.com/vim/vim by below command:

   ```
   git clone https://github.com/vim/vim.git
   ```

   Then changing the directory into vim source code to run **./configure --enable-python3interp=yes**, after that just type make command to compile it. if things done you can find the vim executable in src directory, so goes into src directory and run **./vim --version** to check again. I believe the output will have **+python3** as above picture. Now you can install the new vim to replace the default one.

3. Get the vdebug source code from https://github.com/vim-vdebug/vdebug.git by below command:
    ```
    git clone https://github.com/vim-vdebug/vdebug.git`
    ```
    Then copy/move its content in your ~/.vim/ directory. You should call **:helptags ~/.vim/doc** in vim to generate the necessary help tags, after that to run **:help vdebug** in vim, if you see something like below, that means your vdebug worked well with vim.

    ![vdebug_doc](https://github.com/AlanZheng/Tutorial.devel/raw/master/vdebug_doc.png)

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

6. To create a file phpinfo.php, and put below code in it.
    ```
    <?php phpinfo(); ?>
    ```
    Then to verify if xdebug configure worked well:
    ```
    php phpinfo.php | grep xdebug
    ```

7. Open a php file by vim, then press **F10** to set a break point to cursor line, then press **F5** to let vdebug waiting for connection as below.

    ![vdebug_break](https://github.com/AlanZheng/Tutorial.devel/raw/master/vdebug_break.png)

7. After that to access this php from browser(firefox/chrome), the  xdebug should work now, and you will able to see debug status in the vim, more vdebug command you can type **:help vdebug** in vim.

    ![vdebug_debug](https://github.com/AlanZheng/Tutorial.devel/raw/master/vdebug_debug.png)

    If there is anything won't work for your case, please contact me freely.

#### Proof of Work Done
https://github.com/AlanZheng/Tutorial.devel