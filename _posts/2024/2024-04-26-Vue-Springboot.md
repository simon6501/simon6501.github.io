---
layout: post
title: Webpage development based on Vue and Springboot
---

* TOC
{:toc}

## Vue Configuration - VS Code
### Configuration of environment - Windows
#### 1. Install Node.js
- Install Node.js and npm

Navigate to <a href="https://nodejs.org/en/download">`https://nodejs.org/en/download`</a> and download Node.js with version `16.20.2`. Make sure to choose the correct one between `x64` and `x86`. Reboot the PC after the installation.

- Verifies the right Node.js version is in the environment: should print `v16.20.2`
{% highlight js %}
node -v
{% endhighlight %}

- Verifies the right NPM version is in the environment: should print `v8.19.4`
{% highlight js %}
npm -v
{% endhighlight %}

#### 2. Cd project folder
Open terminal in Vscode, make sure the current folder of terminal is the project folder like `WarehouseManagerVue`.

- 镜像
{% highlight js %}
npm config set registry https://registry.npm.taobao.org
{% endhighlight %}

- Install all dependencies (needs some time: about 1 minute)

Make sure cmd is in the project folder to install all necessary dependencies for this specefic folder.
{% highlight js %}
npm install
{% endhighlight %}

- Run the project
{% highlight js %}
npm run dev
{% endhighlight %}

Navigate to <a href="http://localhost:8080">`localhost:8080`</a>. You will see the page like this:
![Login page](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/login-page.png){: style="height: 400px; margin: 0 auto;"}
<div class="caption">
  Login page
</div>

### Configuration of environment - MacOS
#### 1. <del>Install Node.js by brew</del> **Not working!!** Because it's not possible for not latest versions
- Install brew:
{% highlight js %}
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
{% endhighlight %}

- Check if 'homebrew' is installed by:
{% highlight js %}
brew -v
{% endhighlight %}

- Install Node.js by homebrew (note version '8, 10, 12, 14, 16, 17' is needed for this project):
{% highlight js %}
brew install node
{% endhighlight %}

> Path of homebrew:
>
> /usr/local/HomeBrew
>
> Folder of all packages installed by HomeBrew:
>
> /usr/local/Cellar/
>
> Installation package of npm:
>
> /usr/local/lib/node_modules/npm
>
> The storage location of npm global download template:
>
> /usr/local/lib/node_modules/npm/node_module

#### 2. Install Node.js by NVM
- Installs NVM (Node Version Manager)
{% highlight js %}
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
{% endhighlight %}

- Reopen the terminal and download and install Node.js
{% highlight js %}
nvm install 16
{% endhighlight %}

- Verifies the right Node.js version is in the environment: should print `v16.20.2`
{% highlight js %}
node -v
{% endhighlight %}

- Verifies the right NPM version is in the environment: should print `v8.19.4`
{% highlight js %}
npm -v
{% endhighlight %}

#### 3. Cd project folder
The same as `Configuration of environment - Windows`.

If there is error `sh: xxxx/WarehouseManager1/WarehouseManagerVue/node_modules/.bin/vue-cli-service: Permission denied`, try `chmod 777 node_modules/.bin/vue-cli-service`, which give the permission.

## Springtboot Configuration - IntelliJ IDEA
### Configuration of environment - Windows
#### 1. Install Intellij IDEA Ultimate

#### 2. Open the project folder 'WarehouseManagerApi'
Everything is already configured well inside the project.

#### 3. Test with one easy controller 'HelloWorldController'
Create a new controller under the `controller` folder to test the function. This will not have any impacts on other existing functions.
{% highlight js %}
package com.rabbiter.controller;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

@RestController
public class HelloWorldController {

        @GetMapping("/hello")
        public String hello() {
            return "Hello World!";
        }

        @GetMapping("/hello/{name}")
        public String hello(@PathVariable String name) {
            return "Hello " + name + "!";
        }
}
{% endhighlight %}

Click `Run WarehouseSystemApplication` button. Everthing works well if you can see the following lines inside Console:
![Springboot](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/springboot-success.png){: style="height: 250px; margin: 0 auto;"}
<div class="caption">
  The content in console if everthing is already configured well
</div>

Navigate to <a href="http://localhost:8002/hello">`localhost:8002/hello`</a>, check whether "Hello World!" is printed out.

Navigate to <a href="http://localhost:8002/hello/simon">`localhost:8002/hello/simon`</a>, check whether "Hello Simon!" is printed out.

> If there is error like 'Jdk 8 is missing', just let IDE fix it automatically because everything is already configured well in project settings.

### Configuration of environment - MacOS
The same as `Configuration of environment - Windows`.

## MySQL Configuration
### Configuration of environment - Windows
#### 1. Create a local MySQL server by 'MySQL Community Server'
Navigate to <a href="https://dev.mysql.com/downloads/mysql/">`https://dev.mysql.com/downloads/mysql/`</a> to download MySQL Community Server. It's better to download version `8.3.0`.

Note that the root password is selected as `123456789i`, which should be followed as the same as the settings in Springboot project.
![MySQL Windows](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/mysql-install.png){: style="height: 350px; margin: 0 auto;"}
<div class="caption">
  In windows, just use the default settings. For root password, use '123456789i'.
</div>

![MySQL](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/mysql.png){: style="height: 350px; margin: 0 auto;"}
<div class="caption">
  In macOS, just use the default settings. For root password, use '123456789i'.
</div>

#### 2. Connect to local server and create database 'MySQL Workbench'
I personally suggest using MySQL Workbench for the configuration of the local MySQL server and database.

- Install MySQL Workbench.
![MySQL Workbench](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/mysql-workbench.png){: style="height: 350px; margin: 0 auto;"}
<div class="caption">
  The GUI of Workbench
</div>

- Connect to the local MySQL server created before.
Setup new connection with:
> hostname: localhost
> 
> port: 3306
> 
> username: root
>
> password (store in vault): 123456789i

- Use the Query to create database
Open one SQL Query and type the following:
{% highlight js %}
-- Create the database
CREATE DATABASE IF NOT EXISTS warehouse_manager;

-- Use the database
USE warehouse_manager;
{% endhighlight %}

![MySQL Workbench Create](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/mysql-create.png){: style="height: 200px; margin: 0 auto;"}
<div class="caption">
  Create database
</div>

It can be seen that one database is created with the name of `warehouse_manager`, which should be the same as `application.yml` file in Springboot folder in IntelliJ IDEA. Set `warehouse_manager` as the default schema.

Change the `password` if you are not using `root` during the MySQL server set-up. See the figure below:
![Application yml](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/application-yml.png){: style="height: 200px; margin: 0 auto;"}
<div class="caption">
  Application yml file
</div>

- Use the Query to set-up structures for all tables
Similar as last step, go to the same page where you can input queries. All queries are already generated and stored in `warehouse_manager.sql` file inside Springboot folder in IntelliJ IDEA. So just copy everthing there to the MySQL workbench and run.
![MySQL Add](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/mysql-add.png){: style="height: 350px; margin: 0 auto;"}
<div class="caption">
  Add tables and some entries
</div>

It can be seen the tables and some entries are already added to the database. You can use the users in `user` table to **login**.
![user table](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/user-table.png){: style="height: 200px; margin: 0 auto;"}
<div class="caption">
  The initial content in user table
</div>

- It's also feasible to connect to the database and server in IntelliJ IDEA (not necessary)

- Login the webpage to check if everything is configured well

Firstly, make sure the Vue is running by `npm run dev`, Springboot is runing by clicking `Run WarehouseSystemApplication` button and database is configured well as introduced before.

Try the users shown above to login the webpage. For example, use `admin` and `123456` to login. After login, the web content is shown as below:
![login](../../../../public/images/posts/2024/2024-04-26-Vue-Springboot/after-login.png){: style="height: 350px; margin: 0 auto;"}
<div class="caption">
  The content shown up after login
</div>

> If there is any problem that login is not successful, go to console to check the bug. Mostly, the problem is with database connection like the password is wrong or it's not set up well.

### Configuration of environment - MacOS
The same as `Configuration of environment - Windows`.